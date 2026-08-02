# ASCEND-V1 — PROGRESSION & LOOT SYSTEM SPECIFICATION

> **Technical Specification Document**  
> **Master Entry Point:** https://raw.githubusercontent.com/Jimcarryyy/ASCEND-V1/main/ASCEND.md  
> **Scope:** Leveling Curve, Stat Allocation, Weapon Rarity Budgeting, Weighted Drop Tables, & Weapon Mastery.

---

## 1. Character Leveling & XP Curve

Character progression relies on a predictable, non-linear experience curve designed for sustained engagement.

### Experience Formula
The experience required to reach `Level N` from `Level N-1` is computed on the server:

  RequiredXP(N) = math.floor(100 * ((N - 1) ^ 1.85) + 50)

### Leveling Attributes
* Maximum Level Cap (V1): Level 100
* Stat Point Award: Each level up grants +3 Unallocated Stat Points.
* Base Character Stats at Level 1:
  - Max Health: 100
  - Max Stamina: 100
  - Base Damage Multiplier: 1.0x
  - Base Defense: 0

---

## 2. Primary Stat Attributes & Scaling Math

Players manually allocate stat points into 5 primary attributes via the Character Modal:

| Stat Name | Primary Effect | Secondary Effect | Scaling Formula |
| :--- | :--- | :--- | :--- |
| Strength (STR) | Physical Damage | Heavy Attack Impact | +2.5% Physical Damage per point |
| Dexterity (DEX) | Attack Speed & Crit Rate | Movement Speed | +0.4% Attack Speed, +0.3% Crit Rate per point |
| Intelligence (INT) | Skill / Ability Damage | Cooldown Reduction | +3.0% Ability Damage, +0.2% CDR per point |
| Vitality (VIT) | Maximum Health | Health Regeneration | +12 Health, +0.1 Health Regen/sec per point |
| Endurance (END) | Maximum Stamina | Stamina Recovery | +6 Stamina, +4.0% Stamina Recovery Rate per point |

---

## 3. Weapon Rarity Pipeline & Stat Budget

All weapons and gear scale their attributes using a base stat budget multiplied by a Rarity Factor:

| Rarity Tier | Display Color | Stat Budget Multiplier | Bonus Perk Slots | Base Drop Rate Weight |
| :--- | :--- | :--- | :--- | :--- |
| Common | White (#FFFFFF) | 1.00x | 0 Slots | 60.0% (6000) |
| Uncommon | Green (#38E54D) | 1.25x | 1 Minor Perk | 25.0% (2500) |
| Rare | Blue (#2192FF) | 1.60x | 1 Major Perk | 10.0% (1000) |
| Epic | Purple (#9C2C77) | 2.10x | 2 Major Perks | 4.0% (400) |
| Legendary | Gold (#FFD700) | 2.80x | 1 Signature Boss Skill | 0.9% (90) |
| Mythic | Red (#FF1E1E) | 3.80x | Unique Active Ability | 0.1% (10) |

### Stat Generation Formula (Server-Side Execution)
When a weapon drops, its primary stat rolls within a bounded range:

  BaseStat = ItemBaseValue * RarityMultiplier
  FinalStat = math.floor(BaseStat * (0.95 + (math.random() * 0.10)))

---

## 4. Server-Authoritative Loot Engine

Loot generation occurs strictly on the server when a mob or boss entity dies.

### Loot Calculation Pipeline
1. Mob Death Trigger: Server verifies mob hit history and tags participating players who dealt >= 5% total damage.
2. Roll Base Currency: Award Gold scaled by mob level.
3. Roll Drop Table: Iterate through the entity's Drop Table array using weighted random selection:

   TotalWeight = Sum of all Item Weights in Mob Drop Table
   Roll = math.random(1, TotalWeight)
   Iterate through table: If Roll <= CumulativeWeight -> Select Item

4. Pity Counter Engine:
   - Every boss kill increments the player's session `PityCounter` by +1.
   - If `PityCounter >= 50` and no Legendary/Mythic item dropped, the next drop forcefully upgrades to a guaranteed Legendary drop and resets `PityCounter = 0`.

---

## 5. Weapon Mastery & Talent System

In addition to character level, players develop mastery over specific weapon archetypes by actively using them in combat.

### Weapon Mastery XP
* Dealing damage with a weapon grants Mastery XP equal to `DamageDealt * 0.1`.
* Mastery Level Cap: Level 20 per weapon archetype.

### Mastery Milestone Tree (Per Archetype)
- Level 5: Passive +5% Attack Speed with this weapon type.
- Level 10: Passive -10% Stamina Cost for heavy attacks with this weapon type.
- Level 15: Passive +15% Critical Damage with this weapon type.
- Level 20: Unlocks the Archetype Ultimate Ability (Equippable in Skill Slot 3).

---

## 6. Equipment Enhancement Engine (+1 to +10)

Players can upgrade weapons at the Hub Smithy using Gold and Upgrade Stones:

| Enhancement Level | Success Rate | Stat Boost | Fail Penalty |
| :--- | :--- | :--- | :--- |
| +1 to +3 | 100% | +5% Base Damage / level | None |
| +4 to +6 | 75% | +7% Base Damage / level | -1 Enhancement Level on fail |
| +7 to +9 | 40% | +10% Base Damage / level | -1 Enhancement Level on fail |
| +10 (Max) | 15% | +20% Base Damage | Item locked from further upgrade |

* Protection Items: Using an "Ascension Shard" during +4 to +10 attempts prevents level degradation on failure.