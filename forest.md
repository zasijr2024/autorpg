# AutoRPG – Forest Biome Specification

This document defines all **Forest biome content** for AutoRPG.
It extends the content catalogs in **core.md** and is simulated by **engine.md**.

`forest.md` answers:
- what enemies, weapons, and skills exist in the Forest
- how Forest encounters and bosses are structured
- what hazards, materials, and loot the Forest provides

---

## Table of Contents

1. Biome Identity
2. Biome Affixes
3. Forest-Specific Weapons
4. Forest-Specific Skills
   - Skill–Weapon Compatibility
5. Forest Enemy Roster
   - Ant Colony Hierarchy
   - Giant Forest Predators
   - Plant & Wood Entities
   - Forest Humanoids
   - Forest Horrors
   - Forest Fey
   - Fungal Entities
6. Encounter Templates
7. Boss Phase Breakdowns
8. Environmental Hazards
9. Forest Materials & Loot Bias

---

## 1. Biome Identity

- Dense terrain
- High ambush frequency
- Organic materials
- Poison & control effects common
- Primary material sources: Wood, Chitin, Bone, Leather

---

## 2. Biome Affixes

| Affix | Effect |
|------|--------|
| Dense Growth | Ambush chance ↑ |
| Overgrown | Plant enemies ↑ |
| Toxic Spores | Poison chance |
| Entangling Roots | Rooted chance |
| Predatory Growth | Enemy speed ↑ |

---

## 3. Forest-Specific Weapons

These weapons are defined for forest biome use and extend the core weapon table.

| Weapon | Label | Damage | Type | Reach |
|------|-------|--------|------|-------|
| Ant Lance | Natural | High | Piercing | Medium |
| Queen Mandible | Natural | High | Piercing | Short |
| Wisp Flame | Innate | Low | Magic | Long |

---

## 4. Forest-Specific Skills

These skills are defined for forest biome use and extend the core skill table.

| Skill | Damage | Hit | Speed | Crit | Scope |
|------|--------|-----|-------|------|-------|
| Frenzied Bite | Normal | Normal | Very Fast | Normal | Single |
| Rolling Slam | High | Low | Slow | High | Single |
| Overhead Cleave | High | Normal | Slow | Normal | Cleave |
| Brood Command | None | None | Slow | None | — |
| Infectious Bite | Normal | High | Normal | Low | Single |
| Corrosive Slam | Normal | Normal | Slow | Low | Single |
| Nature's Mend | None | None | Normal | None | Ally |

**Skill Notes**
- **Brood Command**: Summons Ant Workers; does not deal direct damage. Summon count scales with boss phase.
- **Infectious Bite**: Applies Poison status on hit. If target is already Poisoned, applies Disease instead.
- **Corrosive Slam**: Applies Corroded status on hit.
- **Frenzied Bite**: Speed increases further at low HP (mirrors Frenzied prefix behavior).
- **Nature's Mend**: Heals a single ally (Ally scope). Non-attack action — skips hit/crit/damage resolution. Used by Dryad.

**Skill–Weapon Compatibility** (extends core.md Section 3.3)

| Skill | Compatible Labels |
|------|------------------|
| Frenzied Bite | Natural only |
| Rolling Slam | Natural only |
| Overhead Cleave | Wielded, Natural |
| Brood Command | Any (non-attack) |
| Infectious Bite | Natural only |
| Corrosive Slam | Natural only |
| Nature's Mend | Any (non-attack) |

---

## 5. Forest Enemy Roster

All enemies list Race, Rarity range, Material, and compatible Prefixes alongside combat stats.

---

### 5.1 Ant Colony Hierarchy

| Enemy | Race | Rarity | Archetype | Weapon | Armor | Material | Skill | Prefixes |
|------|------|--------|-----------|--------|-------|----------|-------|----------|
| Ant Worker | Insect (Ant) | Common | Swarm | Mandible | Chitin | Chitin | Rapid Jab | — |
| Ant Soldier | Insect (Ant) | Common–Uncommon | Bruiser | Ant Lance | Hardened Chitin | Chitin | Impale | Savage, Vicious |
| Ant Guard | Insect (Ant) | Uncommon | Tank | Mandible | Hardened Chitin | Chitin | Heavy Slam | Heavy, Sundering |
| Ant Spitter | Insect (Ant) | Uncommon | Controller | Venom Spit | Chitin | Chitin | Venom Spray | Poisonous, Infectious |
| Ant Queen | Insect (Ant) | Unique | Boss | Queen Mandible | Hardened Chitin | Chitin | Brood Command | Broodbound, Frenzied, Regenerating |

