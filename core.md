# AutoRPG – Core Systems Specification

This document defines all **biome-agnostic core systems** for AutoRPG.
All values are **relative**; no fixed numbers are used.

---

## Table of Contents

1. Design Principles & Global Rules
   - Resistance & Vulnerability Stacking
   - Material–Damage Interactions
   - Positioning Model
   - Relative Value Scales
2. Core Taxonomies
   - Damage Types
   - Rarities
   - Weapon & Armor Labels
3. Combat Building Blocks
   - Weapons
   - Attack Skills
4. Modifiers & Effects
   - Support Prefixes
   - Status Effects
5. Defense & Materials
   - Armor Types
   - Materials
6. Entity Identity
   - Archetypes
   - Races / Subtypes
7. Encounter & Boss Design
   - Encounter Composition Rules
   - Boss Phase Rules
8. Loot & Rewards
9. Player Entity
   - Skill Acquisition
   - Player Progression Axes
10. Environmental Hazards
11. Crafting System
12. Consumables
13. Relics  
14. Player Progression Axes
15. Crafting & Upgrade Rules
16. World Map & Biome Flow
17. Factions & World State

---

## 1. Design Principles & Global Rules

- Weapons define **WHAT hits**
- Skills define **HOW it hits**
- Prefixes define **SPECIAL EFFECTS**
- Armor Types define **RESISTANCES & VULNERABILITIES**
- Materials define **QUALITY & TIER**
- Archetypes define **BEHAVIOR**
- Races define **BIOLOGY**
- Rarity defines **COMPLEXITY & REWARD**

No system may duplicate another system’s responsibility.

### Global Combat Rules
- Attack speed comes from **skills and prefixes only**
- Armor speed penalties apply after skill speed
- Damage resolution order:
  1. Damage Type
  2. Armor Type
  3. Race modifiers
  4. Status & Prefix effects
- DOT effects tick independently of attack speed

### Resistance & Vulnerability Stacking
- Armor resistances and race resistances are **independent layers**
- If both armor and race resist the same type, the entity gains **strong resistance** (one tier above normal resistance)
- If both armor and race are weak to the same type, the entity gains **severe vulnerability** (one tier above normal weakness)
- A resistance and a vulnerability to the same type **cancel out** to neutral
- No entity may become fully immune through stacking alone

### Material–Damage Interactions
- Some races have material-based weaknesses (e.g., Fey are weak to Iron)
- Attacks made with a weapon of the specified material deal **bonus damage** against that race, regardless of damage type
- Material weakness is resolved after Race modifiers in the damage resolution order

### Positioning Model
- Combat uses an **abstract range system**, not grid-based positioning
- Three range bands: **Melee** (Short/Medium reach), **Ranged** (Long reach), **Out of Range**
- Weapon Reach determines which range band an attacker can target from
- Short reach: Melee only
- Medium reach: Melee only, but strikes before Short
- Long reach: Ranged band, cannot be used in Melee
- Movement is abstracted: entities are either engaged (Melee) or disengaged (Ranged/Out of Range)
- The Rooted status prevents changing range band
- The Charger archetype closes to Melee as its opening action

### Relative Value Scales
All numeric properties use these ordered tiers. Each tier represents a meaningful gameplay difference.

**Speed Scale** (attack/action tempo):

| Tier | Label |
|------|-------|
| 1 | Very Slow |
| 2 | Slow |
| 3 | Normal |
| 4 | Fast |
| 5 | Very Fast |

**Damage Scale** (per-hit output):

| Tier | Label |
|------|-------|
| 1 | Very Low |
| 2 | Low |
| 3 | Normal |
| 4 | High |
| 5 | Very High |

**Hit Chance Scale** (accuracy):

| Tier | Label |
|------|-------|
| 1 | Very Low |
| 2 | Low |
| 3 | Normal |
| 4 | High |
| 5 | Very High |

**Crit Scale** (critical hit likelihood):

| Tier | Label |
|------|-------|
| 0 | None |
| 1 | Low |
| 2 | Normal |
| 3 | High |
| 4 | Very High |

---

## 2. Core Taxonomies

### 2.1 Damage Types

| Damage Type | Category | Description |
|------------|----------|-------------|
| Slashing | Physical | Cutting damage |
| Piercing | Physical | Penetrating damage |
| Crushing | Physical | Blunt force |
| Missile | Physical | Ranged projectiles |
| Fire | Elemental | Burning |
| Cold | Elemental | Freezing |
| Electricity | Elemental | Shock |
| Acid | Elemental | Corrosion |
| Magic | Magical | Pure energy |
| Poison | Exotic | Toxic DOT |
| Disease | Exotic | Persistent weakening DOT |

---

### 2.2 Rarities

| Rarity | Scope | Description |
|------|-------|-------------|
| Common | All | Baseline |
| Uncommon | All | One modifier |
| Rare | All | Strong identity |
| Epic | All | Rule-altering |
| Unique | Boss only | Handcrafted |

**Rules**
- Skills have no rarity
- Unique rarity is reserved for bosses and boss loot
- Only one Epic entity per encounter

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

---

