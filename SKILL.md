# SKILL: Millennium Dawn & Total War 2030 Submod Development Knowledge Base

---
name: md-total-war-2030-submod-guide
description: Comprehensive development skill, engine rules, console workarounds, raid mechanics, and architecture guide for Millennium Dawn submodding (Total War 2030).
---

## 1. Engine Rules & Syntax Constraints

### Clausewitz Date Triggers
- `date` comparison triggers in HOI4 **DO NOT** accept `>=` or `<=` operators.
- **Correct**: `date > 2015.1.1` or `date < 2015.1.1`.
- **Incorrect**: `date >= 2015.1.1` (causes parser syntax error).

### Building Tokens
- Anti-Air building token in HOI4 / Millennium Dawn building definitions (`00_buildings.txt`) is `anti_air_building` (NOT `anti_air`).

### Focus Tree Bypass Behavior (`bypass = { ... }`)
- When a national focus has a `bypass` block that evaluates to `true`, the HOI4 engine skips `completion_reward` entirely unless `bypass_effect = { ... }` is explicitly provided.
- *Example*: In Millennium Dawn's `BRA_pay_back_the_imf`, if foreign debt ideas are absent, the focus bypasses without executing the `remove_ideas = BRA_idea_crippled_currency_*` effect.

### Localization Rules & Encoding
- All English localization files in `localisation/english/*_l_english.yml` MUST be encoded in **UTF-8 BOM** (`utf-8-sig`).
- Missing BOM header causes text keys to render raw in-game (e.g. `tw2030_escalation.1.t`).

---

## 2. In-Game Console Debugging & Workarounds

### Console Command Syntax for `effect`
- Debug mode MUST be active (`debug` entered in console or `-debug` launch flag).
- The HOI4 console parser requires **NO SPACES** around the `=` sign in `effect`:
  - **Correct**: `effect remove_ideas=BRA_idea_crippled_currency_one`
  - **Incorrect**: `effect remove_ideas = BRA_idea_crippled_currency_one` (triggers "invalid effect name").
- Alternatively, force focus completion and execute its reward instantly via: `focus <focus_id>` (e.g. `focus BRA_encourage_consumption`).

---

## 3. Threat Scoping & World Tension vs Country Threat

### Global Threat vs Country-Scoped Threat
- `threat` outside a country scope evaluates **Global World Tension** (`0.00` to `1.00`). Historical events like 9/11 (2001) boost global threat above `0.40` (40%).
- Inside a country scope or `any_country = { is_ai = no threat > 0.35 }`, `threat` evaluates that specific nation's generated threat.
- **Rule**: Never use global `threat > 0.40` to detect early player aggression, as historical events will trigger it prematurely in 2001–2002. Scope threat checks specifically to non-AI player countries:
  ```pdx
  any_country = {
      is_ai = no
      threat > 0.35
  }
  ```

---

## 4. Raid System Mechanics & Overt / Covert Peacetime Attacks

### Peacetime Raids in Millennium Dawn
- Raids in Millennium Dawn (`common/raids/`) DO NOT require formal declarations of war.
- In native MD, `air_strike_fuel_storage` and `sub_slcm_coastal_strike` have `base = 20` or `base = 1000` AI scoring.
- `sub_slcm_coastal_strike` in MD base (`sub_missile_raids.txt`) had `show_target = { always = yes }` and `available = { always = yes }`, causing UK/USA submarines with cruise missiles to launch random coastal strikes on peaceful nations.

### Raid Scoping Fix Pattern
- Override `common/raids/sub_missile_raids.txt` in the submod with proper diplomatic gates:
  ```pdx
  show_target = {
      NOT = { is_in_faction_with = FROM }
      raid_show_target_opinion_neutral = yes
  }
  available = {
      raid_target_eligible = yes
      OR = {
          has_war_with = FROM
          has_wargoal_against = FROM
          has_country_flag = promised_retaliation_against@FROM
      }
  }
  ```

---

## 5. Local Submod Installation & Launcher Registration

### Submod Descriptor Files
1. Mod descriptor inside submod folder: `descriptor.mod`.
2. Launcher descriptor placed at: `~/Documents/Paradox Interactive/Hearts of Iron IV/mod/total_war_2030.mod`.
   - Content:
     ```pdx
     name="Total War 2030"
     path="/Users/caue/Workspace/Millennium-Dawn/total-war-2030-submod"
     dependencies={
         "Millennium Dawn: Modern Day Mod"
         "Millennium Dawn: Developer Version"
     }
     supported_version="1.19.*"
     ```
3. Playset registration in `~/Documents/Paradox Interactive/Hearts of Iron IV/dlc_load.json`:
   - Add `"mod/total_war_2030.mod"` to `"enabled_mods"`.

---

## 6. Submod Architecture & Layered Escalation Engine

### Decoupled Submod Boundary
- All submod code resides strictly in `/total-war-2030-submod/`.
- Never modify files under base Millennium Dawn directly.

### Four Escalation Eras
1. **Era 1 (2000–2014)**: Peace & Stability (Submod triggers inactive).
2. **Era 2 (2015–2024)**: Rearmament & Regional Flashpoints (`tw2030_readiness_level_1`).
3. **Era 3 (2025–2029)**: Arms Race & A2/AD Deployment (`tw2030_readiness_level_2` & `3`).
4. **Era 4 (2030+)**: Total War Era (`tw2030_readiness_level_4`).

### Tag-Free Dynamic State Engine
- Events and dynamic modifiers driven purely by country state variables (no hardcoded tags):
  - Industrial Conversion (`conversion_cost_civ_to_mil_factor`, `industrial_capacity_factory`)
  - Recruitment Surge (`training_time_army_factor`, `conscription_factor`)
  - Defensive Stand (`army_defence_factor`, `max_planning`)
  - War Fatigue & Stability (`stability_factor`, `war_support_factor`, `political_power_cost`)
  - Fuel Rationing (`army_fuel_consumption_factor`, `navy_fuel_consumption_factor`)
