# AutoRPG – Engine Specification (Deterministic Simulation)

This document defines the **runtime simulation rules** for AutoRPG.
It is **deterministic**: given the same inputs, the same outcomes occur.

The engine spec describes:
- time and ticks
- action scheduling (initiative)
- targeting and threat
- hit/crit resolution
- damage resolution and status timing
- encounter loop and run lifecycle

Content catalogs (weapons, armor, enemies, biomes) are defined elsewhere.

---

## 1. Determinism & State

### 1.1 Determinism Guarantee
The simulation contains **no random rolls**.
All “chance” concepts (hit, crit, procs) are implemented via **accumulators / fixed cycles**.

### 1.2 Stable Identity
Every entity created for an encounter has a stable:
- `entity_id` (monotonic per encounter)
- `side` (player / enemy)
- `spawn_order` (derived from entity_id)
- `archetype`, `race`, `weapon`, `armor`, `active_prefixes`, `active_statuses`

Tie-breakers always use:
1) `side` (player first where specified)  
2) `spawn_order` (lower first)

### 1.3 Core Combat State per Entity
Each entity tracks:
- `hp_current`, `hp_band` (Fragile / Low / Normal / High / Massive — see core.md Health scale)
- `position_band` (Melee / Ranged / Out-of-Range)
- `next_action_tick`
- `threat_table` (if enemy AI uses threat; player can also use for taunt logic)
- `hit_accumulator`
- `crit_accumulator`
- active statuses with: `remaining_duration_ticks`, `stack_power`, `stack_rules`

---

## 2. Time & Tick Model

### 2.1 Global Tick
Combat advances in discrete ticks:
- Tick is the smallest time step in the simulation.
- All timers are measured in ticks.

### 2.2 Update Order within a Tick
Within each tick, the engine resolves:

1. **Scheduled actions** (entities whose `next_action_tick == current_tick`)
2. **On-hit / on-action effects** (immediate)
3. **Damage resolution** (type → armor → race → modifiers)
4. **Status application** (including new DOT application)
5. **DOT ticks** (for statuses that tick this tick)
6. **Duration decay** (statuses / temporary effects)
7. **Death checks & removals**
8. **Phase / encounter transitions**

This order is strict and must not vary.

### 2.3 Simultaneous Actions
If multiple entities act on the same tick, action resolution order is:

1) Player-side entities  
2) Enemy-side entities  
Within each side: ascending `spawn_order`

This ensures deterministic repeatability and player-favoring fairness.

---

## 3. Action Scheduling (Initiative)

### 3.1 Action Interval
Each entity’s action interval is derived from:
- the chosen attack skill’s **base speed tier**
- modifiers from prefixes, statuses, biome effects, and armor penalties (if applicable)

Speed modifies **how often** an entity acts, not who goes first.

### 3.2 Scheduling Rule
When an entity completes an action at tick `t`, it schedules its next action:

`next_action_tick = t + action_interval_ticks`

### 3.3 Modifiers Priority
If multiple speed modifiers apply, resolve them in this order:

1) Skill base speed tier  
2) Status effects (e.g., Freezing)  
3) Prefix modifiers (e.g., Rapid, Heavy, Frenzied)  
4) Armor speed penalty  
5) Biome / environmental modifiers

Only one speed-affecting prefix may apply if your content rules enforce that cap.

### 3.4 No Speed “Skipping”
Speed cannot cause an entity to act twice while another eligible entity is skipped on the same tick.
If two entities share a tick, they resolve by the simultaneous action order in 2.3.

---

## 4. Targeting & Threat (Deterministic)

### 4.1 Valid Target Set
An entity may only target enemies that are:
- alive
- reachable in the current `position_band` considering weapon reach/range rules
- not protected by an absolute immunity (rare; bosses may temporarily do this)

If no valid targets exist, the entity performs no action and reschedules normally.

### 4.2 Default Target Priority (Global)
Unless overridden by archetype rules, select the target by:

1) **Valid in reach**
2) **Highest threat** (if threat is used; see 4.4)
3) **Lowest effective HP**
4) **Lowest spawn_order**

**Effective HP** is an abstract ordering:
- Lower HP band is always “lower”
- If same band, compare `hp_current` if numeric exists; otherwise use a stable proxy:
  - “recent damage taken” (higher recent damage implies lower remaining)
  - if still tied, `spawn_order`

### 4.3 Archetype Target Overrides
Archetypes may override step (2) and (3) only:

- Tank: prioritize highest threat
- Assassin: prioritize lowest effective HP
- Sniper: prioritize lowest armor effectiveness (weakest to chosen damage type)
- Controller: prioritize highest impact (entities with strongest output or most allies nearby)
- Swarm: prioritize lowest spawn_order among valid targets (to avoid pseudo-random)
- Bruiser: use default priority (no override)
- Skirmisher: use default priority (no override)
- Charger: prioritize highest effective HP (burst the toughest target)

Overrides must remain deterministic.

### 4.4 Threat Model (Deterministic)
Threat exists per encounter and resets between encounters.

Threat is generated as follows:
- When entity A deals damage to entity B, B increases threat toward A by the **damage band impact**.
- When entity A applies a control status to B (Stun/Root), B increases threat toward A by a fixed control impact.
- Tank archetype gains a passive threat bias (acts like extra threat on all actions).

Threat decay:
- Threat does not decay by default within an encounter.
- If needed later, decay must be deterministic and tick-based.

Tie-breaker:
- If threat equal, use lowest effective HP, then spawn_order.

---

## 5. Hit & Crit Resolution (No RNG)

### 5.1 Accumulator Model
Hit and crit are resolved via accumulators per entity:

- Each action adds `hit_gain` and `crit_gain` based on skill tiers and modifiers.
- When an accumulator reaches a threshold, it triggers and subtracts the threshold.

This makes "chance" predictable over time.

### 5.1.1 Tier-to-Accumulator Mapping

Accumulator gains are derived from the relative tier labels defined in core.md.

| Tier | Accumulator Gain (relative) |
|-----|----------------------------|
| Very Low | Slowest accumulation |
| Low | Below-average accumulation |
| Normal | Baseline accumulation |
| High | Above-average accumulation |
| Very High | Fastest accumulation |

The exact numeric values are implementation-defined but must preserve the tier ordering.
A `None` tier means the accumulator never gains (e.g., Crit = None means no crits).

### 5.2 Hit Resolution
- If the attack is eligible to hit, add `hit_gain`.
- If hit accumulator triggers: the attack hits.
- If it does not trigger: the attack misses.

Hit gains are derived from the **hit chance tier** (Very Low .. Very High).
Higher tiers gain faster.

### 5.3 Crit Resolution
- Only if the attack hits:
  - add `crit_gain`
  - if crit accumulator triggers: crit occurs

Crit gains are derived from the **crit tier** and crit modifiers.
Crit never occurs on a miss.

### 5.4 Boss Immunity Adjustments
Bosses may reduce:
- hit_gain against them (evasion-like)
- crit_gain against them (anti-burst)
But may never make hit/crit impossible unless explicitly stated for a phase.

---

## 6. Damage Resolution

### 6.1 Resolution Order (Canonical)
When an attack hits, resolve damage in this order:

1) Base damage band from weapon + skill damage modifier
2) Damage type interactions (physical/elemental/exotic)
3) Armor type resistance / vulnerability
4) Race resistance / weakness
5) Material–damage interaction (bonus damage if weapon material matches race material weakness)
6) Prefix and status modifiers (e.g., Vulnerable, Corroded)
7) Apply final damage to HP

### 6.2 Armor & Resistance Rules
- Resist reduces effective damage impact by one band (conceptually).
- Vulnerability increases damage impact by one band.
- If multiple sources apply:
  - resist and vulnerability cancel first
  - remaining effects apply once
No **single source** may apply more than one band shift. The exception is resistance stacking (see core.md Section 1): when armor and race both resist the same type, the combined strong resistance applies a two-band shift. This is the only case where stacking exceeds one band.

### 6.3 DOT Damage
DOT effects apply damage on DOT tick steps, not on the initial application step.
DOT damage uses its own band and may scale with target HP band.

---

## 7. Status Application & Timing

### 7.1 Application Timing
Statuses are applied during step (4) of tick order (2.2), after damage is resolved.

### 7.2 Duration & Stacking
Each status defines:
- stacking rule: None / Duration / Power
- duration in ticks (abstract tier → ticks mapping)
- tick cadence: every tick, every N ticks, or phase-based

### 7.3 DOT Tick Timing
DOT ticks occur during step (5) of tick order (2.2).

DOT tick ordering:
- resolve all DOTs on player-side first
- then enemy-side
- within side: spawn_order
- within entity: status list order (stable)

### 7.4 Control Effects
Control statuses (Stun, Root) modify:
- action execution eligibility
- movement eligibility (if movement exists)
They do not delete scheduled actions; they prevent execution and force reschedule.

---

## 8. Positioning, Reach, and Movement

### 8.1 Abstract Position Bands
The engine uses abstract bands:
- Melee
- Ranged
- Out-of-Range