### 3.2 Attack Skills

| Skill | Damage | Hit | Speed | Crit |
|------|--------|-----|-------|------|
| Bite | Normal | Low | Fast | Normal |
| Claw Swipe | Low | High | Very Fast | Low |
| Heavy Slam | High | Low | Very Slow | High |
| Pierce Thrust | Normal | Normal | Normal | Normal |
| Rapid Jab | Low | High | Very Fast | Low |
| Crushing Blow | High | Normal | Slow | High |
| Charge Attack | High | Low | Slow | High |
| Stab | Normal | High | Fast | Normal |
| Sweep Attack | Low | Normal | Slow | Low |
| Precise Strike | Low | Very High | Slow | High |
| Impale | High | Normal | Slow | High |
| Venom Spray | Low | High | Slow | Low |
| Root Grasp | Low | High | Slow | None |

---

## 4. Modifiers & Effects

### 4.1 Support Prefixes

| Prefix | Effect |
|------|--------|
| Poisonous | Applies Poison |
| Diseased | Applies Disease |
| Bleeding | Physical DOT |
| Burning | Applies Burning status |
| Freezing | Slow |
| Shocking | Interrupt |
| Corrosive | Armor reduction |
| Sundering | Armor penetration |
| Precise | Hit chance ↑ |
| Savage | Damage ↑ / accuracy ↓ |
| Rapid | Speed ↑ |
| Heavy | Damage ↑ / speed ↓ |
| Vicious | Crit ↑ |
| Leeching | Life steal |
| Infectious | DOT spreads |
| Frenzied | Speed ↑ at low HP |
| Broodbound | Ally proximity bonus |
| Regenerating | HP regen |

**Prefix Rules**
- Early: 1
- Mid: 2
- Late: 3
- Only one speed-affecting prefix allowed

---

### 4.2 Status Effects

| Status | Type | Effect | Stacking |
|------|------|--------|----------|
| Poison | Exotic | DOT | Power |
| Disease | Exotic | DOT + debuff | Duration |
| Bleeding | Physical | DOT | Power |
| Burning | Fire | DOT | None |
| Freezing | Cold | Slow | None |
| Shocked | Elec | Interrupt | None |
| Corroded | Acid | Armor ↓ | Duration |
| Weakened | Physical | Damage ↓ | None |
| Vulnerable | Any | Damage taken ↑ | None |
| Stunned | Control | No action | None |
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

---

### 5.2 Materials

| Material | Weapon Effect | Armor Effect |
|--------|---------------|--------------|
| Flesh | Very low | None |
| Leather | Flexible | Light |
| Bone | Crit bias | Moderate |
| Wood | Standard | Light |
| Stone | Heavy | Heavy |
| Copper | Poor pen | Light |
| Iron | Reliable | Strong |
| Steel | Crit bonus | Strong |
| Silver | Bonus vs magical | Magic resist |
| Gold | Decorative | None |
| Chitin | Fast | Resilient |
| Mithril | High tier | Low penalty |

---

## 6. Entity Identity

### 6.1 Archetypes

| Archetype | Role |
|----------|------|
| Bruiser | Durable melee |
| Skirmisher | Fast attacker |
| Swarm | Weak in numbers |
| Charger | Burst initiator |
| Sniper | Ranged precision |
| Controller | Debuffs |
| Tank | Damage sponge |
| Assassin | Burst DPS |
| Boss | Multi-phase |

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

This section defines how enemies are grouped, how difficulty is expressed, and how bosses differ from normal encounters.
Encounter and boss design focuses on **behavior, composition, and pacing**, not stat inflation.

---

### 7.1 Encounter Composition Rules

Encounter composition determines how enemies are assembled into fights and how challenge is expressed.

#### Encounter Size Categories

| Encounter Type | Description |
|---------------|-------------|
| Solo | Single enemy, often rare or epic. |
| Small Pack | 2–3 enemies, limited synergy. |
| Standard Pack | 4–6 enemies, mixed archetypes. |
| Swarm | Many weak enemies, high turnover. |
| Rare Group | Fewer enemies with higher rarity. |
| Boss Encounter | One boss with or without adds. |

---

#### Archetype Distribution Rules

- Each encounter has **one primary archetype**.
- Secondary archetypes are chosen to support the primary role.
- Swarm archetypes increase enemy count but reduce individual threat.
- Tank archetypes rarely appear alone unless Rare or higher.
- Assassin and Sniper archetypes favor mixed encounters.

---

#### Archetype Mixing Guidelines

| Primary Archetype | Allowed Secondary Archetypes |
|------------------|-----------------------------|
| Bruiser | Skirmisher, Controller |
| Skirmisher | Swarm, Assassin |
| Swarm | Swarm, Controller |
| Charger | Skirmisher |
| Sniper | Tank, Controller |
| Controller | Bruiser, Swarm |
| Tank | Controller, Bruiser |
| Assassin | Skirmisher |
| Boss | Any (theme-consistent) |

---

#### Biome Influence on Encounters

- Biomes bias **race and enemy type**, not archetype.
- Biome affixes may:
  - increase encounter size
  - replace enemies with hazards
  - alter archetype availability
