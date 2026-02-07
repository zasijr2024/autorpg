# AutoRPG – Combat & Enemy Concept

This document defines the core combat systems, materials, and early-biome enemies for AutoRPG.  
All values are relative (no hard numbers) to keep the system scalable and easy to balance.

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
| Poison      | Exotic     | Toxic damage, usually applied over time. |

---

## Wooden & Natural Weapons (Early Tier)

> Weapons define **damage, type, and reach**.  
> **Attack speed is defined by skills, not weapons.**

| Weapon Name   | Damage | Damage Type | Reach  |
|--------------|--------|-------------|--------|
| Teeth        | Low    | Piercing    | Short  |
| Claws        | Low    | Slashing    | Short  |
| Paw          | Normal | Crushing    | Short  |
| Tusks        | Normal | Piercing    | Short  |
| Mandible     | Low    | Piercing    | Short  |
| Stinger      | Very Low | Piercing  | Short  |
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

> Prefixes modify attacks and can be combined with attack skills.

| Prefix        | Effect |
|---------------|--------|
| Poisonous     | Adds poison damage over time. |
| Venomous      | Increases poison damage and duration. |
| Bleeding      | Causes physical damage over time. |
| Burning       | Adds fire damage over time. |
| Freezing      | Adds cold damage and slows the target. |
| Shocking      | Adds electricity damage with stun chance. |
| Corrosive     | Adds acid damage and reduces armor. |
| Crushing      | Increases armor penetration. |
| Precise       | Increases hit chance. |
| Savage        | Increases damage but lowers hit chance. |
| Rapid         | Reduces attack interval. |
| Heavy         | Increases damage but slows attacks. |
| Vicious       | Increases crit chance and crit damage. |
| Leeching      | Converts part of damage to health. |
| Infectious    | Damage over time can spread to nearby enemies. |

**Prefix Rules**
- Early game: max **1** prefix  
- Mid game: max **2** prefixes  
- Late game / bosses: max **3** prefixes  

---

## Armor Types (Natural & Wearable)

> Armor type defines **resistances and vulnerabilities**.  
> Speed penalty is relative and standardized.

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

## Materials – Effects on Weapons and Armor

> **Material modifies quality and behavior**, not resistances.  
> Armor resistances come from **Armor Type**, not material.

| Material  | Weapon Effect | Armor Effect |
|-----------|---------------|--------------|
| Flesh / Skin | Very low damage | No protection |
| Leather | Low damage, flexible | Light, low penalty |
| Bone | Normal damage, higher crit chance | Moderate protection |
| Wood | Normal damage | Light, fire vulnerable |
| Stone | High damage, very slow | Heavy, very slow |
| Copper | Normal damage, poor penetration | Light protection |
| Iron | High damage, reliable | Good protection |
| Steel | High damage, bonus crit damage | Strong protection |
| Silver | Normal damage, bonus vs magical beings | Magic resistance |
| Gold | Low damage, decorative | No combat value |
| Chitin | Normal damage, fast | Slashing resistant |
| Mithril | High damage, fast | Strong protection, low penalty |

---

## Forest Enemies (Early Biome)

| Enemy Name        | Type       | HP     | Size       | Weapon        | Armor  | Skill |
|-------------------|------------|--------|------------|---------------|--------|-------|
| Forest Bandit     | Humanoid   | Normal | Normal     | Wooden Sword  | Leather | Precise Strike |
| Wild Hunter       | Humanoid   | Normal | Normal     | Wooden Spear  | Hide    | Charge Attack |
| Forest Wolf       | Animal     | Normal | Medium     | Teeth         | Fur     | Bite |
| Dire Boar         | Animal     | High   | Large      | Tusks         | Hide    | Charge Attack |
| Forest Bear       | Animal     | High   | Large      | Paw           | Fur     | Heavy Slam |
| Giant Ant         | Insect     | Normal | Small      | Mandible     | Chitin | Rapid Jab |
| Poison Bee        | Insect     | Low    | Tiny       | Stinger      | Chitin | Bite |
| Forest Spider     | Insect     | Normal | Medium     | Mandible     | Chitin | Precise Strike |
| Walking Sapling   | Plant      | Normal | Medium     | Wooden Club  | Bark   | Crushing Blow |
| Ancient Treant    | Plant      | High   | Very Large | Wooden Staff | Bark   | Sweep Attack |

---

## Design Notes

- Weapons define **what hits**  
- Skills define **how it hits**  
- Prefixes define **special behavior**  
- Armor defines **what resists what**  
- Materials define **quality and progression**

This system is designed for automated combat, procedural enemies, and scalable progression.

## Status Effects