### 8.2 Reach Validation
A weapon’s reach determines which bands it can hit:
- Short: Melee band only
- Medium: Melee band only, but strikes before Short reach in action resolution
- Long: Melee + Ranged bands
- Ranged label: Ranged band only (cannot hit Melee unless specified)

### 8.3 Movement
Movement exists as a **passive system**, not a player action:
- Entities are assigned a position band at encounter start based on weapon reach (Short/Medium → Melee, Long/Ranged → Ranged)
- Entities do not actively move between bands during combat
- Rooted status prevents forced repositioning (from boss abilities or hazards)
- Bosses and hazards may force repositioning during phase transitions
- "Move out of area" hazard avoidance means the entity's position band changes at the end of the current tick if not Rooted

This keeps combat simple for AutoRPG while giving Rooted and positioning meaningful roles.

### 8.4 Non-Attack Actions
Some skills do not deal damage (e.g., summon, heal). These follow the same scheduling rules as attacks but skip hit/crit resolution and damage resolution. They apply their effects during step (2) of tick order (2.2) as on-action effects.

---

## 9. Encounter Execution Loop

### 9.1 Encounter Start
On encounter start:
- spawn entities
- assign spawn_order
- initialize accumulators and next_action_tick
- apply biome affixes and encounter modifiers

### 9.2 Encounter End
An encounter ends when:
- one side has no living entities, or
- a boss phase transition ends combat explicitly

### 9.3 Encounter Rewards
On encounter end:
- rewards are generated deterministically based on:
  - encounter rarity
  - biome node rules
  - enemy rarity distribution
- duplicate conversion rules apply

---

## 10. Boss Phases (State Machine)

### 10.1 Phase Representation
Boss phases are a deterministic state machine:
- each phase defines allowed skills, prefixes, resistances, targeting rules
- phases define triggers: HP threshold, time, event, resource

### 10.2 Transition Timing
Phase transitions occur during step (8) of tick order (2.2) after death checks.

### 10.3 Transition Effects
Phase transitions may:
- cleanse specific statuses (explicit list)
- grant temporary control immunity
- spawn adds
- change targeting override rules

Bosses must always telegraph a phase change.

---

## 11. Run Lifecycle (Engine)

### 11.1 Run Start
A run begins when:
- world map is generated (node graph)
- run variables reset (momentum, run buffs)
- player loadout initialized

### 11.2 Run Progression
During a run:
- nodes are resolved sequentially (or by traversal rules)
- crafting opportunities may occur at designated nodes
- world state may be influenced but not fully rewritten per node

### 11.3 Run End
A run ends when:
- player is defeated, or
- a run-ending boss is defeated, or
- player exits

### 11.4 Persistence
- Meta progression persists always.
- Unlock progression persists always.
- Run progression resets.
- World state updates apply at run end (or at milestone nodes if specified).

---

## 12. Serialization Requirements

To support offline progress and pause/resume:
- full encounter state must serialize deterministically
- tick count, entity states, accumulators, threat tables, and scheduled actions must persist
- loading must reproduce outcomes exactly

---

## 13. Engine Design Principles

- Determinism over randomness
- Complexity over inflation
- Predictability over surprise
- Debuggability over obscurity
- Content grows without engine refactors

This engine spec is the stable foundation for all content modules.

---

## 14. Content Dependencies

This section maps which core.md sections each engine section depends on.

| Engine Section | Depends on (core.md) |
|---------------|---------------------|
| 2. Time & Tick Model | Section 1 (Relative Value Scales — speed tiers) |
| 3. Action Scheduling | Section 3.2 (Attack Skills — speed tier), Section 4.1 (Prefixes — speed modifiers) |
| 4. Targeting & Threat | Section 6.1 (Archetypes — targeting overrides) |
| 5. Hit & Crit Resolution | Section 3.2 (Attack Skills — hit/crit tiers) |
| 6. Damage Resolution | Section 2.1 (Damage Types), Section 5.1 (Armor), Section 6.2 (Races), Section 1 (Resistance Stacking, Material–Damage Interactions) |
| 7. Status Application | Section 4.3 (Status Effects — types, stacking rules) |
| 8. Positioning, Reach & Movement | Section 3.1 (Weapons — reach), Section 4.3 (Status Effects — Rooted) |
| 9. Encounter Execution | Section 7 (Encounter & Boss Design), Section 1 (Complexity Caps) |
| 10. Boss Phases | Section 7.4 (Boss Phase Rules) |
| 11. Run Lifecycle | Section 14 (Player Progression), Section 15 (World Map & Biome Flow) |