- Environmental encounters may substitute enemies entirely.

---

#### Hierarchy & Faction Rules

- Hierarchical enemies spawn in role-appropriate ratios.
- Leaders and queens spawn with followers.
- Killing a leader may:
  - weaken remaining enemies
  - stop reinforcements
  - remove buffs
- Faction enemies prefer spawning together.

---

#### Difficulty Scaling Axes

Encounter difficulty scales via:
- Enemy count
- Rarity distribution
- Archetype complexity
- Prefix count
- Status effect frequency
- Biome affixes

Avoid scaling primarily through HP.

---

#### Anti-Frustration Rules (AutoRPG-Focused)

- Early encounters avoid stacking multiple control archetypes.
- Only one high-tempo modifier per encounter.
- Swarm encounters resolve quickly.
- Encounters should clearly telegraph danger.

---

#### Encounter Identity Principle

Each encounter should reinforce **one primary concept**, such as:
- Armor interaction
- Status effects
- Speed vs durability
- Burst windows
- Crowd control

Encounters should not test all systems at once.

---

### 7.2 Boss Phase Rules

Bosses are **multi-phase encounters** designed around changing behavior rather than extreme durability.

---

#### Phase Triggers

| Trigger Type | Description |
|-------------|-------------|
| Health Threshold | Phase change at HP percentages. |
| Time-Based | Phase change after duration. |
| Event-Based | Triggered by actions or conditions. |
| Resource-Based | Triggered by stacks or energy. |

Bosses may use multiple trigger types.

---

#### Phase Structure Types

| Phase Type | Purpose |
|-----------|---------|
| Introduction | Establishes boss identity. |
| Escalation | Increases pressure or tempo. |
| Control Phase | Focus on debuffs or terrain. |
| Summoning Phase | Introduces adds or hazards. |
| Burn Phase | Short burst-damage window. |
| Desperation | Final high-risk phase. |

Not all bosses require all phase types.

---

#### Phase Changes

A phase transition may alter:
- Archetype
- Preferred skills
- Active prefixes
- Status resistances
- Movement behavior
- Encounter composition

Phase changes must be **telegraphed**.

---

#### Phase Modifiers

| Modifier | Effect |
|--------|--------|
| Empowered | Increased damage or speed. |
| Shielded | Temporary damage mitigation. |
| Enraged | Speed increases over time. |
| Unstable | Periodic area effects. |
| Commanding | Buffs allied enemies. |
| Corrupted | Applies exotic statuses more often. |

Phase modifiers replace previous modifiers; they do not stack infinitely.

---

#### Add & Summon Rules

- Adds follow standard encounter rules.
- Adds reinforce boss mechanics.
- Killing adds may:
  - weaken the boss
  - delay the next phase
  - remove shields or buffs
- Add density decreases over time.

---

#### Status Effects on Bosses

- Bosses are never immune to all status effects.
- Control effects have reduced duration.
- DOT effects are effective but capped.
- Each boss has at least **one clear status weakness**.
- Status resistances may change per phase.

---

#### Phase Transitions

- Phase transitions grant brief control immunity.
- DOT effects persist unless cleansed.
- Cooldowns are not reset unless specified.
- Boss repositioning may occur.

Transitions should feel impactful but fair.

---

#### Boss Difficulty Scaling

Boss difficulty scales via:
- Number of phases
- Phase complexity
- Prefix selection per phase
- Add behavior
- Environmental hazards

Avoid scaling via HP inflation.

---

#### Boss Identity Principle

Each boss should test **one primary mastery**, such as:
- Sustained damage
- Burst timing
- Crowd control management
- Add prioritization
- Environmental awareness

Bosses should not test all systems at once.

---

#### Failure & Recovery (AutoRPG-Friendly)

- Partial progress may be retained.
- Phase checkpoints may be saved.
- Repeated failures reduce aggression slightly.
- Boss encounters should teach, not punish.


---

## 8. Loot & Rewards

## 8. Loot & Rewards

Loot and rewards define progression, build diversity, and long-term motivation.
All rewards are governed by **rarity**, **biome**, and **entity identity**, not raw stats.

---

### 8.1 Loot Categories

| Category | Description |
|---------|-------------|
| Materials | Used for crafting, upgrading, and progression. |
| Weapons | Equipable items defining damage profile and reach. |
| Armor | Equipable items defining resistances and speed penalties. |
| Consumables | Temporary effects or recovery items. |
| Relics | Rare items with passive or rule-altering effects. |
| Currency | Generic progression resource. |

---

### 8.2 Loot Sources

| Source | Primary Rewards |
|------|-----------------|
| Common Enemies | Materials, small currency amounts. |
| Uncommon Enemies | Improved materials, chance for equipment. |
| Rare Enemies | Equipment, consumables, rare materials. |
| Epic Enemies | High-quality equipment, relic chance. |
| Bosses (Unique) | Unique items, relics, progression unlocks. |
| Environment | Biome-specific materials and items. |
| Events | Consumables, rare materials, special rewards. |

---

### 8.3 Rarity-Based Loot Behavior

