# ASCEND-V1 — COMBAT SYSTEM SPECIFICATION

> **Technical Specification Document**  
> **Master Entry Point:** https://raw.githubusercontent.com/Jimcarryyy/ASCEND-V1/main/ASCEND.md  
> **Scope:** Server-Authoritative Combat Engine, Hitbox Pipelines, Combos, Defensive Mechanics, & Damage Formulas.

---

## 1. Security Architecture & Server Validation

To ensure absolute exploit resistance, combat operates on an Intent-Execution Pipeline:

[CLIENT]                                    [SERVER]
  |                                            |
  +--- 1. Press M1 (Fire AttackIntent) ------->|
  |                                            |-- 2. Validate Cooldowns (os.clock())
  |                                            |-- 3. Validate Stamina & Stun State
  |                                            |-- 4. Execute Shapecast / Spatial Query
  |                                            |-- 5. Apply Damage & Status Effects
  |<-- 6. Replicate Visual Effects / Hits -----|

### Server Guard Checks (Evaluated on every attack)
1. Action Cooldown Check: os.clock() - LastAttackTime >= AttackData.Cooldown
2. State Check: Ensure player state is "Neutral" or "ComboBuffering" (Not "Stunned", "KnockedDown", or "ParryStunned").
3. Resource Check: PlayerStamina >= AttackData.StaminaCost
4. Distance Sanity Check: Target distance from attacker must be <= AttackData.MaxRange + LagToleranceMargin.

---

## 2. Hitbox Detection Pipeline

Hitboxes are computed strictly on the server during the active damage frame window using WorldRoot:Blockcast or WorldRoot:Shapecast.

### Spatial Query Specification
* Shapecast Type: CFrame-oriented Caster (WorldRoot:Blockcast or WorldRoot:Spherecast).
* OverlapParams / RaycastParams:
  - FilterType: RaycastFilterType.Exclude
  - FilterDescendantsInstances: Attacker character instance and non-collidable map props.
  - CollisionGroup: "CombatEntities"
* Hit Register Prevention: Each attack swing maintains a HitTable dictionary on the server. An enemy entity can only be damaged once per swing iteration.

---

## 3. Combo Mechanics & Timelines

### Light Attack String (M1 Chain)
A standard melee weapon features a 4-hit light combo sequence:

| Combo Step | Windup (Prep) | Damage Window | Recovery Window | Combo Buffer Window | Damage Multiplier | Impact Effect |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| M1_1 | 0.15s | 0.10s | 0.20s | 0.15s – 0.35s | 1.0x Base | Light Flinch |
| M1_2 | 0.12s | 0.10s | 0.20s | 0.15s – 0.35s | 1.0x Base | Light Flinch |
| M1_3 | 0.14s | 0.10s | 0.22s | 0.15s – 0.38s | 1.2x Base | Medium Flinch |
| M1_4 (Finisher) | 0.25s | 0.15s | 0.45s | None (Resets) | 1.8x Base | Knockback + Stun (0.8s) |

* Combo Reset Timer: If no attack intent is received within 0.8 seconds after the damage window ends, the combo index resets to M1_1.
* Combo Buffering: If the player clicks M1 during the Combo Buffer Window, the next attack is queued and executes automatically upon entering the next recovery window.

### Heavy Attack (M2)
* Windup Time: 0.45 seconds (Telegraphed windup animation).
* Stamina Cost: 25 Stamina.
* Special Attribute: Guard Break. Deals 2.5x damage against blocking targets and breaks guard state.

---

## 4. Defensive & Reaction Mechanics

                       [INCOMING ATTACK HITBOX]
                                  |
        +-------------------------+-------------------------+
        |                         |                         |
        v                         v                         v
 [TARGET DODGE]            [TARGET PARRY]            [TARGET BLOCK]
(i-Frame Active)          (In Parry Window)          (Holding Block)
        |                         |                         |
        v                         v                         v
  0 Damage Taken            0 Damage Taken            70% Damage Reduction
Attacker Continues        Attacker Stunned (1.2s)     Stamina Drained
                          Defender +10 Stamina

### A. Dodge / Roll
* Activation: Keypress (Shift / Space / Double Tap).
* i-Frame Duration: 0.25 seconds starting immediately at activation frame.
* Cooldown: 1.2 seconds.
* Stamina Cost: 20 Stamina.

### B. Parry / Deflect
* Activation Window: First 0.18 seconds of pressing Block (F).
* Success Outcome:
  - Attacker suffers Parry Stun for 1.2 seconds.
  - Attacker combo string is interrupted immediately.
  - Defender receives 0 damage and recovers +10 Stamina.
* Whiff Penalty: If no attack hits during the 0.18s window, the defender enters recovery for 0.4s and cannot block.

### C. Block / Guard
* Damage Reduction: 70% physical damage mitigation.
* Stamina Drain: Drains stamina equal to BaseDamage * 0.5.
* Guard Break: If Stamina drops to 0 while blocking, target enters Guard Break Stun for 2.0 seconds and takes 1.5x damage.

---

## 5. Server State Engine

Every combatant (Player Character & Enemy AI) maintains a server-authoritative State attribute:

Type Definitions:
- Neutral
- Attacking
- Blocking
- Parrying
- iFrame
- Stunned
- KnockedDown

State Rules:
* State transitions are managed by a centralized StateService.
* States enforce mutual exclusion (e.g., an entity in state "Stunned" cannot enter "Attacking" or "Blocking").

---

## 6. Damage & Stat Formulas

### Physical Damage Calculations
- RawDamage = BaseWeaponDamage * (1 + (AttackerStrength * 0.025))
- CritRoll = math.random() <= AttackerCritRate
- FinalDamage = CritRoll ? (RawDamage * AttackerCritDamage) : RawDamage
- DamageTaken = FinalDamage * (100 / (100 + TargetArmor))

### Stat Multiplier Reference
* 1 STR: +2.5% Base Damage
* 1 DEX: +0.5% Attack Speed, +0.3% Crit Rate
* 1 VIT: +10 Health Points
* 1 END: +5 Stamina Points, +5% Stamina Regen Rate