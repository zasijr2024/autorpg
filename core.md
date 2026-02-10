# AutoRPG – Core Content Specification

This document defines all **content systems, taxonomies, and design rules**
used by AutoRPG.

It intentionally does **not** define simulation mechanics.
All runtime behavior (ticks, targeting, damage resolution, status timing, runs)
is defined in **engine.md**, which is the canonical engine specification.

`core.md` answers:
- what entities exist
- how content is structured
- what rules content must obey
- how systems connect conceptually

---

## Table of Contents

1. Design Principles & Content Rules
   - Content Ownership Rules
   - Relative Value Scales
   - Recovery Model
   - Player HP Band
   - Biome-Specific Content
   - Resistance & Vulnerability Stacking
   - Material–Damage Interactions
   - Equipment Slots
   - Complexity Caps
2. Core Taxonomies
   - Damage Types
   - Rarities
   - Weapon & Armor Labels
3. Combat Building Blocks
   - Weapons
   - Attack Skills
   - Skill–Weapon Compatibility
4. Modifiers & Status Effects
   - Support Prefixes
   - Prefix Compatibility
   - Status Effects
5. Defense & Materials
   - Armor Types
   - Materials
6. Entity Identity
   - Archetypes
   - Races / Subtypes
7. Encounter & Boss Design
   - Encounter Composition Rules
   - Encounter Complexity Budget
   - Difficulty Scaling
   - Boss Phase Rules
   - Anti-Frustration Rules
8. Loot & Rewards
   - Loot Categories
   - Loot Sources
   - Enemy Loot Rules
   - Equipment Loot Rules
   - Inventory & Storage
   - Vendors & Currency
   - Anti-Frustration Rules
9. Player Entity
   - Player Identity
   - Skill Acquisition
10. Environmental Hazards
    - Hazard Properties
    - Hazard Interaction Rules
    - Hazard Categories
11. Crafting & Upgrades
    - Crafting Philosophy
    - Crafting Categories
    - Crafting Actions
    - Crafting Rules
    - Upgrade Paths
    - Crafting Access & Progression
12. Consumables
    - Consumable Categories
    - Consumable Rules
13. Relics
    - Relic Rarity
    - Relic Categories
    - Relic Slots & Limits
    - Relic Design Rules
14. Player Progression Axes
    - Progression Layers
    - Meta Progression Axes
    - Run Progression Axes
    - Unlock Progression Axes
    - Progression Philosophy
15. World Map & Biome Flow
    - World Structure
    - Biome Nodes
    - Biome Rules
    - Idle & AutoRPG Considerations
16. Factions & World State
    - Faction Characteristics
    - Faction Auras
    - Faction Influence Tiers
    - World State
    - Faction Design Rules
17. Anti-Power-Creep & Design Philosophy
    - Core Balance Rules
    - System Boundary Rules
    - Complexity Control
    - Design Maxims

---

## 1. Design Principles & Content Rules

These principles govern **all content creation**.

- Each concept has **one owner** (no duplication of responsibility).
- Content must not introduce new simulation rules.
- Complexity scales via **interaction**, not raw power.
- Relative tiers are used instead of absolute numbers.
- Content must remain readable and explainable.

### Content Ownership Rules

| System | Owns |
|------|------|
| Engine | Time, ticks, targeting, damage resolution |
| Weapons | Damage type, reach |
| Skills | How damage is delivered |
| Prefixes | Conditional modifiers |
| Armor | Resistances & vulnerabilities |
| Materials | Quality & crafting paths |
| Archetypes | Behavior |
| Races | Biology |
| Rarity | Complexity |
| Relics | Rule modification |
| Biomes | Context & bias |

### Relative Value Scales

All stats use **tier labels**, never raw numbers.

| Scale | Tiers |
|------|-------|
| General | Very Low, Low, Normal, High, Very High |
| Health | Fragile, Low, Normal, High, Massive |
| Speed | Very Slow, Slow, Normal, Fast, Very Fast |

Tiers map to engine behavior via engine.md. Content only references tier labels.

### Resistance & Vulnerability Stacking

- Armor resistances and race resistances are **independent layers**
- If both armor and race resist the same type → **strong resistance** (one tier above normal resistance)
- If both armor and race are weak to the same type → **severe vulnerability** (one tier above normal weakness)
- A resistance and a vulnerability to the same type **cancel out** to neutral
- No entity may become fully immune through stacking alone

### Material–Damage Interactions

- Some races have material-based weaknesses (e.g., Fey are weak to Iron)
- Attacks made with a weapon of the specified material deal **bonus damage** against that race, regardless of damage type
- Material weakness is resolved after race modifiers in the damage resolution order (see engine.md Section 6)