| Rarity | Loot Behavior |
|-------|---------------|
| Common | Basic materials and currency. |
| Uncommon | Improved materials, chance for equipment. |
| Rare | Guaranteed equipment or relic chance. |
| Epic | Multiple rewards with strong synergies. |
| Unique | Handcrafted, deterministic rewards. |

---

### 8.4 Enemy Loot Rules

- Enemy rarity defines **loot complexity**, not quantity.
- Enemies drop loot consistent with:
  - their race
  - their armor type
  - their biome
- Swarm enemies drop reduced loot individually.
- Leaders and hierarchy units have enhanced drops.
- Boss loot is deterministic and identity-driven.

---

### 8.5 Weapon & Armor Loot Rules

- Dropped equipment inherits:
  - the enemy’s material
  - the enemy’s rarity
- Equipment rarity determines:
  - number of compatible prefixes
  - presence of passive effects
- Weapons and armor never drop with incompatible prefixes.
- Skills are **never** dropped as loot.

---

### 8.6 Material Drop Rules

- Materials drop based on:
  - biome identity
  - enemy armor type
  - enemy race
- Rare materials are biome-restricted.
- Environmental harvesting favors materials over equipment.
- Higher rarity enemies may drop refined materials.

---

### 8.7 Biome Reward Rules

- Each biome biases loot categories and materials.
- Biome rarity influences:
  - material quality
  - relic availability
  - environmental loot density
- Epic biomes may introduce biome-exclusive rewards.
- Unique biomes guarantee unique rewards.

---

### 8.8 Boss & Unique Rewards

- Unique bosses drop:
  - unique weapons or armor
  - relics
  - permanent progression unlocks
- Unique items:
  - do not roll random prefixes
  - may alter core rules
  - are not repeatable drops
- Defeating a boss may unlock:
  - new biomes
  - higher rarity tiers
  - world-state changes

---

### 8.9 Anti-Frustration Rules

- Duplicate loot is converted into materials or currency.
- Bad-luck protection increases rarity odds over time.
- Boss encounters always grant meaningful progress.
- Loot clarity is prioritized over surprise.

---

### 8.10 Reward Philosophy

- Rewards reinforce **player decisions**, not luck.
- Progression should feel steady and readable.
- Rarity adds depth, not randomness.
- Even failed runs contribute to long-term progress.

---

## 9. Player Entity

The player is an entity governed by the same systems as enemies. The player does not receive special exemptions from combat rules.

---

### 9.1 Player Identity

| Property | Rule |
|---------|------|
| Race | Chosen at start; determines racial resist/weakness |
| Archetype | Not fixed; emerges from equipment and skill choices |
| Armor | Equipped; follows standard armor rules |
| Weapon | Equipped; follows standard weapon rules |
| Material | Determined by equipped items |

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

### 9.3 Player Progression Axes

| Axis | Source |
|------|--------|
| Damage output | Weapon upgrades, prefixes, skills |
| Survivability | Armor upgrades, materials, resistances |
| Versatility | Skill slots, relic effects, consumables |
| Reach | Weapon choice, skill choice |

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

- Hazards apply effects using the standard damage resolution order
- Armor and race resistances apply normally against hazard damage
- Hazards may affect **both** players and enemies
- Hazards do not stack with identical hazards; overlapping hazards refresh duration
- Boss encounters may introduce hazards during phase transitions
- Biome affixes may add or intensify hazards

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

## 11. Crafting System

Crafting converts materials into equipment, consumables, and upgrades.

---

### 11.1 Crafting Rules

- Crafting requires **materials** (see Section 5.2 and biome material tables)
- Crafted items follow standard weapon, armor, and prefix rules
- Crafted item rarity is determined by:
  - material rarity
  - recipe complexity
  - crafting milestone tier
- Crafted items may have **one guaranteed prefix** chosen by the player
- Additional prefixes follow standard rarity-based prefix count rules
- Crafting recipes are unlocked through:
  - biome exploration
  - boss defeats
  - material discovery

---

### 11.2 Crafting Actions

| Action | Input | Output |
|--------|-------|--------|
| Forge | Materials + Recipe | New weapon or armor |
| Upgrade | Equipment + Materials | Increased material tier |
| Reforge | Equipment + Materials | Reroll prefixes |
| Salvage | Equipment | Materials (partial) |
| Brew | Materials + Recipe | Consumable |

---

### 11.3 Crafting Constraints

- Crafted items cannot exceed the player's current biome tier
- Unique items cannot be crafted or salvaged
- Reforging preserves the item's base type and material
- Salvaging returns materials based on the item's rarity

---

## 12. Consumables

Consumables are single-use items that provide temporary effects.

---

### 12.1 Consumable Categories

| Category | Effect Type | Duration |
|---------|------------|----------|
| Healing | HP recovery | Instant |
| Antidote | Cleanse status effect | Instant |
| Buff Potion | Stat increase | Timed |
| Resistance Elixir | Resist a damage type | Timed |
| Weapon Oil | Add prefix to next N attacks | Charges |
| Trap | Place environmental hazard | Triggered |

---