---

### 5.2 Giant Forest Predators

| Enemy | Race | Rarity | Archetype | Weapon | Armor | Material | Skill | Prefixes |
|------|------|--------|-----------|--------|-------|----------|-------|----------|
| Dire Squirrel | Animal (Wolf*) | Common–Uncommon | Assassin | Teeth | Fur | Bone | Frenzied Bite | Frenzied, Vicious |
| Giant Hedgehog | Animal (Bear*) | Uncommon | Tank | Spines | Hide | Bone | Rolling Slam | Heavy, Savage |
| Forest Lynx | Animal (Wolf*) | Uncommon–Rare | Assassin | Claws | Fur | Bone | Precise Strike | Precise, Vicious |
| Dire Owl | Animal (Wolf*) | Uncommon–Rare | Sniper | Talons | Feathers | Bone | Precise Strike | Precise, Vicious |
| Moss Bear | Animal (Bear) | Rare | Bruiser | Paw | Mosshide | Bone | Heavy Slam | Heavy, Savage, Regenerating |

*\*Uses closest matching race template. Squirrel/Lynx/Owl use Wolf stats (resist Cold, weak Fire). Hedgehog uses Bear stats (resist Crushing, weak Electricity).*

---

### 5.3 Plant & Wood Entities

| Enemy | Race | Rarity | Archetype | Weapon | Armor | Material | Skill | Prefixes |
|------|------|--------|-----------|--------|-------|----------|-------|----------|
| Twigling | Plant (Treant) | Common | Swarm | Branch | Bark | Wood | Rapid Jab | — |
| Thorn Creeper | Plant (Treant) | Common–Uncommon | Controller | Thorn Whip | Living Bark | Wood | Root Grasp | Poisonous, Bleeding |
| Bark Guardian | Plant (Treant) | Uncommon–Rare | Tank | Branch Halberd | Living Bark | Wood | Overhead Cleave | Heavy, Sundering |
| Vine Horror | Plant (Treant) | Rare | Bruiser | Root Slam | Living Bark | Wood | Crushing Blow | Savage, Bleeding |
| Ancient Oakheart | Plant (Treant) | Unique | Boss | Root Slam | Living Bark | Wood | Sweep Attack | Heavy, Regenerating, Broodbound |

---

### 5.4 Forest Humanoids

| Enemy | Race | Rarity | Archetype | Weapon | Armor | Material | Skill | Prefixes |
|------|------|--------|-----------|--------|-------|----------|-------|----------|
| Forest Poacher | Humanoid (Human) | Common | Skirmisher | Wooden Spear | Leather | Wood | Stab | Rapid, Precise |
| Woodcut Raider | Humanoid (Human) | Common–Uncommon | Bruiser | Wooden Axe | Hide | Wood | Heavy Slam | Savage, Heavy |
| Moss Druid | Humanoid (Human) | Uncommon–Rare | Controller | Wooden Staff | Mosshide | Wood | Root Grasp | Poisonous, Infectious |
| Bark Knight | Humanoid (Human) | Rare | Tank | Branch Halberd | Living Bark | Wood | Crushing Blow | Heavy, Sundering |
| Greenwarden | Humanoid (Elf) | Unique | Boss | Thorn Whip | Living Bark | Wood | Sweep Attack | Regenerating, Bleeding, Precise |

---

### 5.5 Forest Horrors

| Enemy | Race | Rarity | Archetype | Weapon | Armor | Material | Skill | Prefixes |
|------|------|--------|-----------|--------|-------|----------|-------|----------|
| Giant Spiderling | Insect (Spider) | Common | Swarm | Mandible | Chitin | Chitin | Bite | — |
| Widow Spider | Insect (Spider) | Uncommon–Rare | Assassin | Mandible | Chitin | Chitin | Precise Strike | Poisonous, Vicious |
| Broodmother Spider | Insect (Spider) | Unique | Boss | Mandible | Hardened Chitin | Chitin | Infectious Bite | Poisonous, Infectious, Broodbound |
| Forest Slime | Magical (Fey*) | Uncommon–Rare | Bruiser | Acid Body | Skin | Flesh | Corrosive Slam | Corrosive, Leeching |
| Spore Hulk | Plant (Treant) | Rare | Tank | Root Slam | Mosshide | Wood | Heavy Slam | Diseased, Heavy, Regenerating |