### Equipment Slots

The player equips:
- **1 weapon** (determines damage type, reach)
- **1 armor** (determines resistances, speed penalty)
- **1–3 relics** (passive rule modifiers; slots unlock via progression)
- **Limited active skill slots** (increase with progression milestones)

### Recovery Model

- The player **fully heals** between encounters by default
- Rest nodes grant additional benefits: cleanse lingering statuses and refresh consumable charges
- Consumable healing is for **in-combat** recovery only
- No passive HP regeneration during encounters unless granted by a prefix (Regenerating) or relic
- Boss encounters do not allow mid-fight rest; healing comes only from consumables, Leeching, or Regenerating

### Player HP Band

The player's HP band is determined by **race only**:
- Human, Elf, Dwarf: Normal
- Player HP band does not shift with emergent archetype
- Relics or progression axes may grant a one-tier HP band increase (max High)
- HP band can never reach Massive (reserved for Boss archetype)

### Biome-Specific Content

Biome files may extend core tables with biome-restricted content:
- Biome-specific weapons (extend Section 3.1)
- Biome-specific skills (extend Section 3.2)
- Biome-specific materials (extend Section 5.2)

Biome content follows all core rules. Biome-specific materials are only available within their biome and cannot be used outside it unless explicitly stated.

### Complexity Caps

Hard limits that apply at all times:

| Element | Hard Cap |
|---------|----------|
| Simultaneous statuses on one entity | 3 |
| Concurrent hazards per encounter | 2 |
| Active adds per boss encounter | 6 |
| Prefixes per entity | 3 |
| Biome affixes per node | 3 |

These caps cannot be overridden by any content system.

---

## 2. Core Taxonomies

### 2.1 Damage Types

| Damage Type | Category | Description |
|------------|----------|-------------|
| Slashing | Physical | Cutting force |
| Piercing | Physical | Penetration |
| Crushing | Physical | Blunt impact |
| Missile | Physical | Projectiles |
| Fire | Elemental | Burning |
| Cold | Elemental | Freezing |
| Electricity | Elemental | Shock |
| Acid | Elemental | Corrosion |
| Magic | Magical | Pure energy |
| Poison | Exotic | Toxic damage over time |
| Disease | Exotic | Persistent weakening |

---

### 2.2 Rarities

| Rarity | Scope | Meaning |
|------|-------|--------|
| Common | All | Baseline |
| Uncommon | All | Minor specialization |
| Rare | All | Strong identity |
| Epic | All | Rule-altering |
| Unique | Boss only | Handcrafted |

Rules:
- Skills have no rarity
- Unique rarity is reserved for bosses and boss loot

---

### 2.3 Weapon & Armor Labels

**Weapon Labels**
- Wielded
- Natural
- Innate
- Ranged

**Armor Labels**
- Worn
- Natural
- Innate

Labels are informational and used for AI, loot, and crafting logic.

---

## 3. Combat Building Blocks

### 3.1 Weapons

Weapons define **damage type and reach**, not behavior.

| Weapon | Label | Damage | Type | Reach |
|------|-------|--------|------|-------|
| Teeth | Natural | Low | Piercing | Short |
| Claws | Natural | Low | Slashing | Short |
| Paw | Natural | Normal | Crushing | Short |
| Tusks | Natural | Normal | Piercing | Short |
| Mandible | Natural | Low | Piercing | Short |
| Stinger | Natural | Very Low | Piercing | Short |
| Venom Spit | Innate | Low | Poison | Long |
| Wooden Club | Wielded | Normal | Crushing | Short |
| Wooden Sword | Wielded | Normal | Slashing | Medium |
| Wooden Spear | Wielded | High | Piercing | Long |
| Wooden Staff | Wielded | Low | Crushing | Long |
| Sling Stone | Ranged | Low | Missile | Long |
| Wooden Arrow | Ranged | Low | Piercing | Long |
| Thorn Whip | Natural | Low | Slashing | Medium |
| Branch Halberd | Wielded | High | Slashing | Long |
| Talons | Natural | Normal | Slashing | Short |
| Spines | Natural | Low | Piercing | Short |
| Wooden Axe | Wielded | Normal | Slashing | Short |
| Acid Body | Innate | Low | Acid | Short |
| Root Slam | Natural | High | Crushing | Short |
| Branch | Natural | Low | Crushing | Short |
| Fire Brand | Wielded | Normal | Fire | Short |
| Frost Shard | Ranged | Low | Cold | Long |
| Spark Rod | Wielded | Low | Electricity | Medium |
| Magic Bolt | Innate | Low | Magic | Long |