### 12.2 Consumable Rules

- Consumables are acquired through loot, crafting, or environmental harvesting
- Only one buff potion and one resistance elixir may be active at a time
- Consumable rarity affects potency (duration, strength) not effect type
- Consumables cannot replicate Unique item effects
- Traps follow environmental hazard rules (Section 10)

---

## 13. Relics

Relics are rare passive items that alter gameplay rules.

---

### 13.1 Relic Properties

| Property | Description |
|---------|-------------|
| Passive Effect | Always-on modifier to a core system |
| Slot | Relics occupy a limited number of relic slots |
| Source | Boss drops, biome milestones, rare events |
| Rarity | Rare, Epic, or Unique only |

---

### 13.2 Relic Effect Categories

| Category | Example Effects |
|---------|----------------|
| Offensive | Crit chance ↑, DOT duration ↑, bonus damage vs a race |
| Defensive | Resist a status effect, armor ↑ vs a damage type |
| Utility | Extra skill slot, consumable duration ↑, material drop ↑ |
| Rule-Altering | Change how a prefix works, modify phase trigger conditions |

---

### 13.3 Relic Rules

- Maximum **3 relics** equipped at once
- Relic effects do not stack with identical relics
- Unique relics are one-per-save
- Rule-altering relics override the specific rule they modify and note the change explicitly
- Relics cannot be crafted; they can only be found

---

## 14. Player Progression Axes

Player progression defines how the player grows stronger, gains control, and unlocks complexity over time.
Progression is split into **orthogonal axes** to avoid linear scaling, hard lock-ins, and power creep.

---

## 14.1 Progression Layers

Each progression axis belongs to exactly one layer.

| Layer | Description |
|------|-------------|
| Run Progression | Power gained within a single run and reset afterwards. |
| Meta Progression | Persistent improvements across runs. |
| Unlock Progression | Permanent access to systems, content, or options. |

---

## 14.2 Meta Progression Axes

### Axis 1: Combat Mastery  
**Layer:** Meta  
**Focus:** Core combat effectiveness  

- Improves damage consistency and crit reliability.
- Enhances interaction with armor types and archetypes.
- Reduces penalties from accuracy and damage tradeoffs.

---

### Axis 2: Speed & Tempo Control  
**Layer:** Meta  
**Focus:** Combat pacing  

- Improves base action frequency.
- Reduces negative speed modifiers.
- Improves uptime for fast-paced builds.

---

### Axis 3: Status Proficiency  
**Layer:** Meta  
**Focus:** Status effects and debuffs  

- Improves DOT effectiveness.
- Improves debuff application reliability.
- Increases effectiveness against status-resistant enemies.

---

### Axis 4: Defense & Survivability  
**Layer:** Meta  
**Focus:** Longevity and mitigation  

- Improves armor effectiveness.
- Reduces incoming status duration.
- Improves regeneration and recovery.

---

### Axis 5: Rarity Interaction  
**Layer:** Meta  
**Focus:** High-complexity content handling  

- Improves effectiveness of Rare and Epic items.
- Improves synergy handling between prefixes.
- Reduces negative side effects of high-rarity mechanics.

---

### Axis 6: Boss Adaptation  
**Layer:** Meta  
**Focus:** Boss encounters  

- Improves effectiveness during boss phases.
- Reduces punishment from repeated boss mechanics.
- Improves recovery after phase transitions.

---

## 14.3 Run Progression Axes

### Axis 7: Equipment Growth  
**Layer:** Run  
**Focus:** Temporary power within a run  

- Acquisition of stronger weapons and armor.
- Temporary bonuses and run-limited effects.
- Power resets between runs.

---

### Axis 8: Momentum  
**Layer:** Run  
**Focus:** Performance-based scaling  

- Gained by efficient victories.
- Lost through failure or attrition.
- Influences encounter difficulty and rewards.

---

### Axis 9: Risk Amplification  
**Layer:** Run  
**Focus:** High-risk, high-reward play  

- Optional difficulty escalation during a run.
- Increases rewards at the cost of danger.
- Fully optional and player-controlled.

---

## 14.4 Unlock Progression Axes

### Axis 10: System Unlocks  
**Layer:** Unlock  
**Focus:** Mechanical access  

- Unlocks new status effects.
- Unlocks advanced prefixes.
- Unlocks additional archetype behaviors.

---

### Axis 11: Biome Access  
**Layer:** Unlock  
**Focus:** World expansion  

- Unlocks new biomes.
- Unlocks higher biome rarities.
- Enables branching world paths.

---

### Axis 12: Crafting & Upgrade Access  
**Layer:** Unlock  
**Focus:** Long-term customization  

- Unlocks crafting recipes.
- Unlocks upgrade and refinement paths.
- Unlocks material specialization.

---

### Axis 13: Relic & Legacy Access  
**Layer:** Unlock  
**Focus:** Long-term identity  

- Unlocks relic slots or categories.
- Unlocks legacy-style passive bonuses.
- Enables long-term build identity without class lock-in.

---

## 14.5 Progression Interaction Rules

