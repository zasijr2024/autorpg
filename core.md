# AutoRPG – Core Combat Systems

This document defines all global, biome-agnostic systems for AutoRPG.
All values are relative; no fixed numbers are used.

---

## Design Responsibilities

- Weapons define WHAT hits
- Skills define HOW it hits
- Prefixes define SPECIAL EFFECTS
- Armor Types define RESISTANCES & VULNERABILITIES
- Materials define QUALITY & TIER
- Archetypes define BEHAVIOR
- Races define BIOLOGY

No responsibility overlaps.

---

## Damage Types

| Damage Type | Category | Description |
|------------|----------|-------------|
| Slashing | Physical | Cutting damage from blades or claws |
| Piercing | Physical | Penetrating pointed damage |
| Crushing | Physical | Blunt force and impact |
| Missile | Physical | Ranged physical projectiles |
| Fire | Elemental | Heat and burning |
| Cold | Elemental | Freezing and chilling |
| Electricity | Elemental | Lightning and shock |
| Acid | Elemental | Corrosive damage |
| Magic | Magical | Pure non-elemental energy |
| Poison | Exotic | Toxic damage over time |
| Disease | Exotic | Persistent weakening damage |

---

## Weapons

> Weapons define damage profile and reach only.

| Weapon Name | Label | Damage | Damage Type | Reach |
|------------|-------|--------|-------------|-------|
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

## Attack Skills

| Skill | Damage | Hit Chance | Speed | Crit |
|------|--------|------------|-------|------|
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

## Support Prefixes

| Prefix | Effect |
|-------|--------|
| Poisonous | Applies Poison |
| Diseased | Applies Disease |
| Bleeding | Physical DOT |
| Burning | Fire DOT |
| Freezing | Slow effects |
| Shocking | Interrupt / stun chance |
| Corrosive | Reduces armor |
| Crushing | Armor penetration |
| Precise | Hit chance bonus |
| Savage | Damage ↑, accuracy ↓ |
| Rapid | Attack interval ↓ |
| Heavy | Damage ↑, speed ↓ |
| Vicious | Crit chance & damage ↑ |
| Leeching | Life steal |
| Infectious | DOT spreads |
| Frenzied | Speed increases at low HP |
| Broodbound | Bonuses near allies |
| Regenerating | HP regen |

---

## Status Effects

| Status | Type | Effect | Stacking |
|------|------|--------|----------|
| Poison | Exotic | DOT | Power |
| Disease | Exotic | DOT + debuff | Duration |
| Bleeding | Physical | DOT | Power |
| Burning | Fire | DOT | None |
| Freezing | Cold | Slow | None |
| Shocked | Elec | Interrupt | None |
| Corroded | Acid | Armor reduction | Duration |
| Weakened | Physical | Damage ↓ | None |
| Vulnerable | Any | Damage taken ↑ | None |
| Stunned | Control | No actions | None |
| Rooted | Control | No movement | None |

---

## Armor Types

| Armor | Label | Speed | Resist | Vulnerable |
|------|-------|-------|--------|------------|
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

## Materials

| Material | Weapon Effect | Armor Effect |
|---------|---------------|--------------|
| Flesh | Very low quality | No protection |
| Leather | Flexible | Light |
| Bone | Crit bias | Moderate |
| Wood | Standard | Light |
| Stone | Heavy, slow | Heavy |
| Copper | Poor penetration | Light |
| Iron | Reliable | Strong |
| Steel | Crit bonus | Strong |
| Silver | Bonus vs magical | Magic resist |
| Gold | Decorative | None |
| Chitin | Fast | Resilient |
| Mithril | High-tier | Low penalty |

---

## Archetypes

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

## Races / Subtypes

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

## Encounter Composition Rules

Encounter composition defines how enemies are grouped and spawned in combat.
It determines difficulty, pacing, and tactical variety without modifying core stats.

---

### Encounter Size

| Encounter Type | Description |
|---------------|-------------|
| Solo          | Single enemy, often elite or boss. |
| Small Pack    | 2–3 enemies, minimal synergy. |
| Standard Pack | 4–6 enemies, mixed archetypes. |
| Swarm         | Large number of weak enemies. |
| Elite Group   | Few enemies with enhanced traits. |
| Boss Encounter| One boss, often with supporting enemies. |

