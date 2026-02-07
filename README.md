# autorpg
## Damage Types (inspired by Baldurs Gate 2)

| Damage Type  | Category   | Description |
|-------------|------------|-------------|
| Slashing    | Physical   | Cutting damage from bladed weapons or claws. |
| Piercing    | Physical   | Penetrating damage from pointed or sharp attacks. |
| Crushing    | Physical   | Blunt force and impact damage. |
| Missile     | Physical   | Ranged physical projectile damage. |
| Fire        | Elemental  | Heat and burning damage. |
| Cold        | Elemental  | Freezing and chilling damage. |
| Electricity | Elemental  | Lightning and electrical shock damage. |
| Acid        | Elemental  | Corrosive damage that degrades matter. |
| Magic       | Magical    | Pure non-elemental magical energy. |
| Poison      | Exotic     | Toxic damage, often applied over time. |

## Wooden & Natural Weapons (Early / Monster Tier)

| Weapon Name   | Damage | Damage Type | Speed Modifier | Reach  |
|--------------|--------|-------------|----------------|--------|
| Teeth        | 1–2    | Piercing    | Fast           | Short  |
| Claws        | 1–3    | Slashing    | Fast           | Short  |
| Pawn         | 2–4    | Crushing    | Slow           | Short  |
| Tusks        | 2–4    | Piercing    | Normal         | Short  |
| Mandible     | 1–3    | Piercing    | Fast           | Short  |
| Stinger      | 1–2    | Piercing    | Fast           | Short  |
| Wooden Club  | 2–4    | Crushing    | Slow           | Short  |
| Wooden Sword | 2–4    | Slashing    | Normal         | Medium |
| Wooden Spear | 2–5    | Piercing    | Normal         | Long   |
| Wooden Staff | 1–3    | Crushing    | Normal         | Long   |
| Sling Stone  | 1–4    | Missile     | Slow           | Long   |
| Wooden Arrow | 1–3    | Piercing    | Fast           | Long   |
| Thrown Rock  | 1–3    | Crushing    | Slow           | Medium |

## Attack Skills

| Skill Name        | Damage Modif. | Attack Modif. | Speed Modif. | Crit Chance Modif. |
|-------------------|---------------|---------------|--------------|--------------------|
| Bite              | Normal        | Low           | Fast         | Normal             |
| Claw Swipe        | Low           | High          | Very Fast    | Low                |
| Heavy Slam        | High          | Low           | Very Slow    | High               |
| Pierce Thrust     | Normal        | Normal        | Normal       | Normal             |
| Rapid Jab         | Low           | High          | Very Fast    | Low                |
| Crushing Blow     | High          | Normal        | Slow         | High               |
| Charge Attack     | High          | Low           | Slow         | High               |
| Stab              | Normal        | High          | Fast         | Normal             |
| Sweep Attack      | Low           | Normal        | Slow         | Low                |
| Precise Strike    | Normal        | Very High     | Normal       | Very High           |

## Support Attack Skills (Prefixes)

| Prefix        | Effect |
|---------------|--------|
| Poisonous     | Adds poison damage over time. |
| Bleeding      | Causes physical damage over time. |
| Burning       | Adds fire damage over time. |
| Freezing      | Adds cold damage and slows the target. |
| Shocking      | Adds electricity damage with stun chance. |
| Corrosive     | Adds acid damage and reduces armor. |
| Crushing      | Increases armor penetration. |
| Precise       | Increases hit chance and crit chance. |
| Savage        | Increases damage but lowers hit chance. |
| Rapid         | Reduces attack interval. |
| Heavy         | Increases damage but slows attack speed. |
| Vicious       | Increases crit chance and crit damage. |
| Leeching      | Converts part of damage to health. |
| Infectious    | Spreads damage over time to nearby enemies. |

## Armor Types (Natural & Wearable)

| Armor Type | Speed Modif. | Resistance | Vulnerability |
|------------|--------------|------------|---------------|
| Fur        | Normal       | Cold Resist | Fire Weakness |
| Leather    | Normal       | Piercing Resist | Cold Weakness |
| Hide       | Slow         | Slashing Resist | Fire Weakness |
| Bone       | Slow         | Crushing Resist | Acid Weakness |
| Chitin     | Low          | Slashing Resist | Fire Weakness |
| Scales     | Slow         | Fire Resist | Electricity Weakness |
| Bark       | Very Slow    | Piercing Resist | Fire Weakness |
| Shell      | Very Slow    | Missile Resist | Crushing Weakness |
| Feathers  | Fast         | None | Fire Weakness |
| Skin      | Normal       | None | None |

## Forest Enemies (Early Biome)

| Enemy Name        | Type       | HP        | Size        | Weapon           | Armor   | Skill |
|-------------------|------------|-----------|-------------|------------------|---------|-----------------|
| Forest Bandit     | Humanoid   | Normal    | Normal      | Wooden Sword     | Leather | Precise Strike  |
| Wild Hunter       | Humanoid   | Normal    | Normal      | Wooden Spear     | Hide    | Charge Attack   |
| Forest Wolf       | Animal     | Normal    | Medium      | Teeth            | Fur     | Bite            |
| Dire Boar         | Animal     | High      | Large       | Tusks            | Hide    | Charge Attack   |
| Forest Bear       | Animal     | High      | Large       | Pawn             | Fur     | Heavy Slam      |
| Giant Ant         | Insect     | Normal    | Small       | Mandible         | Chitin  | Rapid Jab       |
| Poison Bee        | Insect     | Low       | Tiny        | Stinger          | Chitin  | Bite            |
| Forest Spider     | Insect     | Normal    | Medium      | Mandible         | Chitin  | Precise Strike  |
| Walking Sapling   | Plant      | Normal    | Medium      | Wooden Club      | Bark    | Crushing Blow  |
| Ancient Treant   | Plant      | High      | Very Large  | Wooden Staff     | Bark    | Sweep Attack   |