---

### 3.2 Attack Skills

Skills define **how** an attack is executed.

| Skill | Damage | Hit | Speed | Crit | Scope |
|------|--------|-----|-------|------|-------|
| Bite | Normal | Low | Fast | Normal | Single |
| Claw Swipe | Low | High | Very Fast | Low | Cleave |
| Heavy Slam | High | Low | Very Slow | High | Single |
| Pierce Thrust | Normal | Normal | Normal | Normal | Single |
| Rapid Jab | Low | High | Very Fast | Low | Single |
| Crushing Blow | High | Normal | Slow | High | Single |
| Charge Attack | High | Low | Slow | High | Single |
| Stab | Normal | High | Fast | Normal | Single |
| Sweep Attack | Low | Normal | Slow | Low | AoE |
| Precise Strike | Low | Very High | Slow | High | Single |
| Impale | High | Normal | Slow | High | Single |
| Venom Spray | Low | High | Slow | Low | AoE |
| Root Grasp | Low | High | Slow | None | Single |
| Mend | None | None | Slow | None | Ally |
| Bolster | None | None | Normal | None | Ally |

**Scope Rules**
- **Single**: Targets one enemy
- **Cleave**: Hits primary target and one adjacent entity (same position band)
- **AoE**: Hits all valid targets in the weapon's reach
- **Ally**: Targets one friendly entity (non-attack; see engine.md Section 8.4)

**Skill Notes**
- **Mend**: Restores HP to one ally. Heal strength scales with the caster's weapon damage band.
- **Bolster**: Grants temporary damage reduction to one ally for a short duration.

### 3.3 Skill–Weapon Compatibility

Not all skills work with all weapons. Compatibility is governed by weapon label.

| Skill | Compatible Labels |
|------|------------------|
| Bite | Natural only |
| Claw Swipe | Natural only |
| Heavy Slam | Any |
| Pierce Thrust | Wielded, Natural |
| Rapid Jab | Natural, Wielded |
| Crushing Blow | Wielded, Natural |
| Charge Attack | Any |
| Stab | Wielded only |
| Sweep Attack | Wielded, Natural |
| Precise Strike | Any |
| Impale | Wielded, Natural |
| Venom Spray | Innate only |
| Root Grasp | Natural, Innate |
| Mend | Any (non-attack) |
| Bolster | Any (non-attack) |

Biome-specific skills define their own compatibility in the biome file.

---

## 4. Modifiers & Status Effects

### 4.1 Support Prefixes

Prefixes modify attacks conditionally.

| Prefix | Effect |
|------|--------|
| Poisonous | Applies Poison |
| Diseased | Applies Disease |
| Bleeding | Physical DOT |
| Burning | Fire DOT |
| Freezing | Slow |
| Shocking | Interrupt |
| Corrosive | Armor reduction |
| Sundering | Armor penetration |
| Precise | Hit reliability ↑ |
| Savage | Damage ↑ / accuracy ↓ |
| Rapid | Speed ↑ |
| Heavy | Damage ↑ / speed ↓ |
| Vicious | Crit ↑ |
| Leeching | Life steal |
| Infectious | DOT spreads |
| Frenzied | Speed ↑ at low HP |
| Broodbound | Ally proximity bonus |
| Regenerating | HP regeneration |

Prefix rules:
- Early content: max 1
- Mid content: max 2
- Late content: max 3
- Only one speed-affecting prefix per entity

---

### 4.2 Prefix Compatibility

Not all prefixes are valid on all items.

**Status-applying prefixes** (Poisonous, Diseased, Bleeding, Burning, Freezing, Shocking, Corrosive, Infectious):
- Compatible with **any weapon or attack**
- Biome-biased thematically (e.g., Forest favors Poisonous, Bleeding)

**Stat-modifying prefixes** (Precise, Savage, Rapid, Heavy, Vicious, Leeching, Frenzied, Regenerating, Sundering, Broodbound):
- Weapons may receive all stat-modifying prefixes
- Armor may only receive: Regenerating, Broodbound, Heavy (speed penalty only)

**Conflict rules:**
- Savage and Precise conflict (opposing accuracy effects) — cannot coexist
- Rapid and Heavy conflict (opposing speed effects) — cannot coexist
- Frenzied and Rapid conflict (both speed-increasing) — cannot coexist
- No more than **two status-applying prefixes** per entity
- No more than **one defensive prefix** (Regenerating, Broodbound, Leeching) per entity — **Boss archetype is exempt** (bosses may have up to two defensive prefixes across their phase pool)

---

### 4.3 Status Effects