---

### Archetype Distribution Rules

- Each encounter has **one primary archetype**.
- Secondary archetypes may appear depending on encounter size.
- Swarm archetypes increase enemy count but reduce individual threat.
- Tank archetypes rarely appear alone unless elite or boss-tier.
- Boss encounters may contain **supporting minions**.

---

### Archetype Mixing Guidelines

| Primary Archetype | Allowed Secondary Archetypes |
|-------------------|------------------------------|
| Bruiser           | Skirmisher, Controller |
| Skirmisher        | Swarm, Sniper |
| Swarm             | Swarm, Controller |
| Charger           | Skirmisher |
| Sniper            | Tank, Controller |
| Controller        | Bruiser, Swarm |
| Tank              | Controller, Bruiser |
| Assassin          | Skirmisher |
| Boss              | Any (thematically consistent) |

---

### Biome Influence

- Biomes bias **race selection**, not archetypes.
- Biome affixes may modify encounter composition.
- Environmental encounters may replace enemies with hazards.
- Certain archetypes may be rare or absent in specific biomes.

---

### Hierarchy & Faction Rules

- Hierarchical enemies spawn in **role-appropriate ratios**.
  - Example: Ant Worker > Ant Soldier > Ant Guard > Ant Queen
- Queens, Broodmothers, and Leaders spawn with followers.
- Killing leaders may weaken or disperse remaining enemies.
- Faction enemies prefer spawning together.

---

### Elite & Boss Composition

- Elite enemies replace a standard enemy in a pack.
- Elite groups reduce enemy count but increase threat.
- Boss encounters may:
  - Spawn waves
  - Change composition mid-fight
  - Summon archetype-specific minions
- Bosses should never rely solely on raw HP.

---

### Difficulty Scaling Axes

Encounter difficulty scales by:
- Enemy count
- Archetype complexity
- Prefix count
- Status effect frequency
- Biome affixes

Avoid scaling primarily through HP inflation.

---

### Anti-Frustration Rules (Important for AutoRPG)

- Avoid stacking multiple control-heavy archetypes in early game.
- Do not combine more than one high-tempo modifier per encounter.
- Long-duration control effects are limited on bosses.
- Swarm encounters should resolve quickly.

---

### Encounter Identity Principle

Each encounter should teach or reinforce **one concept**, such as:
- Armor interaction
- Status effects
- Speed vs durability
- Crowd control
- Burst windows

Encounters should not test everything at once.

## Boss Phase Rules

Bosses are multi-phase encounters designed to change behavior, not just durability.
Phases introduce new mechanics, reinforce encounter identity, and create pacing.

---

### Phase Triggers

| Trigger Type | Description |
|-------------|-------------|
| Health Threshold | Phase changes at specific HP percentages. |
| Time-Based | Phase changes after a fixed duration. |
| Event-Based | Phase changes when a condition is met (adds killed, shield broken). |
| Resource-Based | Phase changes when boss energy or stacks reach a limit. |

Bosses may use **multiple trigger types** across phases.

---

### Phase Structure

| Phase Type | Purpose |
|-----------|---------|
| Introduction | Establishes boss identity and core mechanics. |
| Escalation | Increases pressure via speed, damage, or mechanics. |
| Control Phase | Focus on debuffs, terrain, or crowd control. |
| Summoning Phase | Introduces adds or environmental threats. |
| Burn Phase | Short, high-intensity window encouraging burst damage. |
| Desperation | Final phase with high risk and limited duration. |

Not all bosses require all phase types.

---

### Phase Changes (What Can Change)

During a phase transition, a boss may change:

- Archetype (e.g. Tank → Bruiser)
- Preferred skills
- Support prefixes
- Status resistances
- Movement behavior
- Encounter composition (adds, hazards)

Phase changes should **always be visible or telegraphed**.

---

### Phase Modifiers

| Modifier Type | Effect |
|--------------|--------|
| Empowered | Increased damage or speed. |
| Shielded | Temporary damage reduction or immunity. |
| Enraged | Attack speed increases over time. |
| Unstable | Periodic area effects or self-damage. |
| Commanding | Buffs allied enemies. |
| Corrupted | Applies exotic status effects more frequently. |