*\*Forest Slime uses Fey race stats as closest match (resist Magic, weak Iron material).*

---

### 5.6 Forest Fey

| Enemy | Race | Rarity | Archetype | Weapon | Armor | Material | Skill | Prefixes |
|------|------|--------|-----------|--------|-------|----------|-------|----------|
| Sprite | Magical (Fey) | Common–Uncommon | Skirmisher | Wooden Arrow | Feathers | Wood | Rapid Jab | Rapid, Precise |
| Will-o'-Wisp | Magical (Fey) | Uncommon–Rare | Controller | Wisp Flame | Skin | Flesh | Venom Spray | Burning, Freezing |
| Dryad | Magical (Fey) | Rare | Controller | Thorn Whip | Living Bark | Wood | Root Grasp / Nature's Mend | Regenerating, Poisonous |
| Thornfey Knight | Magical (Fey) | Rare–Epic | Bruiser | Branch Halberd | Living Bark | Wood | Overhead Cleave | Savage, Bleeding, Vicious |
| Archfey of Thorns | Magical (Fey) | Unique | Boss | Thorn Whip | Living Bark | Wood | Sweep Attack | Regenerating, Burning, Precise |

---

### 5.7 Fungal Entities

| Enemy | Race | Rarity | Archetype | Weapon | Armor | Material | Skill | Prefixes |
|------|------|--------|-----------|--------|-------|----------|-------|----------|
| Sporecap | Plant (Treant) | Common | Swarm | Acid Body | Skin | Flesh | Bite | Diseased |
| Myconid | Plant (Treant) | Common–Uncommon | Controller | Wooden Club | Mosshide | Wood | Venom Spray | Diseased, Poisonous |
| Rot Shambler | Plant (Treant) | Uncommon–Rare | Bruiser | Root Slam | Mosshide | Flesh | Heavy Slam | Diseased, Leeching |
| Fungal Zombie | Humanoid (Human) | Uncommon–Rare | Charger | Wooden Axe | Hide | Flesh | Charge Attack | Diseased, Infectious |
| Cordyceps Horror | Plant (Treant) | Unique | Boss | Root Slam | Mosshide | Flesh | Corrosive Slam | Diseased, Corrosive, Leeching |

---

## 6. Encounter Templates

These templates use encounter composition rules from core.md Section 7.

---

### 6.1 Standard Encounters

**Ant Patrol** — Swarm (primary) / Bruiser (secondary)
- 4× Ant Worker + 1× Ant Soldier
- Concept: Crowd control through numbers

**Predator Ambush** — Assassin (primary) / Charger (secondary)
- 1× Forest Lynx + 1× Dire Squirrel + 1× Fungal Zombie
- Concept: Burst speed; test reaction and survivability

**Thorn Thicket** — Controller (primary) / Swarm (secondary)
- 2× Thorn Creeper + 3× Twigling
- Concept: Root and whittle; status management

**Poacher Camp** — Skirmisher (primary) / Bruiser (secondary)
- 2× Forest Poacher + 1× Woodcut Raider
- Concept: Weapon variety; mixed reach bands

**Spider Nest** — Swarm (primary) / Assassin (secondary)
- 4× Giant Spiderling + 1× Widow Spider
- Concept: Poison pressure; target prioritization

---

### 6.2 Rare Encounters

**Moss Bear Den** — Solo (Rare)
- 1× Moss Bear (Rare, 3 prefixes)
- Concept: Sustained durability test

**Fey Glade** — Controller (primary) / Skirmisher (secondary)
- 1× Dryad + 2× Sprite
- Concept: Root and harass; positional awareness

**Fungal Bloom** — Controller (primary) / Swarm (secondary)
- 1× Myconid + 3× Sporecap + 1× Rot Shambler
- Concept: Disease stacking; DOT management

---

### 6.3 Epic Encounter

**The Thornfey Court** — Bruiser (primary) / Controller (secondary)
- 1× Thornfey Knight (Epic) + 1× Dryad + 2× Sprite
- Concept: High single-target threat with healing support; burst windows

---

## 7. Boss Phase Breakdowns

---

### 7.1 Ant Queen

**Phase 1 — Summoning** (100%–60% HP)
- Trigger: Start of encounter
- Behavior: Uses Brood Command to summon Ant Workers (2 per cast)
- Prefixes active: Broodbound
- Adds: Ant Workers, up to 6 at a time
- Status weakness: Burning (high effectiveness)
- Concept: Manage add count while dealing damage to boss

