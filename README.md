# AutoRPG – Combat & Enemy System Concept

This document defines the core combat, materials, enemies, and progression systems for AutoRPG.  
All values are **relative** (no fixed numbers) to keep balancing flexible and scalable.

---

## Global Design Principles

- Weapons define **what hits**
- Skills define **how it hits**
- Prefixes define **special effects**
- Armor Types define **resistances & vulnerabilities**
- Materials define **quality, weight, and tier**
- Archetypes define **behavior**
- Races define **biological traits**

Only one system may own one responsibility.

---

## Damage Types

| Damage Type  | Category   | Description |
|-------------|------------|-------------|
| Slashing    | Physical   | Cutting damage from blades or claws. |
| Piercing    | Physical   | Penetrating damage from pointed attacks. |
| Crushing    | Physical   | Blunt force and impact damage. |
| Missile     | Physical   | Ranged physical projectile damage. |
| Fire        | Elemental  | Heat and burning damage. |
| Cold        | Elemental  | Freezing and chilling damage. |
| Electricity | Elemental  | Lightning and electrical shock damage. |
| Acid        | Elemental  | Corrosive damage that degrades matter. |
| Magic       | Magical    | Pure non-elemental magical energy. |
| Poison      | Exotic     | Toxic damage applied over time. |

---

## Weapons (Early / Natural Tier)

> Weapons define **damage profile and reach only**.  
> **Attack speed comes exclusively from skills.**

| Weapon Name   | Damage | Damage Type | Reach  |
|--------------|--------|-------------|--------|
| Teeth        | Low    | Piercing    | Short  |
| Claws        | Low    | Slashing    | Short  |
| Paw          | Normal | Crushing    | Short  |
| Tusks        | Normal | Piercing    | Short  |
| Mandible     | Low    | Piercing    | Short  |
| Stinger      | Very Low | Piercing | Short  |
| Wooden Club  | Normal | Crushing    | Short  |
| Wooden Sword | Normal | Slashing    | Medium |
| Wooden Spear | High   | Piercing    | Long   |
| Wooden Staff | Low    | Crushing    | Long   |
| Sling Stone  | Low    | Missile     | Long   |
| Wooden Arrow | Low    | Piercing    | Long   |
| Thrown Rock  | Low    | Crushing    | Medium |

---

## Attack Skills

> Skills define **tempo, accuracy, and crit behavior**.

| Skill Name        | Damage Modif. | Hit Chance Modif. | Speed Modif. | Crit Chance Modif. |
|-------------------|---------------|-------------------|--------------|--------------------|
| Bite              | Normal        | Low               | Fast         | Normal             |
| Claw Swipe        | Low           | High              | Very Fast    | Low                |
| Heavy Slam        | High          | Low               | Very Slow    | High               |
| Pierce Thrust     | Normal        | Normal            | Normal       | Normal             |
| Rapid Jab         | Low           | High              | Very Fast    | Low                |
| Crushing Blow     | High          | Normal            | Slow         | High               |
| Charge Attack     | High          | Low               | Slow         | High               |
| Stab              | Normal        | High              | Fast         | Normal             |
| Sweep Attack      | Low           | Normal            | Slow         | Low                |
| Precise Strike    | Low           | Very High         | Slow         | High               |

---

## Support Attack Skills (Prefixes)

> Prefixes modify attacks and may be combined with skills.

| Prefix        | Effect |
|---------------|--------|
| Poisonous     | Adds poison damage over time. |
| Venomous      | Increases poison damage and duration. |
| Bleeding      | Causes physical damage over time. |
| Burning       | Adds fire damage over time. |
| Freezing      | Slows attack and movement speed. |
| Shocking      | Chance to stun or interrupt actions. |
| Corrosive     | Reduces armor effectiveness. |
| Crushing      | Increases armor penetration. |
| Precise       | Increases hit chance. |
| Savage        | Increases damage but lowers hit chance. |
| Rapid         | Reduces attack interval. |
| Heavy         | Increases damage but slows attacks. |
| Vicious       | Increases crit chance and crit damage. |
| Leeching      | Converts part of damage to health. |
| Infectious    | Damage over time can spread to nearby enemies. |

### Prefix Rules
- Early game: **1** prefix
- Mid game: **2** prefixes
- Late game / bosses: **3** prefixes
- Only **one speed-affecting prefix** (Rapid or Heavy) may apply.

---

## Status Effects

