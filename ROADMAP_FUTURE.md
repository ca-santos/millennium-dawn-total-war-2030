# Total War 2030 — Future Expansion Roadmap (ROADMAP_FUTURE.md)

This document organizes proposed future features for **Total War 2030** into a 4-Era chronological escalation narrative starting in **2014**, transitioning seamlessly from early regional friction to full 2030 Total War.

---

# SECTION I — REGIONAL FRICTION & HYBRID FLASHOVER (2014–2019)

## Phase 8 — Early Hybrid Conflicts & Regional Pivots (2014–2016)
- [ ] **`tw2030_early_conflict.1` — Crimea & Eastern European Hybrid Pivot (2014+)**:
  - *Locations*: Crimea, Donbass (Ukraine - UKR), Kaliningrad, Belarus (BLR).
  - *Effect*: Border militarization, economic sanctions, and +0.05 threat generation between NATO and Russia.
- [ ] **`tw2030_early_conflict.2` — South China Sea Island Reclamation (2015+)**:
  - *Locations*: Spratly & Paracel Islands (China - CHI, Philippines - PHI, Vietnam - VIE, USA).
  - *Effect*: Artificial island militarization, naval freedom-of-navigation patrols, +10% naval strike efficiency.
- [ ] **`tw2030_early_conflict.3` — Middle East Proxy Surge & Counter-Terrorism (2014+)**:
  - *Locations*: Syria (SYR), Iraq (IRQ), Yemen (YEM).
  - *Effect*: Coalition air strikes, PMC operations, and regional instability modifiers.
- [ ] **`tw2030_early_generic.1` — Regional Border Skirmish & Tensions (Generic)**:
  - *Target Scope*: Randomly selects neighboring nations with low opinion (`opinion < -10`).
  - *Effect*: Border tension event increasing army training speed and generating minor threat (+0.5%).

## Phase 9 — Regional Proxy Warfare & PMC Infiltration (2017–2019)
- [ ] **`tw2030_pmc.1` — Sahel Private Military Conflict**:
  - *Locations*: Mali (MLI), Niger (NGR), Burkina Faso (BFA).
  - *Effect*: Covert PMC infiltration events sparking low-intensity proxy warfare without formal war declarations.
- [ ] **`tw2030_pmc.2` — Donbass & Suwalki Border Proxy Standoff**:
  - *Locations*: Suwalki Gap (Poland - POL / Lithuania - LIT), Belarus (BLR), Eastern Ukraine (UKR).
  - *Effect*: Irregular unit skirmishes and border mobilization events.
- [ ] **`tw2030_pmc.3` — Surrogate Arms Supply & Global Escalator**:
  - *Mechanic*: Decision chain allowing USA, SOV, CHI, and NATO to supply heavy weapons to proxy factions, advancing global threat.
- [ ] **`tw2030_pmc_generic.1` — Paramilitary Infiltration & Instability (Generic)**:
  - *Target Scope*: Random minor nation with low stability (`stability < 0.45`).
  - *Effect*: Infiltration event generating minor insurgent raids, sabotage, or stability reduction (-5%).

---

# SECTION II — HYBRID WARFARE & RESOURCE FRICTION (2020–2024)

## Phase 10 — Cyber Warfare & Infrastructure Disruption (2020–2022)
- [ ] **`tw2030_cyber.1` — Power Grid Blackouts**:
  - *Targets*: North American Interconnection (USA), Central European Grid (GER, FRA, POL), East Asian Grids (CHI, JAP, TAI).
  - *Effect*: -15% Factory Efficiency and -10% Construction Speed for 180 days.
- [ ] **`tw2030_cyber.2` — Financial System & Banking Disruption**:
  - *Targets*: Financial hubs in New York (USA), London (ENG), Frankfurt (GER), Tokyo (JAP), Shanghai (CHI).
  - *Effect*: +15% Consumer Goods Factor and -0.20 Political Power gain.