**Phase 2 — Escalation** (60%–30% HP)
- Trigger: Health threshold
- Behavior: Switches to melee with Queen Mandible; summon rate reduced
- Prefixes active: Broodbound, Frenzied
- Adds: Ant Soldiers replace Ant Workers
- Phase modifier: Empowered
- Concept: Increased direct threat; add quality over quantity

**Phase 3 — Desperation** (30%–0% HP)
- Trigger: Health threshold
- Behavior: Frenzied melee; no more summoning
- Prefixes active: Frenzied, Regenerating
- Adds: None (remaining adds become Weakened)
- Phase modifier: Enraged
- Concept: DPS race against regeneration

---

### 7.2 Ancient Oakheart

**Phase 1 — Introduction** (100%–70% HP)
- Trigger: Start of encounter
- Behavior: Slow Sweep Attacks; Root Slam targeting ranged band
- Prefixes active: Heavy
- Adds: 2× Twigling spawned from bark
- Status weakness: Fire (high effectiveness)
- Concept: Learn attack patterns; exploit slow speed

**Phase 2 — Control Phase** (70%–40% HP)
- Trigger: Health threshold
- Behavior: Entangling roots create Rooted hazards; switches to Root Grasp skill
- Prefixes active: Heavy, Regenerating
- Adds: 2× Thorn Creeper
- Phase modifier: Commanding (buffs Thorn Creepers)
- Hazard: Entangling Roots (Rooted status, proximity trigger)
- Concept: Positioning and status management

**Phase 3 — Desperation** (40%–0% HP)
- Trigger: Health threshold
- Behavior: Rapid Sweep Attacks; bark sheds (armor downgrades to Bark)
- Prefixes active: Regenerating, Broodbound
- Adds: 4× Twigling
- Phase modifier: Enraged
- Concept: Burst window while dodging swarm

---

### 7.3 Broodmother Spider

**Phase 1 — Summoning** (100%–65% HP)
- Trigger: Start of encounter
- Behavior: Spawns Giant Spiderlings while using Infectious Bite
- Prefixes active: Poisonous, Broodbound
- Adds: Giant Spiderlings (2 per wave, up to 4)
- Status weakness: Burning (high effectiveness)
- Concept: Manage poison spread through add control

**Phase 2 — Escalation** (65%–30% HP)
- Trigger: Health threshold
- Behavior: Spawns Widow Spiders instead; more aggressive melee
- Prefixes active: Poisonous, Infectious
- Adds: 1× Widow Spider per wave
- Phase modifier: Corrupted (increased Poison/Disease application rate)
- Concept: Higher threat adds; status pressure intensifies

**Phase 3 — Burn Phase** (30%–0% HP)
- Trigger: Health threshold
- Behavior: No summoning; rapid Infectious Bite spam
- Prefixes active: Infectious, Frenzied
- Adds: None
- Phase modifier: Enraged
- Concept: Survive the DOT onslaught; race to finish

---

### 7.4 Greenwarden

**Phase 1 — Introduction** (100%–70% HP)
- Trigger: Start of encounter
- Behavior: Sweep Attacks with Thorn Whip from ranged band
- Prefixes active: Bleeding, Precise
- Adds: 1× Moss Druid
- Status weakness: Fire (high effectiveness)
- Concept: Deal with controller support while closing range

**Phase 2 — Control Phase** (70%–35% HP)
- Trigger: Health threshold
- Behavior: Retreats and commands; Moss Druid uses Root Grasp
- Prefixes active: Regenerating, Bleeding
- Adds: 1× Moss Druid + 1× Bark Knight
- Phase modifier: Commanding (buffs allies)
- Hazard: Thorn Patches (Bleeding status, proximity trigger)
- Concept: Break through defensive line; disrupt healing

**Phase 3 — Desperation** (35%–0% HP)
- Trigger: Health threshold
- Behavior: Closes to melee; rapid Sweep Attack
- Prefixes active: Regenerating, Precise, Bleeding
- Adds: None (remaining allies become Weakened)
- Phase modifier: Empowered
- Concept: Final duel; burst through regeneration

---

### 7.5 Archfey of Thorns

**Phase 1 — Introduction** (100%–75% HP)
- Trigger: Start of encounter
- Behavior: Ranged Sweep Attacks; establishes thorn hazards
- Prefixes active: Burning, Precise
- Adds: 2× Sprite
- Status weakness: Cold (high effectiveness against fire-using Fey)
- Concept: Navigate hazard field while clearing adds