- No single axis may dominate all builds.
- Progression effects are additive, not multiplicative.
- Meta progression improves **efficiency**, not raw dominance.
- Run progression always resets.
- Unlock progression is permanent and non-repeatable.

---

## 14.6 Anti-Power-Creep Rules

- Progression increases consistency before magnitude.
- Complexity unlocks before numeric scaling.
- Hard counters remain valid at all stages.
- Boss mechanics are never bypassed by progression alone.

---

## 14.7 Progression Philosophy

- Progression should feel inevitable, not lucky.
- Failure still produces progress.
- Depth increases before power.
- Choice matters more than optimization.

## 15. Crafting & Upgrade Rules

Crafting and upgrades convert loot into **agency and long-term progression**.
They emphasize **choice, specialization, and reliability** over raw power inflation.

---

## 15.1 Crafting Philosophy

- Crafting improves **consistency before magnitude**.
- Crafting never invalidates loot drops.
- Upgrades enhance **how items behave**, not just their strength.
- Crafting is deterministic; outcomes are known in advance.
- Unique items cannot be freely crafted or replicated.

---

## 15.2 Crafting Categories

| Category | Purpose |
|--------|---------|
| Weapon Crafting | Create or modify weapons. |
| Armor Crafting | Create or modify armor. |
| Material Refinement | Improve material quality. |
| Prefix Imbuing | Add or modify compatible prefixes. |
| Relic Forging | Create or empower relics. |

---

## 15.3 Material Usage Rules

- Materials determine:
  - crafting eligibility
  - upgrade paths
  - maximum achievable rarity
- Higher-tier materials unlock **qualitative effects**, not flat power.
- Refined materials may replace multiple lower-tier materials.
- Biome-exclusive materials unlock biome-themed effects.

---

## 15.4 Weapon Crafting Rules

- Crafted weapons must use valid:
  - weapon type
  - material
  - label (Wielded / Natural / Innate / Ranged)
- Crafting cannot change:
  - weapon reach
  - weapon damage type
- Crafting may:
  - improve handling
  - unlock prefix slots
  - add conditional effects
- Crafted weapons respect rarity caps.

---

## 15.5 Armor Crafting Rules

- Crafted armor must use a valid armor type and label.
- Crafting cannot remove inherent vulnerabilities.
- Crafting may:
  - reduce speed penalties
  - add conditional resistances
  - interact with status effects
- Armor behavior remains readable and predictable.

---

## 15.6 Prefix Imbuing Rules

- Prefixes added via crafting must be compatible.
- Crafted prefixes count toward rarity prefix limits.
- Prefix removal or replacement is possible but costly.
- Unique items have fixed prefixes and cannot be re-imbued.

---

## 15.7 Upgrade Paths

Upgrades are **branching**, not linear.

| Upgrade Path | Focus |
|-------------|-------|
| Handling | Improves speed, accuracy, or responsiveness. |
| Stability | Reduces negative effects or penalties. |
| Synergy | Enhances interaction with prefixes or statuses. |
| Specialization | Strengthens a narrow playstyle. |

Only one primary upgrade path may be pursued per item.

---

## 15.8 Rarity & Crafting Interaction

- Crafting cannot exceed the item’s maximum rarity.
- Rarity determines:
  - number of upgrade stages
  - number of prefix interactions
- Epic items unlock behavior-changing upgrades.
- Unique items use bespoke upgrade rules.

---

## 15.9 Relic Crafting & Empowerment

- Relics are crafted or empowered, not randomly generated.
- Relics interact with:
  - progression axes
  - rarity systems
  - encounter rules
- Relics may modify:
  - global rules
  - biome behavior
  - encounter composition
- Relic effects are always explicit and limited in scope.

---

## 15.10 Anti-Power-Creep Rules

- Upgrades prioritize reliability over raw damage.
- No upgrade fully negates a counter or vulnerability.
- Crafting effects are additive, not multiplicative.
- Long-term progression widens options before increasing power.

---

## 15.11 Crafting Failure & Recovery

- Crafting never destroys items.
- Failed crafting attempts may:
  - consume materials
  - lock an upgrade path
  - introduce temporary penalties
- Failure always provides feedback and partial progress.

---

## 15.12 Crafting & Player Progression Interaction

- Crafting access is gated by **Unlock Progression Axes**.
- Meta progression improves crafting efficiency, not output.
- Run progression may grant temporary crafting bonuses.
- Crafting choices reinforce long-term build identity.

---

## 15.13 Crafting Design Principle

Crafting exists to:
- reward preparation
- reduce reliance on luck
- support diverse builds
- reinforce player intent

Crafting should never feel mandatory, but always meaningful.

## 16. World Map & Biome Flow

The world map defines **how biomes are arranged, unlocked, and traversed**.
It controls pacing, difficulty escalation, and player choice without relying on linear progression.

---

## 16.1 World Structure

- The world is composed of interconnected **biome nodes**.
- Each node represents a biome instance with a defined rarity.
- Players progress by choosing paths between nodes.
- Paths may branch, converge, or loop.

The map is **semi-linear**:
- early progression is guided
- later progression is player-directed

---

## 16.2 Biome Nodes

