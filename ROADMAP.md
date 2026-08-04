# Total War 2030 — Phased Development Roadmap

This document outlines the step-by-step development roadmap for the **Total War 2030** submod. Each phase builds modularly on previous work, allowing for discrete testing and validation.

---

## Phase 1 — Research & Architectural Foundations [COMPLETED]
- [x] Audit Millennium Dawn AI production, limiter, and threat logic (`MD_combat_ai_strategies.txt`, `MD_econ_ai.txt`, `00_AI_scripted_effects.txt`).
- [x] Identify factors causing MD AI passivity (peacetime unit limiters, civ factory priority, low wargoal generation, high `avoid_starting_wars` weight, routine equipment dumping).
- [x] Establish submod directory structure under `/total-war-2030-submod`.
- [x] Author comprehensive Design Document (`DESIGN.md`).

---

## Phase 2 — Core Engine Hooks & Escalation Triggers [COMPLETED / IN PROGRESS]
- [x] Create custom script triggers for escalation eras: `tw2030_is_era_1`, `tw2030_is_era_2`, `tw2030_is_era_3`, `tw2030_is_era_4`.
- [x] Implement monthly on_action pulse (`tw2030_on_monthly_pulse`) in `common/on_actions/tw2030_on_actions.txt`.
- [x] Implement era transition global flags and progressive threat generation.
- [x] Wire dynamic escalation notifications via `events/tw2030_escalation_events.txt`.

---

## Phase 3 — Strategic AI Production & Equipment Overrides [COMPLETED / IN PROGRESS]
- [x] Add dynamic AI strategies (`common/ai_strategy/tw2030_ai_strategies.txt`) for military industry investment (MIC/NIC).
- [x] Scale role ratios for ground forces (MBTs, IFVs, Mechanized), air forces (Air Superiority, Strike CAS), and navies (Carriers, Destroyers, Submarines) as eras advance.
- [x] Implement equipment production priority overrides (`common/ai_equipment/tw2030_ai_equipment.txt`).
- [x] Implement weapon dump suppression so rearming powers stockpile infantry weapons, missiles, and armored chassis.

---

## Phase 4 — Dynamic Readiness & Economic Posture [COMPLETED / IN PROGRESS]
- [x] Define escalating readiness dynamic modifiers (`tw2030_state_of_readiness_1` through `4`).
- [x] Apply defense budget scaling and factory conversion speed bonuses as global threat rises.
- [x] Integrate bankruptcy safety guards to prevent AI financial collapse during rearmament.

---

## Phase 5 — Power-Specific Geopolitical Alignment & Behaviors [COMPLETED]
- [x] Implement major-power specific escalation profiles for USA, China (CHI), Russia (SOV), NATO members, and India (RAJ).
- [x] Configure strategic rivalries (`ai_strategy = { type = conquer / declare_war }`) for major friction points.
- [x] Add reactive rearmament triggers if player engages in early rapid expansion.

---

## Phase 6 — Regional Flashpoints & Dynamic Events [COMPLETED]
- [x] Implement flashpoint crisis chain: Taiwan Strait Escalation, Eastern European Border Crisis, Middle East Conflict Expansion, Korean Peninsula Rearmament.
- [x] Integrate strategic resource friction (Microchip shortages, Rare earths competition, Oil embargoes).
- [x] Fix native sub missile coastal strikes (`sub_missile_raids.txt`) to require war / promised retaliation before AI launching raids on peaceful nations.

---

## Phase 7 — Comprehensive Balance, Performance & Release Package [FUTURE]
- [ ] Perform long-term automated hands-off testing (spectator runs 2000–2035) to verify performance and balance.
- [ ] Validate standard unit limits under potato and standard game rules.
- [ ] Package final release build for steam workshop and community distribution.
