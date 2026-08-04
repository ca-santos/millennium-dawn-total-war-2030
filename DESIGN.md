# Total War 2030 — Submod Design Document

## 1. Executive Summary & Vision

**Total War 2030** is an overhaul submod for **Millennium Dawn: Modern Day Mod** (Hearts of Iron IV). Its purpose is to transform Millennium Dawn’s geopolitical sandbox from a predominantly peaceful economic simulator into a world experiencing credible, escalating geopolitical friction that culminates in **global conventional war around the year 2030**.

Millennium Dawn offers an unprecedented level of depth regarding 21st-century politics, economic development, debt mechanics, and modern military tech trees. However, standard MD gameplay often suffers from passive AI behavior: major powers maintain peacetime economic focus for decades, stockpile minimal equipment, build limited military factories, and rarely initiate large-scale peer-to-peer conventional warfare.

**Total War 2030** solves this passivity. The submod does **not** force a single railroaded outcome (such as a scripted scripted World War 3 event on January 1st, 2030). Instead, it implements dynamic AI strategic profiles, dynamic threat mechanics, evolving readiness modifiers, and escalating military production priorities that naturally push the global power structure into an intense arms race and eventual high-intensity global war.

---

## 2. Design Philosophy

### 2.1 Dynamic Escalation vs. Hardcoded Railroading
- **Preserve Sandbox Agency**: Players must retain complete freedom to alter history, form alternative alliances, de-escalate crises, or trigger early wars.
- **Systemic Incentive Structures**: Rather than using forced wargoal events, escalation is driven by scriptable AI strategy shifts, threat modifiers, economic re-tooling, and alliance friction.
- **Believable Geopolitical Timeline**: Escalation follows a 4-phase timeline (2000–2014 Stability, 2015–2024 Friction, 2025–2029 Pre-War Mobilization, 2030+ Total War Era).

### 2.2 Realistic & Non-Cheating AI Enhancements
- **No Artificial Free Troops**: Avoid spawning magical armies or giving free infinite equipment unless explicitly tied to wartime mobilization mechanics.
- **Smart Resource Allocation**: Instruct the AI to prioritize Military Industry (MIC) and Naval Industry (NIC) as global tension rises, transition unit limiters, stockpile infantry weapons/missiles/armored vehicles, and upgrade division templates.
- **Financial Stability**: Maintain Millennium Dawn’s bankruptcy guards so rearming AI nations do not collapse into financial insolvency before war breaks out.

---

## 3. Escalation Timeline & Mechanics

The submod divides the timeline into four organic operational eras:

```
+-----------------------------------------------------------------------------------+
| ERA 1: Stability & Modernization (2000 - 2014)                                    |
| - Economic growth, counter-terrorism, regional focus                              |
| - Peacetime military limiters, low MIC investment                                 |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
| ERA 2: Geopolitical Friction (2015 - 2024)                                        |
| - Regional proxy wars, rising threat, initial remilitarization                    |
| - MIC build score boosted (+35), equipment dumping reduced                        |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
| ERA 3: Strategic Arms Race & Mobilization (2025 - 2029)                            |
| - Great power polarization, high defense budgets, naval/air expansion            |
| - Division limiters expanded x1.4, aggressive wargoal weighting active            |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
| ERA 4: Total War Era (2030+)                                                      |
| - High world tension, peak military readiness, global conventional war focus      |
| - Full military industrial mobilization, aggressive conflict AI                   |
+-----------------------------------------------------------------------------------+
```

### Era Breakdown & Technical Triggers
1. **Era 1 (2000–2014)**:
   - Global Tension: Low (0%–15%).
   - AI Behavior: Standard MD economic development (Offices, Civs, Infrastructure).
   - Flag: `tw2030_era_1_active`.

2. **Era 2 (2015–2024)**:
   - Global Tension: Moderate (15%–35%).
   - Trigger: Date >= 2015.1.1.
   - AI Behavior: Major powers begin military modernization; MIC investment weight increased; equipment dumping thresholds doubled.
   - Dynamic Modifier: `tw2030_escalation_phase_1`.

3. **Era 3 (2025–2029)**:
   - Global Tension: High (35%–65%).
   - Trigger: Date >= 2025.1.1 or World Threat > 40%.
   - AI Behavior: Pre-war mobilization. Division, air, and ship limiters scaled up by 40%. AI increases production of armored chassis, IFVs, SAMs, and multirole air superiority fighters.
   - Dynamic Modifier: `tw2030_escalation_phase_2`.

4. **Era 4 (2030+)**:
   - Global Tension: Critical (65%–100%).
   - Trigger: Date >= 2030.1.1 or World Threat > 60%.
   - AI Behavior: Total War Readiness posture (`tw2030_state_of_readiness_4`). Wargoal generation constraints lifted for revisionist powers; military production consumes max available industrial capacity.