- [ ] **`tw2030_cyber.3` — Air Traffic Control & Logistics Jamming**:
  - *Targets*: Logistics hubs at Ramstein (GER), Okinawa (JAP), Diego Garcia.
  - *Effect*: -25% Supply Throughput and -10% Air Superiority Efficiency.
- [ ] **`tw2030_cyber_generic.1` — Regional Infrastructure Cyber Attack (Generic)**:
  - *Target Scope*: Randomly targets any nation with `internet_station > 0`.
  - *Effect*: Short-term temporary loss of stability (-5%) or consumer goods penalty (+5%).

## Phase 11 — Strategic Resource Friction & Economic Warfare (2023–2024)
- [ ] **`tw2030_resource.1` — Lithium Triangle Mining Friction**:
  - *Locations*: Salar de Uyuni (Bolivia - BOL), Jujuy/Salta (Argentina - ARG), Atacama (Chile - CHL).
  - *Effect*: Diplomatic pressure events forcing South American nations to choose economic alignment between USA and China.
- [ ] **`tw2030_resource.2` — Central African Cobalt & Rare Earth Standoff**:
  - *Locations*: Katanga Region (DR Congo - DRC) and Copperbelt (Zambia - ZAM).
  - *Effect*: Resource extraction friction events causing supply shortages for advanced military electronics.
- [ ] **`tw2030_resource.3` — Taiwan TSMC Microchip Supply Bottleneck**:
  - *Location*: Hsinchu Science Park (Taiwan - TAI).
  - *Effect*: Trade embargoes and export controls halting 5th-gen fighter (F-35, J-20) and modern MBT production.
- [ ] **`tw2030_resource_generic.1` — Strategic Resource Market Volatility (Generic)**:
  - *Target Scope*: Randomly selects any nation producing key strategic resources (oil, rubber, aluminum, steel, tungsten, chromium).
  - *Effect*: Temporary export reduction or trade efficiency penalty (+10% resource market cost).

---

# SECTION III — PRE-WAR ESCALATION & A2/AD DEPLOYMENT (2025–2029)

## Phase 12 — Maritime Chokepoints & Island Fortifications (2025–2027)
- [ ] **`tw2030_maritime.1` — Strait of Malacca & Sunda Passage Blockade**:
  - *Locations*: Maritime chokepoints between Singapore (SIN), Malaysia (MAY), Indonesia (INS).
  - *Effect*: Interdiction events threatening East Asian crude oil import routes, causing +20% naval fuel consumption.
- [ ] **`tw2030_maritime.2` — Bab-el-Mandeb & Red Sea Shipping Risk**:
  - *Locations*: Horn of Africa coast (Djibouti - DJI, Eritrea - ERI, Yemen - YEM).
  - *Effect*: Naval convoy escort requirements along the Suez Canal maritime corridor.
- [ ] **`tw2030_maritime.3` — Pacific & Baltic Strategic Island Rearmament**:
  - *Locations*: Spratly & Paracel Islands (South China Sea), Guam (USA), Diego Garcia (ENG), Gotland (Sweden - SWE).
  - *Effect*: AI construction logic for airbases (`air_base`), naval bases (`naval_base`), and coastal radars.
- [ ] **`tw2030_maritime_generic.1` — Coastal Trade Route Insecurity (Generic)**:
  - *Target Scope*: Random coastal country with `is_coastal = yes`.
  - *Effect*: Temporary convoy efficiency malus (-10%) or increased naval patrol requirement.

## Phase 13 — Space Control & Missile Defense Networks (2028–2029)
- [ ] **`tw2030_space.1` — Anti-Satellite (ASAT) Reconnaissance Strike**:
  - *Target*: GPS, Beidou, and GLONASS military satellite constellations.
  - *Effect*: -20% Max Planning Speed and -15% Guided Missile Accuracy for USA, CHI, and SOV.