| Status | Type | Effect | Stacking |
|------|------|--------|----------|
| Poison | Exotic | DOT | Power |
| Disease | Exotic | DOT + debuff | Duration |
| Bleeding | Physical | DOT | Power |
| Burning | Fire | DOT | None |
| Freezing | Cold | Slow | None |
| Shocked | Electricity | Interrupt | None |
| Corroded | Acid | Armor ↓ | Duration |
| Weakened | Physical | Damage ↓ | None |
| Vulnerable | Any | Damage taken ↑ | None |
| Stunned | Control | No actions | None |
| Rooted | Control | No movement | None |

---

## 5. Defense & Materials

### 5.1 Armor Types

| Armor | Label | Speed | Resist | Weak |
|------|-------|-------|--------|------|
| Skin | Innate | Normal | None | None |
| Fur | Natural | Normal | Cold | Fire |
| Leather | Worn | Normal | Piercing | Cold |
| Hide | Natural | Slow | Slashing | Fire |
| Bone | Natural | Slow | Crushing | Acid |
| Chitin | Natural | Slow | Slashing | Fire |
| Hardened Chitin | Natural | Very Slow | Piercing | Fire |
| Bark | Natural | Very Slow | Piercing | Fire |
| Living Bark | Natural | Very Slow | Slashing | Fire |
| Mosshide | Natural | Normal | Cold | Fire |
| Shell | Natural | Very Slow | Missile | Crushing |
| Feathers | Natural | Fast | None | Fire |
| Chain | Worn | Slow | Slashing | Piercing |
| Plate | Worn | Very Slow | Piercing | Acid |
| Padded | Worn | Normal | Crushing | Slashing |

---

### 5.2 Materials

| Material | Weapon Effect | Armor Effect |
|--------|---------------|--------------|
| Flesh | Very weak | None |
| Leather | Flexible | Light |
| Bone | Crit-biased | Moderate |
| Wood | Standard | Light |
| Stone | Heavy | Heavy |
| Copper | Poor penetration | Light |
| Iron | Reliable | Strong |
| Steel | Crit bonus | Strong |
| Silver | Anti-magical | Magic resist |
| Gold | Decorative | None |
| Chitin | Fast | Resilient |
| Mithril | High-tier | Low penalty |

---

## 6. Entity Identity

### 6.1 Archetypes

| Archetype | Role | Health |
|----------|------|--------|
| Bruiser | Durable melee | High |
| Skirmisher | Fast attacker | Normal |
| Swarm | Weak in numbers | Fragile–Low |
| Charger | Burst initiator | Normal |
| Sniper | Ranged precision | Low |
| Controller | Debuffs | Normal |
| Tank | Damage sponge | High–Massive |
| Assassin | Burst DPS | Low |
| Boss | Multi-phase | Massive |

---

### 6.2 Races / Subtypes

| Category | Race | Resist | Weak |
|--------|------|--------|------|
| Humanoid | Human | None | None |
| Humanoid | Elf | Piercing | Crushing |
| Humanoid | Dwarf | Poison | Piercing |
| Animal | Wolf | Cold | Fire |
| Animal | Bear | Crushing | Electricity |
| Insect | Ant | Slashing | Fire |
| Insect | Spider | Poison | Fire |
| Plant | Treant | Piercing | Fire |
| Magical | Fey | Magic | Iron (material) |

---

## 7. Encounter & Boss Design

Encounter and boss design define **composition, pacing, and behavior**.
Execution is handled by the engine (see engine.md Sections 9–10).

---

### 7.1 Encounter Composition Rules

Each encounter has **one primary archetype**. Secondary archetypes support the primary role.

| Primary Archetype | Allowed Secondary Archetypes |
|------------------|-----------------------------|
| Bruiser | Skirmisher, Controller, Charger |
| Skirmisher | Swarm, Assassin, Bruiser |
| Swarm | Swarm, Controller, Assassin |
| Charger | Skirmisher, Bruiser |
| Sniper | Tank, Controller |
| Controller | Bruiser, Swarm, Skirmisher |
| Tank | Controller, Bruiser, Charger |
| Assassin | Skirmisher, Charger |
| Boss | Any (theme-consistent) |

**Encounter Size Categories**

| Encounter Type | Description |
|---------------|-------------|
| Solo | Single enemy, often rare or epic |
| Small Pack | 2–3 enemies, limited synergy |
| Standard Pack | 4–6 enemies, mixed archetypes |
| Swarm | Many weak enemies, high turnover |
| Rare Group | Fewer enemies with higher rarity |
| Boss Encounter | One boss with or without adds |

