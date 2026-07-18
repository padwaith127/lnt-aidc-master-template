# Title: Project Overview - {{cookiecutter.it_capacity_mw}} MW AI-Ready Hyperscale DC
## Purpose: To define the technical scope and strategic objectives of the {{cookiecutter.project_name}}.
## Tags: #ProjectOverview #{{cookiecutter.it_capacity_mw}}MW #{{cookiecutter.city}} #{{cookiecutter.ai_silicon_vendor}}
## Standards Covered: Uptime Tier III, TIA-942-C

---

## 1. Project Introduction
The {{cookiecutter.project_name}} project at {{cookiecutter.city}}, {{cookiecutter.state}}, is a state-of-the-art {{cookiecutter.it_capacity_mw}} MW IT-load hyperscale data centre. Unlike traditional enterprise data centres, this facility is designed "AI-first," meaning it is engineered to support the extreme power densities and thermal requirements of {{cookiecutter.ai_silicon_vendor}} high-performance computing clusters.

## 2. Key Technical Specifications
* **Total IT Power:** {{cookiecutter.it_capacity_mw}} MW.
* **Location:** {{cookiecutter.city}}, {{cookiecutter.state}}.
* **Power Density:** 
    * Standard Network/Storage Zones: 10-15 kW/rack.
    * AI Compute Zones: 60 kW to 120+ kW/rack (Direct-to-Chip Liquid Cooled).
* **Redundancy:** Uptime Tier III (Concurrent Maintainability).
* **Incoming Utility:** {{cookiecutter.utility_voltage_kv}} kV (Dedicated Substation via {{cookiecutter.utility_provider}}).
* **Power Usage Effectiveness (PUE) Target:** < {{cookiecutter.target_pue}} (Annualized).

## 3. The AI Shift: Legacy vs. AI-Ready
The "AI-Ready" label changes three primary electrical domains fundamentally:
1.  **Step Loads:** AI training runs create massive, instantaneous swings in power demand. The power train (UPS/DG) must respond without voltage collapse.
2.  **Harmonics:** High-density SMPS in GPU servers increase THD-i (Total Harmonic Distortion - Current). 200% Neutral sizing is mandatory.
3.  **Cooling Integration:** The transition from Air-Cooled (Fans/Chillers) to Liquid-Cooled (CDUs/Pumps) shifts the motor-load profile, requiring critical cooling pumps to be placed on the UPS bus.

## 4. Engineering Workflow for {{cookiecutter.project_name}}
The design follows a sequential "Outside-In" approach:
1.  **Utility Interface:** Securing {{ (cookiecutter.it_capacity_mw | float * cookiecutter.target_pue | float / 0.95) | round(2) }} MVA capacity from {{cookiecutter.utility_provider}}.
2.  **HT Yard:** {{cookiecutter.utility_voltage_kv}} kV Substation design per local statutory safety norms.
3.  **Transformation:** {{cookiecutter.utility_voltage_kv}} kV to LV (415V/480V) transformation using K-rated transformers.
4.  **Backup:** N+1 or 2N Diesel Generator sets with continuous DCC ratings and 24-48 hour fuel autonomy.
5.  **Conditioning:** Double-conversion UPS systems paired with Lithium-ion Battery Energy Storage (BESS).
6.  **Distribution:** High-ampacity (4000A-6000A) sandwich busducts replacing traditional cabling to handle the massive current density.

## 5. Design Checklist (Initial Phase)
- [ ] Confirm Utility Fault Level and X/R ratio at the {{cookiecutter.utility_provider}} Substation.
- [ ] Define the exact IT / Mechanical / Electrical Load Split.
- [ ] Establish Redundancy Topology (e.g., Block Redundant vs. 2N).
- [ ] Assess Site Seismic Zone for {{cookiecutter.city}} to determine Switchgear structural mounting.