Phase modifiers replace or override previous ones — they do not stack infinitely.

---

### Add & Summon Rules

- Summoned enemies follow standard encounter rules.
- Add waves should reinforce boss mechanics (not distract).
- Killing adds may:
  - Weaken the boss
  - Delay the next phase
  - Remove a buff or shield
- Add density must decrease as fight duration increases.

---

### Status Effect Rules for Bosses

- Bosses are **never fully immune** to all status effects.
- Control effects (Stun, Root) have reduced duration.
- DOT effects are effective but capped.
- Exotic effects (Disease, Corruption) may be resisted per phase.

Each boss should have **one clear status weakness**.

---

### Phase Transition Rules

- Phase transitions grant brief immunity to control effects.
- Ongoing DOTs persist unless explicitly cleansed.
- Cooldowns are not reset unless specified.
- Phase changes may reposition the boss.

Transitions should feel impactful but fair.

---

### Difficulty & Scaling Rules

Boss difficulty scales via:
- Number of phases
- Phase complexity
- Prefix count per phase
- Add behavior
- Environmental hazards

Avoid scaling bosses primarily via HP.

---

### Boss Identity Principle

Each boss should test **one primary concept**, such as:
- Sustained damage vs regeneration
- Crowd control management
- Burst timing
- Add prioritization
- Environmental awareness

Bosses should not test all systems at once.

---

### Failure & Recovery Rules (AutoRPG-Friendly)

- Boss encounters allow partial progress.
- Phase checkpoints may be saved.
- Wipes should teach, not punish excessively.
- Repeated failures may reduce boss aggression slightly.

## Rarities

Rarity defines **impact, complexity, and reward**, not raw power.
Rarities apply to **enemies, weapons, armor, and biomes**.
Skills do not have rarities.

---

### Rarity Levels

| Rarity | Availability | Description |
|-------|--------------|-------------|
| Common | Frequent | Baseline entities with minimal modifiers. |
| Uncommon | Occasional | Slightly enhanced entities with one modifier. |
| Rare | Infrequent | Strong identity, multiple modifiers, higher rewards. |
| Epic | Very Rare | Significant behavioral or environmental changes. |
| Unique | Boss Only | Handcrafted, multi-phase, narrative-defining. |

---

## Enemy Rarity Effects

| Rarity | Enemy Effects |
|-------|---------------|
| Common | Base archetype and race only. |
| Uncommon | Gains **one support prefix** or enhanced behavior. |
| Rare | Gains **two support prefixes** or altered archetype behavior. |
| Epic | Gains **multiple prefixes**, may alter encounter rules. |
| Unique | Multi-phase boss with unique mechanics. |

### Enemy Rarity Rules
- Rarity does not change base enemy type.
- Higher rarity increases **mechanical complexity**, not just stats.
- Epic enemies may override biome affixes.
- Unique enemies ignore rarity caps and prefix limits.

---

## Weapon Rarity Effects

| Rarity | Weapon Effects |
|-------|----------------|
| Common | Base weapon behavior only. |
| Uncommon | Minor quality improvement or single prefix interaction. |
| Rare | Gains **one compatible support prefix**. |
| Epic | Gains **two compatible prefixes** or a unique interaction. |
| Unique | Boss-only weapons with unique effects. |

### Weapon Rarity Rules
- Rarity never changes weapon damage type or reach.
- Prefix compatibility is enforced (e.g. no Rapid on Heavy-only weapons).
- Unique weapons are not dropped randomly.

---

## Armor Rarity Effects

| Rarity | Armor Effects |
|-------|---------------|
| Common | Base armor behavior. |
| Uncommon | Slight reduction of speed penalty or vulnerability. |
| Rare | Gains conditional resistance or passive effect. |
| Epic | Gains strong passive or interaction with status effects. |
| Unique | Boss-only armor with unique mechanics. |

### Armor Rarity Rules
- Armor type still defines resistances and vulnerabilities.
- Rarity enhances **how armor behaves**, not what it resists.
- Epic armor may alter status duration or mitigation.

---

## Biome Rarity Effects