**Composition Rules**
- Biomes bias **race and enemy type**, not archetype
- Hierarchical enemies spawn in role-appropriate ratios
- Leaders spawn with followers; killing a leader may weaken remaining enemies or stop reinforcements
- Faction enemies prefer spawning together; faction presence may add **faction auras** (see Section 16)
- Each encounter should reinforce **one primary concept** (e.g., armor interaction, status effects, burst windows)

---

### 7.2 Encounter Complexity Budget

| Encounter Type | Max Archetypes | Max Prefixes (total) | Max Hazards | Max Statuses (in play) |
|---------------|----------------|---------------------|-------------|----------------------|
| Solo | 1 | 3 | 1 | 2 |
| Small Pack | 2 | 4 | 1 | 2 |
| Standard Pack | 2 | 6 | 1 | 3 |
| Swarm | 1 | 2 | 1 | 1 |
| Rare Group | 2 | 6 | 1 | 3 |
| Boss Encounter | 3 | 9 (across phases) | 2 | 3 |

These budgets are design guidelines. The hard caps from Section 1 (Complexity Caps) always apply at runtime.

---

### 7.3 Difficulty Scaling

Encounter difficulty scales via:
- Enemy count
- Rarity distribution
- Archetype complexity
- Prefix count
- Status effect frequency
- Biome affixes

Avoid scaling primarily through HP inflation.

---

### 7.4 Boss Phase Rules

Bosses are **multi-phase encounters** that change behavior rather than simply growing stronger.

**Phase Triggers**

| Trigger Type | Description |
|-------------|-------------|
| Health Threshold | Phase change at HP percentages |
| Time-Based | Phase change after duration |
| Event-Based | Triggered by actions or conditions |
| Resource-Based | Triggered by stacks or energy |

**Phase Structure Types**

| Phase Type | Purpose |
|-----------|---------|
| Introduction | Establishes boss identity |
| Escalation | Increases pressure or tempo |
| Control Phase | Focus on debuffs or terrain |
| Summoning Phase | Introduces adds or hazards |
| Burn Phase | Short burst-damage window |
| Desperation | Final high-risk phase |

**Phase Change Rules**
- Phase transitions must be **telegraphed**
- Transitions grant brief control immunity (1 tick)
- DOT effects persist unless explicitly cleansed
- Cooldowns are not reset unless specified
- Phase modifiers replace previous modifiers; they do not stack infinitely

**Phase Modifiers**

| Modifier | Effect |
|--------|--------|
| Empowered | Increased damage or speed |
| Shielded | Temporary damage mitigation |
| Enraged | Speed increases over time |
| Unstable | Periodic area effects |
| Commanding | Buffs allied enemies |
| Corrupted | Applies exotic statuses more often |

**Add & Summon Rules**
- Adds follow standard encounter rules
- Adds reinforce boss mechanics
- Killing adds may weaken the boss, delay next phase, or remove shields
- Maximum active adds: 6 (hard cap from Complexity Caps)

**Status Effects on Bosses**
- Bosses are never immune to all status effects
- Control effects have reduced duration (1 tick instead of normal)
- DOT effects are effective but capped (cannot exceed Normal damage per tick)
- Each boss has at least **one clear status weakness**
- Status resistances may change per phase

---

### 7.5 Anti-Frustration Rules

- Early encounters avoid stacking multiple control archetypes
- Only one high-tempo modifier per encounter
- Swarm encounters resolve quickly
- Encounters clearly telegraph danger
- Partial boss progress may be retained
- Repeated boss failures reduce aggression slightly

---

## 8. Loot & Rewards

Loot and rewards define progression, build diversity, and long-term motivation.
All rewards are governed by **rarity**, **biome**, and **entity identity**.

---

### 8.1 Loot Categories

| Category | Description |
|---------|-------------|
| Materials | Used for crafting, upgrading, and progression |
| Weapons | Equipable items defining damage profile and reach |
| Armor | Equipable items defining resistances and speed penalties |
| Consumables | Temporary effects or recovery items |
| Relics | Rare items with passive or rule-altering effects |
| Currency | Generic progression resource |

---

### 8.2 Loot Sources

| Source | Primary Rewards |
|------|-----------------|
| Common Enemies | Materials, small currency amounts |
| Uncommon Enemies | Improved materials, chance for equipment |
| Rare Enemies | Equipment, consumables, rare materials |
| Epic Enemies | High-quality equipment, relic chance |
| Bosses (Unique) | Unique items, relics, progression unlocks |
| Environment | Biome-specific materials and items |

---

### 8.3 Enemy Loot Rules

- Enemy rarity defines **loot complexity**, not quantity
- Enemies drop loot consistent with their race, armor type, and biome
- Swarm enemies drop reduced loot individually
- Leaders and hierarchy units have enhanced drops
- Boss loot is deterministic and identity-driven

