# AutoRPG – Core Systems Specification

This document defines all **biome-agnostic core systems** for AutoRPG.
All values are **relative**; no fixed numbers are used.

---

## Table of Contents

1. Design Principles & Global Rules  
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
| Burning | Fire DOT |
| Freezing | Slow |
| Shocking | Interrupt |
| Corrosive | Armor reduction |
| Crushing | Armor penetration |
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
| Magical | Fey | Magic | Iron |

---

## 7. Encounter & Boss Design

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

(see Loot & Reward Rules section you already approved)## 8. Loot & Rewards

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

## Final Note

This file defines **stable system interfaces**.
New content should extend via:
- new tables
- new rows
- new biomes

Not by altering core rules.