Each biome node is defined by:

- Biome type (Forest, Swamp, Mountain, etc.)
- Biome rarity
- Active biome affixes
- Encounter density
- Environmental loot bias

Biome nodes are **generated per run**.

---

## 16.3 Biome Rarity Distribution

| Biome Rarity | World Role |
|-------------|------------|
| Common | Early progression, low risk |
| Uncommon | Mid progression, light challenge |
| Rare | High challenge, strong rewards |
| Epic | Late-game spikes, rule-altering |
| Unique | Boss arenas, narrative moments |

Rules:
- Only one Epic biome may exist per map branch.
- Unique biomes appear only at progression milestones.
- Biome rarity affects **rules**, not just enemies.

---

## 16.4 Biome Connectivity Rules

- Biomes connect through visible paths.
- Paths indicate **risk vs reward**, not exact outcomes.
- Some paths may:
  - increase biome rarity
  - introduce new affixes
  - alter encounter composition
- Backtracking is limited but possible.

---

## 16.5 Branching & Choice

- Players are frequently offered **meaningful choices**:
  - safer route vs risky route
  - familiar biome vs unknown biome
  - material-focused vs relic-focused paths
- Choices should affect:
  - loot types
  - enemy composition
  - progression pace

No path is strictly optimal.

---

## 16.6 Biome Sequencing Rules

- Early biomes favor:
  - Common and Uncommon rarity
  - simple affixes
  - limited archetype variety
- Mid biomes introduce:
  - Rare enemies
  - complex affixes
  - mixed encounters
- Late biomes allow:
  - Epic rarity
  - multiple affixes
  - high mechanical pressure

Difficulty increases via **complexity**, not HP inflation.

---

## 16.7 World Progression Gates

Progress through the world may be gated by:

- Boss defeats
- Unlock Progression Axes
- Key relics
- Narrative milestones

Gates prevent premature exposure to overwhelming complexity.

---

## 16.8 Boss Nodes

- Bosses occupy **Unique biome nodes**.
- Boss nodes:
  - end branches
  - guard transitions
  - unlock new regions
- Boss arenas may:
  - override biome affixes
  - apply unique rules
  - restrict retreat

Bosses represent **checkpoints**, not dead ends.

---

## 16.9 World Events & Anomalies

- Some nodes may contain:
  - world events
  - anomalies
  - special encounters
- Events may:
  - temporarily alter rules
  - inject rare loot opportunities
  - create narrative hooks
- Events are optional but tempting.

---

## 16.10 Idle & AutoRPG Considerations

- World traversal may continue automatically.
- Player choices set **intent**, not micro-actions.
- Map state is readable at a glance.
- Long runs remain meaningful even without manual input.

---

## 16.11 Anti-Frustration Rules

- No unavoidable dead ends.
- Retreat options exist before high-risk nodes.
- Failure never locks the world permanently.
- Exploration always yields some progress.

---

## 16.12 World Design Principle

The world map exists to:
- frame player choice
- pace complexity
- reinforce biome identity
- support long-term replayability

The map should feel **inviting, dangerous, and understandable**.

## 17. Factions & World State

Factions represent organized forces within the world.
World State tracks how player actions permanently alter the world over time.

Together, they ensure the world feels **reactive, persistent, and alive**.

---

## 17.1 Factions

A faction is a group with:
- shared identity and goals
- preferred biomes
- characteristic enemies and behaviors
- influence over parts of the world

Factions are **systemic**, not purely narrative.

---

### 17.1.1 Faction Characteristics

Each faction may define:

- Preferred enemy races
- Preferred archetypes
- Signature prefixes or status effects
- Biome presence or control
- Unique bosses or leaders

Factions do not override core systems.

---

### 17.1.2 Example Faction Types

| Faction Type | Description |
|-------------|-------------|
| Beast Packs | Organized animal predators |
| Insect Colonies | Hierarchical swarm societies |
| Druidic Circles | Nature-aligned humanoids |
| Cult Orders | Ideological humanoid groups |
| Ancient Entities | Long-lived, territory-bound forces |
| Corrupted Growth | Spreading hostile ecosystems |

---

## 17.2 Faction Presence & Influence

- Factions exert influence over biome nodes.
- Influence affects:
  - encounter composition
  - enemy rarity distribution
  - active biome affixes
- Multiple factions may contest the same biome.

Faction influence is **graded**, not binary.

---

## 17.3 World State

World State tracks persistent changes caused by player actions.

World State exists across runs but may evolve gradually.

---

### 17.3.1 World State Variables

World State may include:

- Which factions are dominant
- Which bosses are defeated
- Which biomes are stabilized or corrupted
- Which world events are active or resolved

World State does not store moment-to-moment combat data.

---

## 17.4 Faction Progression & Regression

- Factions may:
  - expand into new biomes
  - retreat after losses
  - change behavior after key events
- Defeating faction leaders weakens faction presence.
- Ignoring factions may allow them to grow stronger.

Factions react, but do not require constant micromanagement.

---

## 17.5 Player Interaction with Factions

Players may interact with factions by:

- Defeating faction enemies
- Targeting faction leaders or bosses
- Completing faction-related events
- Using faction-aligned relics or crafting paths

Interactions are **implicit**, not dialog-driven.

---

## 17.6 Faction Conflict

- Factions may conflict with each other.
- Conflicts may result in:
  - biome changes
  - new encounter types
  - emergent events
- Player actions may tip conflicts in one direction.

Faction conflict creates **dynamic world variation**.

---

## 17.7 World Events & State Changes

- Major actions may trigger world events:
  - biome invasions
  - faction wars
  - environmental transformations
- Events may be:
  - temporary
  - semi-permanent
  - permanent milestones

Events are readable and telegraphed.

---

## 17.8 Persistence & Reset Rules

- World State persists across runs.
- Some world elements may:
  - decay over time
  - reset partially
  - escalate if ignored
- Core progression is never lost.

Persistence supports long-term goals without punishing failure.

---

## 17.9 Idle & AutoRPG Considerations

- Faction influence changes gradually.
- World State updates do not require constant player input.
- Offline progress may advance faction activity.
- Player intent determines long-term outcomes.

---

## 17.10 Anti-Frustration Rules

- No single faction may permanently block progression.
- World State changes are reversible over time.
- New players are protected from extreme world states.
- Critical paths remain accessible.

---

## 17.11 Faction & World State Design Principle

Factions and World State exist to:
- create emergent stories
- provide long-term goals
- make choices meaningful
- ensure no two worlds evolve identically

The world should feel **responsive, not reactive**.

## 18. Relic Design Rules

Relics are rare, powerful artifacts that modify **rules, interactions, or priorities** rather than raw stats.
They define long-term identity, enable unconventional builds, and introduce controlled rule-breaking.

Relics are never mandatory, but always meaningful.

---

## 18.1 Relic Identity

A relic is defined by:
- a clear thematic concept
- a narrow but impactful effect
- explicit interaction with existing systems

Relics do not replace weapons, armor, or skills.

---

## 18.2 Relic Categories

| Category | Purpose |
|--------|---------|
| Combat Relics | Modify combat rules or interactions. |
| Status Relics | Alter status effect behavior. |
| Rarity Relics | Interact with rarity mechanics. |
| Biome Relics | Modify biome or world behavior. |
| Encounter Relics | Alter encounter composition or pacing. |
| Progression Relics | Interact with progression axes. |

A relic belongs to **one primary category**.

---

## 18.3 Relic Power Model

- Relics modify **rules**, not numbers.
- Relics introduce **conditional advantages**.
- Relics create tradeoffs or commitments.
- Relics should enable playstyles that are otherwise inefficient.

Relics should never simply be “always better”.

---

## 18.4 Relic Rarity Rules

- Relics follow the global rarity system.
- Common relics introduce minor rule tweaks.
- Rare relics unlock new interactions.
- Epic relics alter core assumptions.
- Unique relics are boss-bound and handcrafted.

Relics do not roll random prefixes.

---

## 18.5 Relic Slots & Limits

- Players have a limited number of relic slots.
- Slot availability is unlocked via **Progression Axes**.
- Relics may compete for the same conceptual space.
- Some relics may occupy multiple slots.

Relic limits prevent runaway complexity.

---

## 18.6 Relic Interaction Rules

- Relics may:
  - modify status stacking rules
  - alter rarity effects
  - change encounter pacing
  - bias loot outcomes
- Relics never:
  - invalidate boss mechanics
  - remove counters entirely
  - bypass core restrictions

Relic effects are explicit and readable.

---

## 18.7 Relic Synergy & Conflict

- Some relics synergize intentionally.
- Some relics conflict and cannot be equipped together.
- Synergies reward planning; conflicts prevent dominance.
- Synergy chains are limited in depth.

Relics should encourage **deliberate loadouts**.

---

## 18.8 Relic Acquisition Rules

- Relics are acquired through:
  - bosses
  - epic biomes
  - major world events
- Relics are never purely random drops.
- Acquisition conditions are always visible.

Relics feel **earned**, not lucky.

---

## 18.9 Relic Persistence & Loss

- Relics persist across runs.
- Relics are never destroyed.
- Some relics may:
  - deactivate temporarily
  - require reactivation
  - evolve through use

Relic loss should never feel punitive.

---

## 18.10 Relic Evolution

- Some relics may evolve when conditions are met.
- Evolution may:
  - alter effects
  - introduce tradeoffs
  - unlock secondary behaviors
- Evolution paths are finite and explicit.

Relic evolution enhances identity, not power creep.

---

## 18.11 Anti-Power-Creep Rules

- Relics widen options before increasing strength.
- Relics create constraints as often as benefits.
- Relics never stack multiplicatively.
- No relic bypasses failure or challenge entirely.

---

## 18.12 Relic Design Principle

Relics exist to:
- support unconventional builds
- reward system mastery
- create long-term identity
- add replay-defining variation

A good relic changes **how you think**, not just how hard you hit.


## Final Note

This file defines **stable system interfaces**.
New content should extend via:
- new tables
- new rows
- new biomes

Not by altering core rules.