---

### 8.4 Equipment Loot Rules

- Dropped equipment inherits the enemy's material and rarity
- Equipment rarity determines number of compatible prefixes and passive effects
- Weapons and armor never drop with incompatible prefixes (see Section 4.2)
- Skills are **never** dropped as loot

---

### 8.5 Inventory & Storage

- Materials stack infinitely — no material cap
- Equipment inventory has a limited capacity (scales with progression)
- Excess equipment is auto-salvaged into materials if inventory is full (player may set salvage threshold by rarity)
- Consumables have a carry limit per type (e.g., 3 healing items, 2 buffs)
- Relics in storage are unlimited; only equipped relics are limited by slots

### 8.6 Vendors & Currency

- Vendors appear at designated world map nodes (Event or Rest nodes)
- Vendors sell: consumables, basic materials, crafting recipes
- Vendors buy: equipment (at reduced value compared to Salvage)
- Vendor stock rotates per run and is biome-influenced
- Currency sinks: vendor purchases, crafting costs, material refinement
- Currency is never the primary progression driver — it supplements crafting and loot

### 8.7 Anti-Frustration Rules

- Duplicate loot is converted into materials or currency
- Bad-luck protection increases rarity odds over time
- Boss encounters always grant meaningful progress
- Even failed runs contribute to long-term progress

---

## 9. Player Entity

The player is an entity governed by the same systems as enemies. No special exemptions from combat rules.

---

### 9.1 Player Identity

| Property | Rule |
|---------|------|
| Race | Chosen at start; determines racial resist/weakness |
| Archetype | Not fixed; emerges from equipment and skill choices |
| Armor | Equipped; follows standard armor rules |
| Weapon | Equipped; follows standard weapon rules |
| Material | Determined by equipped items |
| Health | Determined by race (see Section 1: Player HP Band) |

---

### 9.2 Skill Acquisition

- The player begins with **one basic attack skill**
- New skills are acquired through:
  - **Biome milestones** (clearing zones, defeating bosses)
  - **Trainer encounters** (non-combat events within biomes)
  - **Relic effects** (some relics grant or modify skills)
- Skills are **never** dropped as loot
- The player may equip a limited number of active skills at once
- Skill slots increase with progression milestones

---

## 10. Environmental Hazards

Environmental hazards are non-entity threats that occupy encounters or biome zones. They use the status effect system but have no HP, armor, or loot.

---

### 10.1 Hazard Properties

| Property | Description |
|---------|-------------|
| Trigger | How the hazard activates (proximity, time, event) |
| Effect | Status effect or damage type applied |
| Duration | Persistent, timed, or one-shot |
| Avoidance | Whether positioning or speed can mitigate |

---

### 10.2 Hazard Interaction Rules

- Hazards apply effects using the standard damage resolution order (see engine.md Section 6)
- Armor and race resistances apply normally against hazard damage
- Hazards may affect **both** players and enemies
- Hazards do not stack with identical hazards; overlapping hazards refresh duration
- Boss encounters may introduce hazards during phase transitions
- Biome affixes may add or intensify hazards
- Maximum concurrent hazards per encounter: 2 (hard cap)

---

### 10.3 Hazard Categories

| Category | Examples |
|---------|----------|
| Terrain | Quicksand (Rooted), Thorns (Bleeding), Ice Patches (Slow) |
| Atmospheric | Toxic Clouds (Poison), Spore Bursts (Disease), Heat Waves (Burning) |
| Structural | Falling Debris (Crushing damage), Collapsing Ground (repositioning) |
| Magical | Ley Surges (Magic damage), Corruption Zones (Vulnerable) |

Specific hazard instances are defined per biome.

---

## 11. Crafting & Upgrades

Crafting and upgrades convert loot into **agency and long-term progression**.
They emphasize **choice, specialization, and reliability** over raw power inflation.

---

### 11.1 Crafting Philosophy

- Crafting improves **consistency before magnitude**
- Crafting never invalidates loot drops
- Upgrades enhance **how items behave**, not just their strength
- Crafting outcomes are **deterministic**: the player always knows what they will receive before committing materials
- Unique items cannot be freely crafted or replicated

---

### 11.2 Crafting Categories

| Category | Purpose |
|--------|---------|
| Weapon Crafting | Create or modify weapons |
| Armor Crafting | Create or modify armor |
| Material Refinement | Improve material quality |
| Prefix Imbuing | Add or modify compatible prefixes |
| Consumable Brewing | Create consumables from materials |

---

### 11.3 Crafting Actions