| Rarity | Biome Effects |
|-------|----------------|
| Common | Standard biome rules and affixes. |
| Uncommon | One additional biome affix active. |
| Rare | Stronger affixes or altered encounter composition. |
| Epic | Biome-wide rule changes (environmental hazards, altered pacing). |
| Unique | Boss arena with bespoke mechanics. |

### Biome Rarity Rules
- Biome rarity affects **encounter composition**, not enemy stats.
- Epic biomes may restrict or amplify certain archetypes.
- Unique biomes exist only for major bosses or story events.

---

## Rarity Interaction Rules

- Rarity effects are **additive**, not multiplicative.
- Rarity never invalidates core mechanics.
- Higher rarity increases **decision pressure**, not randomness.
- Rarity complexity should be readable at a glance.
- Only one **Epic** entity should appear per encounter.

---

## Design Intent

- Rarity = **depth**, not inflation
- Complexity grows before power
- Bosses feel special without breaking systems
- Loot, enemies, and environments share the same language

## Loot & Reward Rules

Loot and rewards define progression, build variety, and long-term motivation.
All rewards are governed by **rarity**, **biome**, and **enemy identity**.

---

### Loot Categories

| Category | Description |
|---------|-------------|
| Materials | Used for crafting, upgrading, and progression. |
| Weapons | Equipable items defining damage profile and reach. |
| Armor | Equipable items defining resistances and speed penalties. |
| Consumables | Temporary effects or recovery items. |
| Relics | Rare items with passive or rule-altering effects. |
| Currency | Generic progression resource. |

---

### Loot Sources

| Source | Primary Rewards |
|------|-----------------|
| Common Enemies | Materials, currency |
| Uncommon Enemies | Materials, low-tier equipment |
| Rare Enemies | Equipment, consumables |
| Epic Enemies | High-quality equipment, relics |
| Bosses (Unique) | Unique items, relics, progression unlocks |
| Environment | Materials, biome-specific items |
| Events | Consumables, rare materials |

---

### Rarity-Based Loot Rules

| Rarity | Loot Behavior |
|-------|---------------|
| Common | Basic materials, low-value currency |
| Uncommon | Improved materials, chance for equipment |
| Rare | Guaranteed equipment or relic chance |
| Epic | Multiple rewards, high synergy potential |
| Unique | Handcrafted loot, no random rolls |

---

### Enemy Loot Rules

- Enemy rarity defines **loot complexity**, not quantity.
- Enemies drop loot consistent with:
  - their race
  - their armor material
  - their biome
- Swarm enemies drop reduced loot individually.
- Leaders and hierarchy units (e.g. Ant Queen) have enhanced drops.
- Boss loot is deterministic and narrative-aligned.

---

### Weapon & Armor Loot Rules

- Dropped equipment inherits:
  - the enemy’s material
  - the enemy’s rarity
- Equipment rarity determines:
  - number of compatible prefixes
  - presence of passive effects
- Skills are **never dropped** as loot.

---

### Material Drop Rules

- Materials drop based on:
  - biome identity
  - enemy armor type
  - enemy race
- Rare materials are biome-restricted.
- Environmental harvesting favors materials over equipment.
- Higher rarity enemies may drop refined materials.

---

### Biome Reward Rules

- Each biome has preferred loot categories.
- Biome rarity influences:
  - material quality
  - chance for relics
  - environmental hazards yielding loot
- Epic biomes may introduce biome-exclusive rewards.
- Unique biomes guarantee unique rewards.

---

### Boss & Unique Rewards

- Unique bosses drop:
  - unique weapons or armor
  - permanent progression unlocks
  - world-state changes
- Unique items:
  - do not roll random prefixes
  - may alter core rules
  - are not repeatable drops
- Defeating a boss may unlock new biomes or rarities.

---

### Anti-Frustration Rules

- Duplicate loot is converted to materials or currency.
- Bad luck protection increases rarity chance over time.
- Bosses always provide meaningful progress.
- Loot clarity is prioritized over surprise.

---

### Reward Philosophy

- Rewards reinforce **player decisions**
- Power growth is gradual and readable
- Rarity adds depth, not randomness
- Progression should feel inevitable, not lucky