| Status Effect | Damage Type | Effect | Stacking Rule | Duration Behavior |
|---------------|------------|--------|----------------|-------------------|
| Poison        | Poison     | Damage over time. | Stacks in power | Refreshes |
| Bleeding      | Physical   | Damage over time. | Stacks in power | Refreshes |
| Burning       | Fire       | Damage over time. | No stacking | Refreshes |
| Freezing      | Cold       | Slows actions. | No stacking | Refreshes |
| Shocked       | Electricity | Interrupt / stun chance. | No stacking | Short |
| Corroded      | Acid       | Reduces armor. | Stacks in duration | Refreshes |
| Weakened      | Physical   | Reduces outgoing damage. | No stacking | Refreshes |
| Vulnerable    | Any        | Increases damage taken. | No stacking | Short |
| Stunned       | Control    | Cannot act. | No stacking | Very Short |
| Rooted        | Control    | Cannot move. | No stacking | Refreshes |

---

## Armor Types (Natural & Wearable)

> Armor Types define **resistances, vulnerabilities, and speed penalties**.

| Armor Type | Speed Modif. | Resistance | Vulnerability |
|------------|--------------|------------|---------------|
| Skin       | Normal       | None       | None          |
| Fur        | Normal       | Cold       | Fire          |
| Leather    | Normal       | Piercing   | Cold          |
| Hide       | Slow         | Slashing   | Fire          |
| Bone       | Slow         | Crushing   | Acid          |
| Chitin     | Slow         | Slashing   | Fire          |
| Scales     | Slow         | Fire       | Electricity  |
| Bark       | Very Slow    | Piercing   | Fire          |
| Shell      | Very Slow    | Missile    | Crushing     |
| Feathers  | Fast         | None       | Fire          |

---

## Materials (Quality & Tier)

> Materials modify **quality, weight, and tier**.  
> They **do not** define resistances or vulnerabilities.

| Material  | Weapon Effect | Armor Effect |
|-----------|---------------|--------------|
| Flesh / Skin | Very low damage | No protection |
| Leather | Low damage, flexible | Light, minimal penalty |
| Bone | Normal damage, higher crit chance | Moderate protection |
| Wood | Normal damage | Light, fire-susceptible |
| Stone | High damage, very slow | Heavy, very slow |
| Copper | Normal damage, poor penetration | Light protection |
| Iron | High damage, reliable | Good protection |
| Steel | High damage, bonus crit damage | Strong protection |
| Silver | Normal damage, bonus vs magical beings | Magic resistance |
| Gold | Low damage, decorative | No combat value |
| Chitin | Normal damage, fast | Light and resilient |
| Mithril | High damage, fast | Strong protection, low penalty |

---

## Enemy Archetypes

> Archetypes define **combat behavior**, not biology.

| Archetype   | Role | HP | Speed | Preferred Range |
|-------------|------|----|-------|-----------------|
| Bruiser     | Durable frontline fighter | High | Slow | Short |
| Skirmisher  | Fast melee attacker | Normal | Fast | Short |
| Swarm       | Numerous weak enemies | Low | Fast | Short |
| Charger     | Burst initiator | High | Normal | Short |
| Sniper      | Accurate ranged attacker | Low | Slow | Long |
| Controller  | Debuff & control | Normal | Normal | Medium |
| Tank        | Damage sponge | Very High | Very Slow | Short |
| Assassin    | High burst, fragile | Low | Very Fast | Short |
| Boss        | Multi-phase threat | Very High | Variable | Variable |

---

## Enemy Races / Subtypes

> Races define **biological traits**.

| Category | Race | Typical Resistance | Typical Vulnerability |
|--------|------|--------------------|-----------------------|
| Humanoid | Human | None | None |
| Humanoid | Elf | Piercing | Crushing |
| Humanoid | Dwarf | Poison | Piercing |
| Animal | Wolf | Cold | Fire |
| Animal | Bear | Crushing | Electricity |
| Insect | Ant | Slashing | Fire |
| Insect | Spider | Poison | Fire |
| Insect | Bee | None | Cold |
| Plant | Sapling | Piercing | Fire |
| Plant | Treant | Piercing | Fire |

---

## Forest Enemies (Early Biome)

| Enemy Name | Type | HP | Size | Weapon | Armor | Skill |
|-----------|------|----|------|--------|-------|-------|
| Forest Bandit | Humanoid | Normal | Normal | Wooden Sword | Leather | Precise Strike |
| Wild Hunter | Humanoid | Normal | Normal | Wooden Spear | Hide | Charge Attack |
| Forest Wolf | Animal | Normal | Medium | Teeth | Fur | Bite |
| Dire Boar | Animal | High | Large | Tusks | Hide | Charge Attack |
| Forest Bear | Animal | High | Large | Paw | Fur | Heavy Slam |
| Giant Ant | Insect | Normal | Small | Mandible | Chitin | Rapid Jab |
| Poison Bee | Insect | Low | Tiny | Stinger | Chitin | Bite |
| Forest Spider | Insect | Normal | Medium | Mandible | Chitin | Precise Strike |
| Walking Sapling | Plant | Normal | Medium | Wooden Club | Bark | Crushing Blow |
| Ancient Treant | Plant | High | Very Large | Wooden Staff | Bark | Sweep Attack |

