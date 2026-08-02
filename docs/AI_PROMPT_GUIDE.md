# ASCEND-V1 — COMPLETE AI ASSET GENERATION PROMPT GUIDE

> **Technical Specification Document**  
> **Master Entry Point:** https://raw.githubusercontent.com/Jimcarryyy/ASCEND-V1/main/ASCEND.md  
> **Scope:** Copy-Paste AI Prompts for Midjourney, Leonardo, Flux, and DALL-E for all 2D Game Assets.

---

## 1. Global Prompting Rules & Negative Parameters

When generating assets using AI models (Midjourney, Leonardo AI, Flux, DALL-E 3), apply these global settings to enforce transparency and clean vector isolation:

### Universal Prompt Modifiers
* Style Keyword: 2d video game UI asset, vector art style, clean outline, dark fantasy RPG UI, isolated on solid black background.
* Technical Modifiers: 8k resolution, centered composition, game icon design, crisp edges, high contrast.
* Universal Negative Prompt (--no parameter in Midjourney): photorealism, 3d render, realistic photographic texture, human face, complex background, shadow, blurry edges, tilted camera, depth of field.

---

## 2. Category Prompts

### Category A: Minimalist HUD Elements

Prompt: Action Skill Slot Frame (hud_slot_base)
2d game UI slot frame, dark charcoal square container, minimalist thin light gray outline, clean flat vector design, dark fantasy RPG HUD element, isolated on solid black background --ar 1:1 --no 3d render, shadows, glowing effects

Prompt: Minimalist Crosshair Reticle (hud_reticle_dot)
2d vector crosshair reticle, minimal white center dot, subtle glowing outer circle, clean gaming UI asset, isolated on solid black background --ar 1:1 --no complex lines, 3d

Prompt: Boss Health Bar Frame (hud_boss_frame)
2d game boss health bar frame, sleek dark iron horizontal bar, ornate gold metallic terminal tips on left and right, dark fantasy UI asset, isolated on solid black background --ar 4:1 --no fill texture, 3d camera tilt

---

### Category B: Handcrafted Fantasy Panels & Modals

Prompt: Master Window Panel Frame (panel_modal_bg)
2d dark fantasy game UI window frame, square slate stone texture center, intricate gold filigree metal border frame, bronze corner rivets, dark fantasy RPG menu frame, orthogonal top-down flat view, isolated on solid black background --ar 1:1 --no tilted camera, 3d depth, text, buttons inside

Prompt: Header Banner Ribbon (panel_header_banner)
2d dark crimson silk banner ribbon, gold metallic filigree ornamental borders on edges, dark fantasy RPG UI header banner, horizontal composition, isolated on solid black background --ar 4:1 --no text, 3d tilt

Prompt: Section Divider Line (panel_divider_line)
2d game UI section divider line, horizontal gold filigree metal bar with center diamond emblem, ornate fantasy decoration, isolated on solid black background --ar 16:1 --no background, 3d angle

---

### Category C: Equipment Rarity Frames

Prompt: Legendary Gold Rarity Frame (frame_rarity_legendary)
2d inventory item rarity frame, square format, intricate gold filigree border frame, ruby gem accents on four corners, golden glowing inner aura, hollow center for item icon, isolated on solid black background --ar 1:1 --no item inside, 3d angle

Prompt: Mythic Crimson Rarity Frame (frame_rarity_mythic)
2d inventory item rarity frame, square format, dark crimson iron frame with glowing red energy runes, dark fantasy RPG UI frame, hollow center, isolated on solid black background --ar 1:1 --no item inside, 3d angle

---

### Category D: Weapon Archetype & Equipment Icons

Prompt: Katana Blade Icon (icon_weapon_blade)
2d game weapon icon, curved Japanese Katana blade, glowing celestial blue sharp edge, dark steel hilt, vector art style, dark fantasy RPG asset, centered, isolated on solid black background --ar 1:1 --no realistic hands, 3d render

Prompt: Greatsword Icon (icon_weapon_greatsword)
2d game weapon icon, massive two-handed broadsword, heavy stone-crushing crossguard, glowing golden runes along blade center, dark fantasy RPG asset, centered, isolated on solid black background --ar 1:1 --no character holding sword, 3d

Prompt: Heavy Chestplate Armor Icon (icon_gear_chestplate)
2d game armor icon, heavy dark steel knight chestplate armor, gold trim highlights, dark fantasy RPG equipment asset, centered, isolated on solid black background --ar 1:1 --no character body, 3d render

---

### Category E: Skill & Ability Icons

Prompt: Light Attack Slash Combo (icon_skill_m1_slash)
2d game skill icon, triple white and light blue sword slash motion arcs, high velocity arc energy, vector art, dark fantasy RPG icon, isolated on solid black background --ar 1:1 --no character, sword model, 3d

Prompt: Heavy Slam Attack (icon_skill_m2_heavy)
2d game skill icon, heavy downward ground impact shockwave, orange and red cracked earth energy burst, vector art, dark fantasy RPG icon, isolated on solid black background --ar 1:1 --no character model, 3d

Prompt: Dodge Roll Silhouette (icon_skill_dodge)
2d game skill icon, ghosted dash silhouette with horizontal speed motion lines, bright cyan energy trail, vector art, dark fantasy RPG icon, isolated on solid black background --ar 1:1 --no realistic human

Prompt: Parry Shield Deflect (icon_skill_parry)
2d game skill icon, heraldic shield emblem deflecting a glowing sword strike, golden energy spark burst impact point, vector art, dark fantasy RPG icon, isolated on solid black background --ar 1:1 --no 3d render

---

### Category F: Currencies & Status Effect Icons

Prompt: Gold Currency Icon (icon_currency_gold)
2d game currency icon, stack of minted shiny gold fantasy coins, golden radiant glow, vector art, dark fantasy RPG icon, isolated on solid black background --ar 1:1 --no realistic photo

Prompt: Stunned Status Indicator (icon_status_stunned)
2d game status icon, yellow dizzy spiral star bursting over fractured skull outline, vector art, status debuff icon, isolated on solid black background --ar 1:1 --no realistic 3d skull