- [ ] **`tw2030_space.2` — Metropolitan ABM & SAM Shield Deployment**:
  - *Locations*: Moscow (SOV), Beijing (CHI), Washington D.C. (USA), Berlin (GER), Tokyo (JAP).
  - *Effect*: AI prioritized construction of SAM sites (`anti_air_building`) and Radars (`radar_station`) to intercept incoming missile salves.
- [ ] **`tw2030_space.3` — Integrated Maritime A2/AD Bubbles**:
  - *Locations*: Kaliningrad (SOV), Crimea (SOV), Hainan Island (CHI), Okinawa (JAP).
  - *Effect*: Anti-Ship Cruise Missile (ASCM) coastal fortification modifiers giving +25% naval strike efficiency.
- [ ] **`tw2030_space_generic.1` — Regional Air Defense Alert (Generic)**:
  - *Target Scope*: Random secondary or regional power (`num_of_factories > 15`).
  - *Effect*: Grants temporary construction speed bonus (+15%) for `anti_air_building` and `radar_station`.

---

# SECTION IV — TOTAL WAR ERA & DYNAMIC STATE ENGINE (2030+)

## Phase 14 — Tag-Free State-Driven Dynamic Modifier Engine

### 1. Emergency Industrial Restructuring & Efficiency
- [ ] **`tw2030_generic.1` — Emergency Industrial Conversion**:
  - *Trigger*: `ai_is_threatened = yes` or `has_war = yes` with low military factory count.
  - *Modifiers*: `conversion_cost_civ_to_mil_factor = -0.35`, `industrial_capacity_factory = +0.10`, `consumer_goods_factor = +0.03`.
- [ ] **`tw2030_generic.2` — Assembly Line Efficiency Bottleneck**:
  - *Trigger*: Prolonged war with critical equipment surplus ratio deficit (`equipment_stockpile_surplus_ratio < -0.25`).
  - *Modifiers*: `production_factory_efficiency_gain_factor = -0.20`, `line_change_production_efficiency_factor = -0.15`.

### 2. Military Posture, Recruitment & Defensive Standoff
- [ ] **`tw2030_generic.3` — Accelerated Recruitment Surge**:
  - *Trigger*: Wargoal justification or active war preparation (`is_justifying_wargoal_against = yes`).
  - *Modifiers*: `training_time_army_factor = -0.25`, `conscription_factor = +0.10`, `army_fuel_consumption_factor = +0.10`.
- [ ] **`tw2030_generic.4` — Fortification & Defensive Stand**:
  - *Trigger*: Neighboring hostile nation with 1.5x larger army strength (`strength_ratio > 1.5` & `is_neighbor_of`).
  - *Modifiers*: `army_defence_factor = +0.10`, `max_planning = +0.20`, `land_reinforce_rate = +0.05`.

### 3. Internal Stability & War Support Dynamics
- [ ] **`tw2030_generic.5` — Popular Discontent & War Fatigue**:
  - *Trigger*: Conflict duration > 365 days with low stability (`stability < 0.35`).
  - *Modifiers*: `stability_factor = -0.10`, `war_support_factor = -0.15`, `political_power_cost = +0.30`.
- [ ] **`tw2030_generic.6` — Pro-War Euphoria & Unification**:
  - *Trigger*: Defending core territory against a larger aggressor with high stability (`stability > 0.70`).
  - *Modifiers*: `war_support_factor = +0.20`, `army_morale_factor = +0.15`, `political_power_gain = +0.25`.

### 4. Logistics, Supply & Fuel Rationing
- [ ] **`tw2030_generic.7` — Strategic Fuel Rationing**:
  - *Trigger*: Active naval or air fleet with low fuel ratio (`fuel_ratio < 0.20`).
  - *Modifiers*: `army_fuel_consumption_factor = -0.25`, `navy_fuel_consumption_factor = -0.25`, `air_superiority_efficiency_factor = -0.20`.
- [ ] **`tw2030_generic.8` — Logistics Overload & Supply Attrition**:
  - *Trigger*: Overextended supply lines or saturated logistics network.
  - *Modifiers*: `supply_consumption_factor = +0.20`, `attrition = +0.10`.