---

## Combat Resolution Rules (High-Level)

- Attack speed is determined **only by skills and prefixes**
- Armor speed penalties apply after skill speed
- Damage type → armor → race modifiers are applied in that order
- DOT effects tick independently of attack speed
- Bosses may partially or fully resist control effects

---

## Summary

This system is designed for:
- Automated combat
- Procedural enemies
- Scalable difficulty
- Clear counterplay
- Minimal rework during balancing

## Biomes

| Biome        | Preferred Enemy Types              | Preferred Environmental Loot |
|--------------|------------------------------------|-------------------------------|
| Forest       | Animals, Insects, Plants, Humanoids | Wood, Leather, Herbs, Bone |
| Deep Forest  | Plants, Insects, Beasts              | Wood, Chitin, Poisonous Herbs |
| Plains       | Animals, Humanoids                  | Leather, Hide, Food, Bone |
| Hills        | Humanoids, Beasts                   | Stone, Bone, Copper |
| Mountains    | Humanoids, Beasts                   | Stone, Iron, Hide |
| Caves        | Insects, Beasts                     | Stone, Bone, Chitin |
| Swamp        | Insects, Plants                     | Poisonous Herbs, Leather, Acidic Sludge |
| Desert       | Beasts, Insects                     | Bone, Leather, Sandstone |
| Tundra       | Beasts, Humanoids                   | Fur, Hide, Ice Crystals |
| Jungle       | Insects, Plants, Beasts             | Wood, Chitin, Poisonous Herbs |
| Ruins        | Humanoids, Constructs (future)      | Stone, Metal Scraps, Relics |
| Graveyard    | Undead (future), Humanoids          | Bone, Cloth, Dark Relics |
| Volcanic     | Beasts, Elementals (future)         | Obsidian, Fire Crystals, Metal |
| Magical Grove| Fey (future), Plants               | Magical Herbs, Mithril Traces |

### Biome Rules

- Biomes bias enemy races, not archetypes.
- Environmental loot drops independently of enemy loot.
- Rare materials have higher drop chance in specific biomes.
- Elite and boss enemies may override biome rules.

## Biome Affixes

> Biome Affixes apply global modifiers to all encounters within a biome.

| Biome        | Affix Name        | Effect |
|--------------|-------------------|--------|
| Forest       | Dense Growth      | Reduced visibility; increased ambush chance. |
| Forest       | Overgrown         | Plant enemies appear more frequently. |
| Deep Forest  | Toxic Spores      | Chance to apply Poison on hit. |
| Deep Forest  | Entangling Roots  | Movement speed reduced; Rooted may occur. |
| Plains       | Open Terrain      | Increased ranged attack effectiveness. |
| Plains       | Roaming Packs     | Animal enemies appear in larger groups. |
| Hills        | Uneven Ground     | Reduced movement speed; Charge less effective. |
| Mountains    | Thin Air          | Reduced attack speed; stamina drains faster. |
| Mountains    | Falling Rocks     | Periodic area damage events. |
| Caves        | Darkness          | Reduced hit chance; ambush damage increased. |
| Caves        | Narrow Passages   | Cleave and sweep attacks are limited. |
| Swamp        | Boggy Ground      | Movement speed reduced; Poison duration increased. |
| Swamp        | Corrosive Mists   | Acid effects are more common. |
| Desert       | Scorching Heat    | Fire damage increased; stamina recovery reduced. |
| Desert       | Sandstorms        | Reduced hit chance; missile attacks less effective. |
| Tundra       | Bitter Cold       | Cold damage increased; movement slowed. |
| Tundra       | Frozen Ground     | Chance to apply Freezing on movement. |
| Jungle       | Predatory Growth  | Insect and plant enemies gain attack speed. |
| Ruins        | Crumbling Walls  | Environmental traps more common. |
| Graveyard    | Unholy Presence  | Undead resist control effects. |
| Volcanic     | Lava Fissures    | Periodic fire damage zones. |
| Magical Grove| Arcane Saturation | Magic effects are amplified. |

### Biome Affix Rules

- Each biome has **1–2 active affixes** at a time.
- Affixes affect both enemies and players.
- Affixes may modify environment, enemies, or combat rules.
- Elite and boss enemies may gain additional biome-related bonuses.
- Biome affixes never invalidate core mechanics; they bias them.