| Action | Input | Output |
|--------|-------|--------|
| Forge | Materials + Recipe | New weapon or armor |
| Upgrade | Equipment + Materials | Increased material tier |
| Reforge | Equipment + Materials | Reroll prefixes (deterministic: player chooses from valid options) |
| Salvage | Equipment | Materials (partial return based on rarity) |
| Brew | Materials + Recipe | Consumable |
| Refine | Raw Materials | Higher-tier material |

---

### 11.4 Crafting Rules

- Crafted weapons must use valid weapon type, material, and label (Wielded or Ranged only — player cannot craft Natural/Innate)
- Crafted armor must use a valid armor type and label (Worn only)
- Crafting cannot change weapon reach or damage type
- Crafting cannot remove inherent armor vulnerabilities
- Prefixes added via crafting must follow compatibility rules (Section 4.2)
- Crafted prefixes count toward rarity prefix limits
- Crafted items cannot exceed the item's maximum rarity or the player's current biome tier

---

### 11.5 Upgrade Paths

Upgrades are **branching**, not linear.

| Upgrade Path | Focus |
|-------------|-------|
| Handling | Improves speed, accuracy, or responsiveness |
| Stability | Reduces negative effects or penalties |
| Synergy | Enhances interaction with prefixes or statuses |
| Specialization | Strengthens a narrow playstyle |

- Only one primary upgrade path may be pursued per item
- Rarity determines number of upgrade stages
- Epic items unlock behavior-changing upgrades
- Unique items use bespoke upgrade rules

---

### 11.6 Crafting Access & Progression

- Crafting access is gated by **Unlock Progression** (Section 14)
- Meta progression improves crafting efficiency, not output
- Run progression may grant temporary crafting bonuses
- Crafting recipes are unlocked through biome exploration, boss defeats, and material discovery

---

## 12. Consumables

Consumables are single-use items that provide temporary effects.

---

### 12.1 Consumable Categories

| Category | Effect Type | Duration |
|---------|-------------|----------|
| Healing | Restore HP | Instant |
| Antidote | Cleanse status | Instant |
| Buff | Temporary stat boost | Timed |
| Trap | Deploy hazard | Encounter |
| Utility | Non-combat effect | Varies |

---

### 12.2 Consumable Rules

- Maximum active consumable effects: 2
- Consumables cannot replicate relic effects
- Traps follow environmental hazard rules (Section 10)
- Consumables are crafted, found, or purchased — never infinite
- Consumables never trivialize bosses

---

## 13. Relics

Relics are powerful items that modify **rules**, not raw stats.

---

### 13.1 Relic Rarity

| Rarity | Source | Behavior |
|-------|--------|----------|
| Rare | Rare enemies, boss loot | Single passive effect |
| Epic | Epic enemies, boss loot | Stronger effect with tradeoff |
| Unique | Specific boss drops only | Rule-altering; handcrafted |

Relics are **never** Common or Uncommon. They cannot be crafted from scratch but may be empowered through materials.

---

### 13.2 Relic Categories

| Category | Effect Type |
|---------|-------------|
| Passive | Always-on modifier |
| Conditional | Activates under specific conditions |
| Transformative | Alters a core rule |
| Synergy | Enhances interaction between systems |

---

### 13.3 Relic Slots & Limits

- The player starts with **1 relic slot**
- Additional slots unlock via **Progression Axes** (Section 14), up to a maximum of **3**
- Relics cannot be swapped during a run
- Relics may conflict: conflicting relics cannot occupy slots simultaneously

---

### 13.4 Relic Design Rules

- Relics enable unconventional builds
- Relics have clear tradeoffs (power has a cost)
- Unique relics are boss-bound and never repeatable
- Relics may alter complexity caps (Section 1) only if explicitly designed to do so
- Relics never grant flat stat increases — they modify behavior

---

## 14. Player Progression Axes

Progression is divided into three layers with distinct persistence and purpose.

---

### 14.1 Progression Layers

| Layer | Persistence | Purpose |
|------|-------------|---------|
| Run Progression | Resets each run | In-run momentum and power curve |
| Meta Progression | Persists always | Long-term efficiency and options |
| Unlock Progression | Persists always | Permanent new content access |

---

### 14.2 Meta Progression Axes

| Axis | Effect |
|-----|--------|
| Crafting Efficiency | Reduces material costs, unlocks recipes |
| Loot Quality | Improves rarity distribution |
| Combat Mastery | Unlocks advanced skill interactions |
| Relic Attunement | Unlocks relic slots, improves relic effects |
| Faction Standing | Unlocks faction-specific rewards |

---

### 14.3 Run Progression Axes