**Phase 2 — Escalation** (75%–50% HP)
- Trigger: Health threshold
- Behavior: Summons Dryad; Sweep Attacks intensify
- Prefixes active: Burning, Regenerating
- Adds: 1× Dryad (heals boss)
- Phase modifier: Shielded (temporary damage mitigation)
- Concept: Kill the Dryad or outlast the shield

**Phase 3 — Control Phase** (50%–25% HP)
- Trigger: Health threshold
- Behavior: Roots erupt everywhere; heavy status pressure
- Prefixes active: Regenerating, Burning, Precise
- Adds: None
- Phase modifier: Unstable (periodic fire/root area effects)
- Hazard: Ley Eruption (Magic damage + Burning, timed trigger)
- Concept: Pure hazard survival; damage during safe windows

**Phase 4 — Desperation** (25%–0% HP)
- Trigger: Health threshold
- Behavior: All hazards clear; frenzied melee
- Prefixes active: Burning, Precise (Regenerating removed)
- Adds: None
- Phase modifier: Enraged
- Concept: Clean duel; execute before Enraged overwhelms

---

### 7.6 Cordyceps Horror

**Phase 1 — Summoning** (100%–65% HP)
- Trigger: Start of encounter
- Behavior: Spawns Sporecaps while using Corrosive Slam
- Prefixes active: Diseased
- Adds: 3× Sporecap
- Status weakness: Fire (high effectiveness)
- Concept: Clear adds before Disease spreads

**Phase 2 — Escalation** (65%–35% HP)
- Trigger: Health threshold
- Behavior: Spawns Fungal Zombies; more aggressive melee
- Prefixes active: Diseased, Corrosive
- Adds: 2× Fungal Zombie
- Phase modifier: Corrupted
- Hazard: Spore Cloud (Disease status, atmospheric, timed)
- Concept: Armor degradation through Corroded stacking; DOT pressure

**Phase 3 — Desperation** (35%–0% HP)
- Trigger: Health threshold
- Behavior: Absorbs remaining adds (heals per add consumed); rapid Corrosive Slam
- Prefixes active: Corrosive, Leeching
- Adds: None (consumed)
- Phase modifier: Enraged
- Concept: Race the heal; punished for leaving adds alive

---

## 8. Environmental Hazards

Forest-specific hazards following hazard rules from core.md Section 10.

| Hazard | Trigger | Effect | Duration | Avoidance |
|--------|---------|--------|----------|-----------|
| Toxic Spore Cloud | Proximity | Poison status | Persistent | Move out of area |
| Entangling Roots | Proximity | Rooted status | Timed (3 ticks) | Speed-based mitigation |
| Thorn Patches | Proximity | Bleeding status | Persistent | Reposition |
| Falling Canopy | Timed | Crushing damage | One-shot | Speed-based mitigation |
| Ley Eruption | Timed | Magic damage + Burning | One-shot | Positioning |
| Spore Burst | Event (enemy death) | Disease status | One-shot | Range band |
| Quickmoss | Proximity | Slow (Freezing equivalent) | Persistent | Move out of area |

**Forest Hazard Rules**
- Toxic Spore Clouds intensify with the Toxic Spores biome affix
- Entangling Roots intensify with the Entangling Roots biome affix
- Spore Burst triggers when Fungal enemies die, affecting Melee range band
- Plant boss phases may create hazards as part of phase transitions

---

## 9. Forest Materials & Loot Bias

### 9.1 Biome Material Table

| Material | Source | Availability |
|---------|--------|-------------|
| Wood | All plant enemies, environmental harvesting | Common |
| Chitin | All insect enemies | Common |
| Bone | All animal enemies | Common |
| Leather | Animal enemies, humanoid enemies | Common |
| Flesh | Slimes, fungal enemies | Common |
| Living Wood | Rare plant enemies, bosses | Rare |
| Hardened Chitin | Rare insect enemies, bosses | Rare |
| Fey Essence | Fey enemies (Rare+) | Rare |
| Cordyceps Extract | Fungal enemies (Rare+) | Rare |

### 9.2 Loot Category Bias

| Category | Forest Bias |
|---------|-------------|
| Materials | Wood, Chitin, Bone dominant |
| Weapons | Natural and Wielded (wooden) most common |
| Armor | Bark, Chitin, Leather, Hide most common |
| Consumables | Antidotes and healing items more frequent (Poison-heavy biome) |
| Relics | Nature and poison themed |
| Currency | Standard |