New Weapons
| Weapon Name        | Damage | Damage Type | Reach |
|--------------------|--------|-------------|-------|
| Ant Lance          | Normal | Piercing    | Medium |
| Queen Mandible     | High   | Piercing    | Short |
| Thorn Whip         | Low    | Slashing    | Medium |
| Root Slam          | Normal | Crushing    | Short |
| Branch Halberd     | High   | Slashing    | Long |
| Venom Spit         | Low    | Poison      | Long |

New Armor Types
| Armor Type     | Speed Modif. | Resistance | Vulnerability |
|----------------|--------------|------------|---------------|
| Hardened Chitin| Slow         | Piercing   | Fire |
| Living Bark    | Very Slow    | Slashing   | Fire |
| Mosshide       | Normal       | Cold       | Fire |

New Attack Skills
| Skill Name        | Damage Modif. | Hit Chance Modif. | Speed Modif. | Crit Chance Modif. |
|-------------------|---------------|-------------------|--------------|--------------------|
| Impale           | High          | Normal            | Slow         | High |
| Frenzied Bite    | Normal        | Normal            | Fast         | Normal |
| Venom Spray      | Low           | High              | Slow         | Low |
| Root Grasp       | Low           | High              | Slow         | None |
| Overhead Cleave  | High          | Low               | Very Slow    | High |

New Support Prefixes
| Prefix        | Effect |
|---------------|--------|
| Frenzied      | Increases speed as HP decreases. |
| Broodbound    | Gains bonuses when allies are nearby. |
| Regenerating  | Slowly restores health over time. |

🐜 Insect Hierarchy (Ant Colony)
Enemy Name	Archetype	HP	Size	Weapon	Armor	Skill
Ant Worker	Swarm	Low	Tiny	Mandible	Chitin	Rapid Jab
Ant Soldier	Bruiser	Normal	Small	Ant Lance	Hardened Chitin	Impale
Ant Guard	Tank	High	Small	Mandible	Hardened Chitin	Heavy Slam
Ant Spitter	Controller	Low	Small	Venom Spit	Chitin	Venom Spray
Ant Queen	Boss	Very High	Large	Queen Mandible	Hardened Chitin	Brood Command

(Brood Command = Sweep + Broodbound aura)

🐺 Giant & Reimagined Predators
Enemy Name	Archetype	HP	Size	Weapon	Armor	Skill
Dire Squirrel	Assassin	Normal	Medium	Teeth	Fur	Frenzied Bite
Giant Hedgehog	Tank	High	Medium	Spines	Hide	Rolling Slam
Forest Lynx	Assassin	Normal	Medium	Claws	Fur	Precise Strike
Dire Owl	Sniper	Low	Medium	Talons	Feathers	Precise Strike
Moss Bear	Bruiser	Very High	Large	Paw	Mosshide	Heavy Slam
🌿 Plant & Wood Entities
Enemy Name	Archetype	HP	Size	Weapon	Armor	Skill
Twigling	Swarm	Low	Small	Branch	Bark	Rapid Jab
Thorn Creeper	Controller	Normal	Medium	Thorn Whip	Living Bark	Root Grasp
Bark Guardian	Tank	High	Large	Branch Halberd	Living Bark	Overhead Cleave
Vine Horror	Bruiser	High	Large	Root Slam	Living Bark	Crushing Blow
Ancient Oakheart	Boss	Very High	Huge	Root Slam	Living Bark	Sweep Attack
🧍 Humanoids & Forest Folk
Enemy Name	Archetype	HP	Size	Weapon	Armor	Skill
Forest Poacher	Skirmisher	Normal	Normal	Wooden Spear	Leather	Stab
Woodcut Raider	Bruiser	High	Normal	Wooden Axe	Hide	Heavy Slam
Moss Druid	Controller	Normal	Normal	Wooden Staff	Mosshide	Root Grasp
Bark Knight	Tank	High	Normal	Branch Halberd	Living Bark	Crushing Blow
Greenwarden	Boss	Very High	Large	Thorn Whip	Living Bark	Sweep Attack
🕷️ Other Forest Horrors
Enemy Name	Archetype	HP	Size	Weapon	Armor	Skill
Giant Spiderling	Swarm	Low	Small	Mandible	Chitin	Bite
Widow Spider	Assassin	Normal	Medium	Mandible	Chitin	Precise Strike
Broodmother Spider	Boss	Very High	Large	Mandible	Hardened Chitin	Infectious Bite
Forest Slime	Bruiser	High	Medium	Acid Body	Skin	Corrosive Slam
Spore Hulk	Tank	Very High	Large	Root Slam	Mosshide	Heavy Slam