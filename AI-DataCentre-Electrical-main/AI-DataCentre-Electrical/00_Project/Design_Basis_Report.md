# Title: Design Basis Report (DBR) - Electrical Systems
## Purpose: To establish the fundamental design parameters, assumptions, and criteria for the {{cookiecutter.it_capacity_mw}} MW AI-Ready Data Centre.
## Project: {{cookiecutter.project_name}}
## Revision: 2.0 (Parametric AI Master)
## Tags: #DBR #DesignCriteria #Hyperscale #AI-Ready #{{cookiecutter.ai_silicon_vendor}}
## Standards Covered: Uptime Tier III, TIA-942-C, IEEE 3001.2, Local Grid Codes

---

## 1. Introduction
The Design Basis Report (DBR) is the "Source of Truth" for the project. For the {{cookiecutter.project_name}} {{cookiecutter.it_capacity_mw}} MW facility, this document ensures that the electrical infrastructure can support the high-density transient loads of {{cookiecutter.ai_silicon_vendor}} AI clusters while maintaining the strict uptime requirements of a hyperscale facility.

## 2. Site Environmental Conditions ({{cookiecutter.city}}, {{cookiecutter.state}})
Design parameters must account for the specific environmental and atmospheric conditions of {{cookiecutter.city}}.

| Parameter | Value | Reference |
| :--- | :--- | :--- |
| **Max Ambient Temperature** | {{cookiecutter.max_ambient_temp}}°C | ASHRAE / Local Meteorological Data |
| **Design Ambient for Equipment** | {{cookiecutter.max_ambient_temp | int + 5}}°C (De-rating factor applied) | Manufacturer Standard (IEC/IEEE) |
| **Relative Humidity** | Site Specific (Up to 95% peak) | Local Data |
| **Seismic Zone** | Site Specific | IS 1893 / IBC / Local Code |
| **Atmospheric Conditions** | Subject to local industrial/coastal pollutants | Requires appropriate IP/NEMA enclosures |

## 3. Power Requirements & Topology
### 3.1 Utility Connection
*   **Incoming Voltage:** {{cookiecutter.utility_voltage_kv}} kV (Dual Source from {{cookiecutter.utility_provider}}).
*   **Ultimate IT Load:** {{cookiecutter.it_capacity_mw}} MW.
*   **Total Facility Apparent Power:** ~{{ (cookiecutter.it_capacity_mw | float * cookiecutter.target_pue | float / 0.95) | round(2) }} MVA (including cooling and losses).

### 3.2 Redundancy Architecture
*   **System Topology:** Distributed Redundant (N+1) or 2N (System+System).
*   **Tier Rating:** Uptime Tier III (Concurrent Maintainability) or TIA-942 Rated-3. 
*   **Logic:** Any component (Transformer, UPS, Switchgear) can be removed from service for maintenance without impacting the IT load.

## 4. Electrical Design Criteria

| Parameter | Standard Value | Tolerance/Notes |
| :--- | :--- | :--- |
| **System Frequency** | 50 Hz / 60 Hz | Local Grid Standard |
| **HT Voltage** | {{cookiecutter.utility_voltage_kv}} kV | +/- 10% |
| **LT Voltage** | 415 V / 480 V | +/- 6% |
| **Voltage Harmonic Distortion (THD-v)** | < 3% | IEEE 519 / Local Grid Code |
| **Current Harmonic Distortion (THD-i)** | < 5% | At Point of Common Coupling (PCC) |
| **Power Factor** | 0.99 (Leading/Lagging) | At UPS Output |
| **Fault Level (HT)** | TBD by Utility Study | Subject to {{cookiecutter.utility_provider}} data |
| **Fault Level (LT)** | {{cookiecutter.fault_level_ka}} kA | 1 Second Duration |

## 5. AI-Specific Design Considerations (The "{{cookiecutter.ai_silicon_vendor}} Footprint")
Standard DBRs fail at AI densities. This project incorporates:
1.  **High-Density Zones:** Support for 60kW to 120kW+ per rack for liquid-cooled clusters.
2.  **Step Load Handling:** UPS and Generators must handle 0% to 100% load steps common during {{cookiecutter.ai_silicon_vendor}} model "Check-pointing" and "Training Start."
3.  **Liquid Cooling Power:** Dedicated, UPS-backed power feeds for Coolant Distribution Units (CDUs) with N+1 redundancy.
4.  **Busbar Distribution:** Overhead busway (4000A+) to replace traditional cabling for high-density AI rack rows.

## 6. Equipment Selection Basis
### 6.1 Transformers
*   **Type:** Cast Resin Dry Type (for indoor) or Oil-filled (for HT Yard).
*   **Vector Group:** Dyn11 (or local equivalent).
*   **K-Factor:** K-13 minimum (to handle non-linear AI loads).

### 6.2 UPS System
*   **Technology:** Double Conversion Online (VFI).
*   **Storage:** Lithium-ion Battery Energy Storage Systems (BESS) - LFP Chemistry preferred.
*   **Autonomy:** 5-10 minutes at full load (optimized for Generator start-up).

### 6.3 Backup Power (Generators)
*   **Fuel:** Diesel / HVO (Hydrotreated Vegetable Oil).
*   **Rating:** Data Centre Continuous (DCC) rating per ISO 8528.
*   **Synchronization:** < 15 seconds to full load pickup.

## 7. Design Calculations Workflow
To validate this DBR, the following studies must be performed using ETAP/SKM:
1.  **Load Flow Study:** To ensure transformer/cable sizing and voltage stability under AI step-loads.
2.  **Short Circuit Study:** To define switchgear breaking capacity ({{cookiecutter.fault_level_ka}} kA).
3.  **Relay Coordination:** To ensure localized, selective tripping.
4.  **Arc Flash Analysis:** To define PPE requirements (Note: IEEE 1584 limited to 15kV; use ARCPRO for {{cookiecutter.utility_voltage_kv}}kV).

---

## 8. Design Checklist
- [ ] Utility "Sanctioned Load" letter received from {{cookiecutter.utility_provider}}?
- [ ] Is the PUE target (<{{cookiecutter.target_pue}}) achievable with the current cooling electrical load?
- [ ] Are the HT and LT rooms located above the 100-year flood level for {{cookiecutter.city}}?
- [ ] Does the earthing design meet both safety codes and IEEE 1100 (Electronic Grounding / SRG) for AI networking?

---
## 📚 References
### Standards
* **IEEE 3001.2:** Recommended Practice for Evaluating the Reliability of Industrial and Commercial Power Systems.
* **TIA-942-C:** Telecommunications Infrastructure Standard for Data Centers.
* **Local Codes:** Statutory regulations governing electrical safety in {{cookiecutter.state}}.
