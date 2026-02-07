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