| Axis | Effect |
|-----|--------|
| Momentum | Temporary combat bonuses that build over encounters |
| Crafting Bonus | Run-specific crafting improvements |
| Exploration Bonus | Improved loot from environmental sources |

---

### 14.4 Unlock Progression Axes

| Axis | Effect |
|-----|--------|
| Biome Access | Unlocks new biomes |
| Rarity Tiers | Unlocks higher rarity enemies and loot |
| Crafting Recipes | Unlocks new crafting options |
| Relic Slots | Unlocks additional relic capacity |
| Skill Slots | Unlocks additional active skill capacity |

---

### 14.5 Progression Philosophy

- No axis dominates all builds
- Progress improves **consistency before power**
- Failure always grants progress
- Progression adds **options**, not flat power
- Additive scaling, never multiplicative

---

## 15. World Map & Biome Flow

The world is a connected graph of biome nodes.

---

### 15.1 World Structure

- The world map is generated per run
- Nodes represent encounters, events, crafting stations, or bosses
- Paths between nodes offer branching choices
- Boss nodes gate progression to new biome tiers

---

### 15.2 Biome Nodes

| Node Type | Content |
|----------|---------|
| Combat | Standard encounter |
| Elite | Rare/Epic encounter |
| Boss | Boss encounter (gates progression) |
| Event | Non-combat choice or opportunity |
| Crafting | Crafting station access |
| Rest | Recovery or preparation |

---

### 15.3 Biome Rules

- Each biome biases enemy races, materials, and hazards
- Biome rarity influences material quality, relic availability, and loot density
- Biomes define available affixes that modify encounters
- Biome sequencing follows difficulty progression (early → mid → late)
- Boss nodes are mandatory for biome completion
- Branching paths offer meaningful risk/reward choices

---

### 15.4 Idle & AutoRPG Considerations

- Node traversal is automatic unless branching choice is required
- Failed encounters do not force restart — player may retry or route around
- Offline progress may advance through cleared nodes
- World state changes apply at run end or at milestone nodes

---

## 16. Factions & World State

Factions are persistent organizations that influence biomes and encounters.

---

### 16.1 Faction Characteristics

Each faction defines:

| Property | Description |
|---------|-------------|
| Identity | Name, theme, and biome affinity |
| Race bias | Preferred races and archetypes |
| Aura | Passive combat effect when present |
| Influence | How strongly the faction controls a biome node |

---

### 16.2 Faction Auras

When a faction controls a biome node, its aura applies to all encounters at that node.

| Aura | Effect |
|-----|--------|
| Coordinated | Enemies act in tighter sync (reduced action interval variance) |
| Zealous | Enemies gain damage bonus at low HP |
| Fortified | Enemies gain temporary damage reduction at encounter start |
| Toxic | Every 3rd attack from any enemy applies Poison (deterministic cycle) |
| Relentless | Enemies do not flee or weaken when allies die |

---

### 16.3 Faction Influence Tiers

| Tier | Effect |
|-----|--------|
| Presence | Faction enemies may appear; no aura |
| Control | Aura active; faction enemies favored |
| Dominance | Strong aura; faction-specific affixes added |
| Stronghold | Maximum aura; boss-level faction leader present |

---

### 16.4 World State

- Factions expand, retreat, and conflict with each other
- Player actions shift world state (defeating faction enemies reduces influence, completing faction quests increases standing)
- World state persists across runs
- Faction conflict may alter biome enemy composition between runs
- World events may trigger faction invasions or retreats

---

### 16.5 Faction Design Rules

- Factions add **context**, not power creep
- Faction auras modify behavior, not raw stats
- Players interact with factions through gameplay, not menus
- No faction should be strictly better to ally with than another

---

## 17. Anti-Power-Creep & Design Philosophy

---

### 17.1 Core Balance Rules

- All bonuses are **additive**, never multiplicative
- No single system may grant more than one tier of advantage
- Consistency improvements always precede magnitude improvements
- New content adds **sideways options**, not vertical power

---

### 17.2 System Boundary Rules

- No system may duplicate another system's responsibility (see Content Ownership in Section 1)
- Engine rules are never overridden by content
- Biomes and factions add context, not new mechanics
- Relics may bend rules but never break them

---

### 17.3 Complexity Control

- Complexity caps (Section 1) are hard limits and cannot be altered by any system
- New systems must justify their existence by enabling meaningful player choices
- If a system can be expressed as content within an existing system, it should be

---

### 17.4 Design Maxims

- Complexity > numbers
- Systems > stats
- Choice > optimization
- Determinism > randomness

The core exists to support **infinite content without engine refactor**.
