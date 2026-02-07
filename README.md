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
