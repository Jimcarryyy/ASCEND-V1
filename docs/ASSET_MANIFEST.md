# ASCEND-V1 — MASTER 2D ASSET MANIFEST & DESIGN PHILOSOPHY

> **Technical Specification Document**  
> **Master Entry Point:** https://raw.githubusercontent.com/Jimcarryyy/ASCEND-V1/main/ASCEND.md  
> **Scope:** 2D Asset Inventory, Dual Visual Identity, Design Consistency Rules, Aspect Ratios, Color Palettes, & 9-Slice Geometry.

---

## 1. Visual Design Philosophy & Harmony Rules

ASCEND-V1 maintains strict visual coherence across all 2D assets using a **Dual Visual Identity Framework**:

### Dual Identity Breakdown
1. **In-Combat HUD Identity (Clean Vector & Minimalist Geometry):**
   - **Goal:** Maximum legibility during high-speed combat. Zero screen clutter.
   - **Style:** Flat vector shapes, thin geometric borders (1px-2px outline), high-contrast fills, dark charcoal background containers.
   - **Colors:** Crimson Red (Health), Emerald Green (Stamina), Celestial Blue (Energy), Solar Gold (Cooldowns).

2. **Out-of-Combat Panel Identity (Handcrafted Dark Fantasy):**
   - **Goal:** High-dopamine, immersive RPG menu management.
   - **Style:** Heavy slate/parchment textured backgrounds, golden filigree borders, bronze corner rivets, distressed metallic trim.
   - **Colors:** Deep Obsidian Slate (#121216), Royal Gold (#FFD700), Aged Bronze (#8B5A2B), Crimson Ribbon (#8B0000).

---

## 2. Asset Technical Standards & Specifications

To ensure optimal performance and eliminate visual stretching in Roblox Studio:

* **Resolution Benchmarks:**
  - Standard Icons (Skills, Items, Statuses): 128x128 pixels (1:1 Aspect Ratio)
  - Slot & Rarity Frames: 256x256 pixels (1:1 Aspect Ratio)
  - Banner Banners & Dividers: 512x128 pixels (4:1 Aspect Ratio)
  - Full Modal Frame Backgrounds: 1024x1024 pixels (1:1 Aspect Ratio)
* **File Format:** 32-bit PNG with transparent alpha channel.
* **Scale Unit Standard:** Roblox UI elements must use relative Scale units. Modal background frames use ScaleType = Enum.ScaleType.Slice (9-Slice) with 32px border margin offsets.

---

## 3. Comprehensive Master 2D Asset Inventory

### Category A: Minimalist Combat HUD Assets

| Asset Name | Target Resolution | Primary Colors | Description / Usage |
| :--- | :--- | :--- | :--- |
| hud_slot_base | 128x128 PNG | #1E1E23 (Dark Charcoal) | Action skill slot container frame |
| hud_slot_active | 128x128 PNG | #2192FF (Celestial Blue) | Active selection glow border overlay |
| hud_cooldown_mask | 128x128 PNG | #000000 (80% Alpha) | Radial/Vertical sweep overlay for active cooldowns |
| hud_key_badge | 64x64 PNG | #2A2A30 (Dark Gray) | Keybind indicator badge for PC (M1, M2, Q, E, R, Shift) |
| hud_reticle_dot | 32x32 PNG | #FFFFFF (Crisp White) | Center screen aim reticle with faint outer ring |
| hud_boss_frame | 512x64 PNG | #141418, #FFD700 | Boss top health bar frame with gold terminal tips |
| hud_boss_phase_dim | 32x32 PNG | #3A3A40 (Dark Gray) | Inactive boss phase diamond emblem |
| hud_boss_phase_lit | 32x32 PNG | #FFD700 (Solar Gold) | Active boss phase diamond emblem |

---

### Category B: Handcrafted Fantasy Menu & Modal Assets

| Asset Name | Target Resolution | Primary Colors | Description / Usage |
| :--- | :--- | :--- | :--- |
| panel_modal_bg | 1024x1024 PNG | #121216, #FFD700 | Master modal frame background with gold filigree borders |
| panel_header_banner | 512x128 PNG | #8B0000, #FFD700 | Window title header ribbon with gold metallic ends |
| panel_divider_line | 512x32 PNG | #FFD700 (Royal Gold) | Horizontal section separator with center ornamental emblem |
| panel_grid_slot | 128x128 PNG | #1A1A20 (Slate Gray) | Recessed dark iron inventory grid slot frame |
| panel_button_primary | 256x64 PNG | #2A2A35, #FFD700 | Main interactive button with beveled metallic trim |
| panel_button_hover | 256x64 PNG | #3A3A48, #FFE066 | Brightened hover state overlay for primary buttons |
| panel_tooltip_bg | 256x256 PNG | #0E0E12 (Deep Black) | Stat hover panel container with thin gold border |

---

### Category C: Equipment Rarity Frames & Border Badges

| Rarity Tier | Asset Name | Border Color (Hex) | Visual Features |
| :--- | :--- | :--- | :--- |
| Common | frame_rarity_common | #FFFFFF (White) | Clean silver/white metallic border |
| Uncommon | frame_rarity_uncommon | #38E54D (Green) | Emerald green border with notched corners |
| Rare | frame_rarity_rare | #2192FF (Blue) | Sapphire blue border with inner glow gradient |
| Epic | frame_rarity_epic | #9C2C77 (Purple) | Royal purple frame with ornamental corner trim |
| Legendary | frame_rarity_legendary | #FFD700 (Gold) | Intricate gold filigree frame with corner rubies |
| Mythic | frame_rarity_mythic | #FF1E1E (Crimson) | Crimson dark iron frame with aura glow effect |

---

### Category D: Weapon Archetype & Equipment Icons

| Asset Name | Asset Category | Visual Description |
| :--- | :--- | :--- |
| icon_weapon_blade | Weapon Archetype | Sleek Katana blade silhouette with glowing blue edge |
| icon_weapon_greatsword | Weapon Archetype | Heavy two-handed broadsword with stone-crushing hilt |
| icon_weapon_daggers | Weapon Archetype | Crossed curved daggers with dripping poison aura |
| icon_weapon_staff | Weapon Archetype | Wooden catalyst staff topped with an orb crystal |
| icon_gear_chestplate | Armor Equipment | Heavy iron chestplate armor icon |
| icon_gear_helmet | Armor Equipment | Knight visor helmet icon |
| icon_gear_boots | Armor Equipment | Armored greaves / boots icon |
| icon_gear_ring | Accessory | Gold signet ring with inset gem |
| icon_gear_amulet | Accessory | Pendant necklace with glowing shard |

---

### Category E: Combat Skill & Ability Icons

| Asset Name | Skill Keybind | Visual Description |
| :--- | :--- | :--- |
| icon_skill_m1_slash | Light Attack (M1) | Triple light blade slash motion arc |
| icon_skill_m2_heavy | Heavy Attack (M2) | Downward heavy overhead slam with impact shockwave |
| icon_skill_dodge | Dodge / Roll | Ghosted dash silhouette with directional motion trails |
| icon_skill_parry | Parry / Block | Glowing heraldic shield deflecting an incoming blade |
| icon_skill_blade_whirl | Blade Archetype Q | 360-degree spinning sword wave trajectory |
| icon_skill_cleave_wave | Greatsword Archetype Q | Ground-splitting horizontal energy arc |
| icon_skill_shadow_step | Daggers Archetype Q | Teleport shadow blur behind enemy target |
| icon_skill_arcane_burst | Staff Archetype Q | Expanding radial magic nova energy ring |

---

### Category F: Currencies, Materials & Status Indicators

| Asset Name | Asset Type | Visual Description |
| :--- | :--- | :--- |
| icon_currency_gold | Currency | Stack of glowing minted gold fantasy coins |
| icon_currency_shard | Currency | Floating blue Ascension Shard crystal |
| icon_mat_stone_low | Upgrade Material | Rough bronze blacksmith enhancement stone |
| icon_mat_stone_mid | Upgrade Material | Polished silver rune stone |
| icon_mat_stone_high | Upgrade Material | Glowing radiant gold enhancement artifact |
| icon_status_stunned | Status Indicator | Dazed yellow spiral star over broken skull |
| icon_status_bleed | Status Indicator | Dripping crimson blood droplet with aura |
| icon_status_guardbreak | Status Indicator | Fractured orange shield with impact crack |
| icon_status_empowered | Status Indicator | Upward glowing golden sword with radiant aura |