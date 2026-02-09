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
2. Core Taxonomies  
3. Combat Building Blocks  
4. Modifiers & Status Effects  
5. Defense & Materials  
6. Entity Identity  
7. Encounter & Boss Design  
8. Loot & Rewards  
9. Player Entity  
10. Environmental Hazards  
11. Crafting & Upgrades  
12. Consumables  
13. Relics  
14. Player Progression Axes  
15. World Map & Biome Flow  
16. Factions & World State  
17. Anti-Power-Creep & Design Philosophy  

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

---

### 3.2 Attack Skills

Skills define **how** an attack is executed.

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
| Crushing | Armor penetration |
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

### 4.2 Status Effects

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

Encounter and boss design define **composition, pacing, and behavior**.
Execution is handled by the engine.

- Encounters emphasize one dominant concept.
- Difficulty scales by:
  - enemy count
  - rarity
  - interaction density
- Bosses are multi-phase and telegraphed.

---

## 8. Loot & Rewards

Loot defines progression and build variety.

- Loot complexity scales with rarity.
- Boss rewards are deterministic.
- Duplicate loot converts into materials or currency.
- All encounters grant progress.

---

## 9. Player Entity

The player is a persistent entity across runs.

- The player equips weapons, armor, relics.
- Skills are unlocked, not learned via drops.
- Player identity persists beyond individual runs.

---

## 10. Environmental Hazards

Hazards are biome-bound modifiers.

- Hazards apply consistent effects.
- Hazards interact with statuses and positioning.
- Hazards never override core rules.

---

## 11. Crafting & Upgrades

Crafting converts materials into **agency**.

- Crafting is deterministic.
- Upgrades are branching, not linear.
- Crafting cannot bypass vulnerabilities.

---

## 12. Consumables

Consumables provide temporary effects.

- Consumables never stack infinitely.
- Consumables are optional but powerful.
- Consumables never trivialize bosses.

---

## 13. Relics

Relics modify **rules**, not stats.

- Relics enable unconventional builds.
- Relics have clear tradeoffs.
- Unique relics are boss-bound.

---

## 14. Player Progression Axes

Progression is divided into **run**, **meta**, and **unlock** layers.

- No axis dominates all builds.
- Progress improves consistency before power.
- Failure always grants progress.

---

## 15. World Map & Biome Flow

The world is composed of biome nodes.

- Biomes bias enemies and loot.
- Branching paths offer meaningful choices.
- Boss nodes gate progression.

---

## 16. Factions & World State

Factions influence biomes over time.

- Factions expand, retreat, and conflict.
- Player actions shift world state.
- World state persists across runs.

---

## 17. Anti-Power-Creep & Design Philosophy

- Complexity > numbers
- Systems > stats
- Choice > optimization
- Determinism > randomness

The core exists to support **infinite content without refactor**.