---

## 4. Gameplay Objectives

- **Encourage Arms Races**: Major powers (USA, China, Russia, NATO, India) monitor rival army/navy sizes and reactively increase defense budgets.
- **Naval Expansion**: Great naval powers build balanced carrier strike groups, missile frigates/destroyers, and attack submarines.
- **Air Superiority & SAM Integration**: AI active investment in airbases, SAM networks, radar coverage, and 5th-gen fighter production.
- **Missile & Counter-Missile Development**: Increased AI prioritization of strategic and tactical missile stockpiles.
- **Resource Competition**: Heightened AI interest in securing critical strategic materials (microchips, composite materials, fuel reserves).

---

## 5. AI Strategy & Production Architecture

### 5.1 Industrial Re-tooling & Investment Weights
In standard MD (`MD_econ_ai.txt`), AI spending heavily favors civilian factories (base score 170) and offices (base score 180). **Total War 2030** injects dynamic AI strategy modifiers in `common/ai_strategy/tw2030_ai_strategies.txt`:
- **MIC Investment Boost**: As threat increases, `building_target = arms_factory` receives +40 to +120 weight.
- **NIC Investment Boost**: Maritime powers receive +30 to +80 weight for `building_target = dockyard`.
- **Infrastructure & Airbase Priority**: Defensive SAM sites and airbases receive elevated construction priority during Era 3 and Era 4.

### 5.2 Stockpile & Weapon Dump Management
In standard MD (`99_weapon_dump_effects.txt`), peacetime AI routinely dumps excess infantry weapons (>150k), tanks (>2.5k), and artillery (>5k) for cash.
- **Submod Override**: Under `tw2030_escalation_phase_1` and beyond, the dump thresholds are quadrupled or disabled for major powers, allowing them to accumulate massive wartime reserves of small arms, APCs, MBTs, and artillery.

### 5.3 Force Build & Unit Limiters
- **Division Limiters**: Standard MD calculates `division_limiter_limit` daily. Submod applies positive situational multipliers (+25% in Era 2, +50% in Era 3, +100% in Era 4).
- **Force Build Armies**: Great powers receive `force_build_armies` weighting adjustments up to +150 in Era 3/4.

---

## 6. Military & Economic Balance Philosophy

- **Bankruptcy Guarding**: All submod military spending and focus/decision triggers check MD's bankruptcy condition (`NOT = { has_active_mission = bankruptcy_incoming_collapse }`).
- **Dynamic Readiness Modifiers**: Nation-level dynamic modifiers give escalating defense throughput, training speed, and factory conversion speed while maintaining realistic resource costs.
- **Balanced Template Design**: AI division templates maintain proper front-width, air defense, anti-tank capability, and logistics support.

---

## 7. Submod File Structure

```text
/total-war-2030-submod
├── descriptor.mod
├── total-war-2030.mod
├── DESIGN.md
├── ROADMAP.md
├── common/
│   ├── ai_equipment/
│   │   └── tw2030_ai_equipment.txt
│   ├── ai_strategy/
│   │   └── tw2030_ai_strategies.txt
│   ├── dynamic_modifiers/
│   │   └── tw2030_dynamic_modifiers.txt
│   ├── ideas/
│   │   └── tw2030_ideas.txt
│   ├── on_actions/
│   │   └── tw2030_on_actions.txt
│   ├── scripted_effects/
│   │   └── tw2030_scripted_effects.txt
│   └── scripted_triggers/
│       └── tw2030_scripted_triggers.txt
├── events/
│   └── tw2030_escalation_events.txt
└── localisation/
    └── english/
        └── total_war_2030_l_english.yml
```

---

## 8. Risks & Mitigation Strategies

| Risk Factor | Potential Impact | Mitigation Strategy |
|---|---|---|
| End-game Performance Degradation | Micro-stutter due to unit spam | Enforce tuned upper bounds in `division_limiter` math; scale equipment requirements for larger divisions rather than pure division count. |
| AI Early Bankruptcy | Rearming AI collapses economically before 2030 | Integrate tax desire checks and bankruptcy guards into all custom AI mobilization effects. |
| Suicidal AI Declarations | Minor nations attacking majors prematurely | Gate aggressive `conquer` and `declare_war` strategy weights behind power ratios and faction support checks. |
| Player Exploits | Player rushing AI before 2030 | Grant major AI nations reactive emergency mobilization triggers if player starts aggressive conquests early. |

---

## 9. Future Expansion Ideas

1. **Flashpoint Crisis System**: Dynamic regional crisis events (Taiwan Strait, Suwalki Gap, Kashmir, Strait of Hormuz) that elevate world threat.
2. **Resource Embargo & Sanctions Mechanics**: AI economic warfare prior to military conflict.
3. **Space Control & Cyber Escalation**: Integrated cyber-attack waves leading up to kinetic war.