| Status Effect | Damage Type | Effect | Stacking Rule | Duration Behavior | Notes |
|---------------|------------|--------|----------------|-------------------|-------|
| Poison        | Poison     | Deals damage over time. | Stacks in power | Refreshes duration | Core DOT, common on insects and venoms. |
| Bleeding      | Physical   | Deals damage over time. | Stacks in power | Refreshes duration | Strong vs unarmored targets. |
| Burning       | Fire       | Deals damage over time. | Does not stack | Refreshes duration | Strong vs organic targets, weak vs fire resist. |
| Freezing      | Cold       | Slows attack and movement speed. | Does not stack | Refreshes duration | Can enable shatter mechanics later. |
| Shocked       | Electricity| Chance to stun or interrupt actions. | Does not stack | Short duration | Strong control effect, rare. |
| Corroded      | Acid       | Reduces armor effectiveness. | Stacks in duration | Refreshes duration | Synergizes with physical damage. |
| Weakened      | Physical   | Reduces outgoing damage. | Does not stack | Refreshes duration | Defensive debuff, good for elites. |
| Vulnerable    | Any        | Increases damage taken. | Does not stack | Short duration | Burst window enabler. |
| Stunned       | Control    | Cannot act. | Does not stack | Very short duration | Bosses usually resistant or immune. |
| Rooted        | Control    | Cannot move, can still attack. | Does not stack | Refreshes duration | Strong vs melee enemies. |

### Status Effect Rules

- Damage-over-time effects tick independently of attack speed.
- Only one instance of non-stacking effects can be active at a time.
- Bosses and elites may have partial or full resistance to control effects.
- Status effects respect damage resistances and vulnerabilities.
- Multiple different status effects can be active simultaneously.

## Enemy Archetypes

| Archetype     | Role Description | HP Profile | Speed Profile | Preferred Range | Preferred Skills | Common Prefixes |
|---------------|------------------|------------|---------------|-----------------|------------------|-----------------|
| Bruiser       | High-durability frontline fighter. | High | Slow | Short | Heavy Slam, Crushing Blow | Heavy, Armored |
| Skirmisher    | Fast melee attacker relying on speed. | Normal | Fast | Short | Bite, Rapid Jab, Claw Swipe | Rapid, Bleeding |
| Swarm         | Weak individual enemies attacking in numbers. | Low | Fast | Short | Rapid Jab, Bite | Infectious, Poisonous |
| Charger       | High-damage initiator with burst attacks. | High | Normal | Short | Charge Attack | Savage, Vicious |
| Sniper        | Long-range attacker with high accuracy. | Low | Slow | Long | Precise Strike, Stab | Precise, Vicious |
| Controller    | Focuses on debuffs and crowd control. | Normal | Normal | Medium | Sweep Attack, Crushing Blow | Freezing, Shocking |
| Tank          | Soaks damage and protects allies. | Very High | Very Slow | Short | Heavy Slam | Armored, Crushing |
| Assassin      | High burst damage, low durability. | Low | Very Fast | Short | Precise Strike, Stab | Vicious, Rapid |
| Caster (Future) | Ranged magical damage dealer. | Low | Slow | Long | Magic-based skills | Burning, Shocking |
| Boss          | Unique enemy with multiple phases. | Very High | Variable | Variable | Multiple | Multiple |

### Archetype Rules

- Archetypes define behavior, not exact stats.
- Enemies may belong to only one archetype by default.
- Elites may combine an archetype with additional prefixes.
- Bosses may switch archetypes between phases.
- Archetypes influence target selection and skill priority.

## Enemy Races / Subtypes

> Races define **biological traits and resist tendencies**.  
> Archetypes define **combat behavior**.  
> Both are combined to form a complete enemy.

| Category  | Race / Subtype | Trait Description | Typical Resistance | Typical Vulnerability |
|-----------|----------------|-------------------|--------------------|-----------------------|
| Humanoid  | Human          | Balanced and adaptable. | None | None |
| Humanoid  | Elf            | Agile and precise. | Piercing | Crushing |
| Humanoid  | Dwarf          | Sturdy and resilient. | Poison | Piercing |
| Humanoid  | Orc            | Brutal and aggressive. | Slashing | Cold |
| Humanoid  | Goblin         | Small and evasive. | None | Fire |
| Animal    | Wolf           | Fast pack predator. | Cold | Fire |
| Animal    | Bear           | Massive and durable. | Crushing | Electricity |
| Animal    | Boar           | Tough charger. | Slashing | Poison |
| Animal    | Deer           | Fast and fragile. | None | Piercing |
| Insect    | Ant            | Armored swarm creature. | Slashing | Fire |
| Insect    | Spider         | Venomous ambusher. | Poison | Fire |
| Insect    | Bee            | Fast flying stinger. | None | Cold |
| Plant     | Sapling        | Weak animated plant. | Piercing | Fire |
| Plant     | Treant         | Ancient living wood. | Piercing | Fire |
| Plant     | Fungus         | Spore-based organism. | Poison | Fire |
| Undead (Future) | Skeleton | Bone-based undead. | Poison | Crushing |
| Undead (Future) | Zombie   | Slow rotting corpse. | Poison | Fire |
| Magical (Future) | Fey     | Ethereal forest beings. | Magic | Iron |

### Race Rules

- Races define biological resistances and vulnerabilities.
- Races do not define skills or weapons directly.
- Armor type may override or enhance racial resistances.
- Archetype + Race + Weapon + Skill = complete enemy identity.
- Bosses may ignore racial weaknesses.
