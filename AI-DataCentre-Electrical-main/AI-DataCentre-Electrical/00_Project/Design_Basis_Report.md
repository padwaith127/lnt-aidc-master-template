# Title: Design Basis Report (DBR) - Electrical Systems
## Purpose: To establish the fundamental design parameters, assumptions, and criteria for the 40 MW AI-Ready Data Centre.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #DBR #DesignCriteria #Hyperscale #AI-Ready #LTVyoma
## Related Files: [[Project_Overview.md]], [[Load_Calculation.md]], [[NVIDIA_Architecture.md]]
## Standards Covered: Uptime Tier III, TIA-942-C, IEEE 3001.2, CEA 2023, NBC 2016

---

## 1. Introduction
The Design Basis Report (DBR) is the "Source of Truth" for the project. For the L&T Vyoma 40 MW facility, this document ensures that the electrical infrastructure can support the high-density transient loads of NVIDIA GPU clusters while maintaining the strict uptime requirements of a hyperscale facility.

## 2. Site Environmental Conditions (Mahape, Navi Mumbai)
Design parameters must account for the coastal, humid, and industrial environment of Navi Mumbai.

| Parameter | Value | Reference |
| :--- | :--- | :--- |
| **Max Ambient Temperature** | 45°C | ASHRAE / Local Data |
| **Design Ambient for Equipment** | 50°C (De-rating factor applied) | Manufacturer Standard |
| **Relative Humidity** | 90% (Peak) | Local Data |
| **Seismic Zone** | Zone III | IS 1893 |
| **Atmospheric Conditions** | Saline & Industrial Pollutants | Coastal Proximity |

## 3. Power Requirements & Topology
### 3.1 Utility Connection
*   **Incoming Voltage:** 33kV or 110kV (Dual Source from MSEDCL/Tata Power).
*   **Ultimate IT Load:** 40 MW.
*   **Total Facility Apparent Power:** ~55-60 MVA (including cooling and losses).

### 3.2 Redundancy Architecture
*   **System Topology:** Distributed Redundant (N+1) or 2N (System+System).
*   **Tier Rating:** Uptime Tier III (Concurrent Maintainability). 
*   **Logic:** Any component (Transformer, UPS, Switchgear) can be removed from service for maintenance without impacting the IT load.

## 4. Electrical Design Criteria

| Parameter | Standard Value | Tolerance/Notes |
| :--- | :--- | :--- |
| **System Frequency** | 50 Hz | +/- 3% (CEA) |
| **HT Voltage** | 33,000 V | +/- 10% |
| **LT Voltage** | 415 V / 240 V | +/- 6% |
| **Voltage Harmonic Distortion (THD-v)** | < 3% | IEEE 519 / CEA |
| **Current Harmonic Distortion (THD-i)** | < 5% | At Point of Common Coupling |
| **Power Factor** | 0.99 (Leading/Lagging) | At UPS Output |
| **Fault Level (HT)** | 25 kA or 40 kA | TBD by Utility Study |
| **Fault Level (LT)** | 50 kA / 65 kA | 1 Second Duration |

## 5. AI-Specific Design Considerations (The "NVIDIA Footprint")
Standard DBRs fail at AI densities. This project incorporates:
1.  **High-Density Zones:** Support for 60kW to 120kW per rack.
2.  **Step Load Handling:** UPS and Generators must handle 0% to 100% load steps common during AI model "Check-pointing" and "Training Start."
3.  **Liquid Cooling Power:** Dedicated power feeds for Coolant Distribution Units (CDUs) with N+1 redundancy.
4.  **Busbar Distribution:** Overhead busway (4000A+) to replace traditional cabling for rack rows.

## 6. Equipment Selection Basis
### 6.1 Transformers
*   **Type:** Cast Resin Dry Type (for indoor) or Oil-filled (for HT Yard).
*   **Vector Group:** Dyn11.
*   **K-Factor:** K-13 minimum (to handle non-linear AI loads).

### 6.2 UPS System
*   **Technology:** Double Conversion Online.
*   **Storage:** Lithium-ion Battery Energy Storage Systems (BESS).
*   **Autonomy:** 5-10 minutes at full load (optimized for DG start-up).

### 6.3 Backup Power (Generators)
*   **Fuel:** Diesel (HSD).
*   **Rating:** Data Centre Continuous (DCC) rating per ISO 8528.
*   **Synchronization:** < 15 seconds to full load.

## 7. Design Calculations Workflow
To validate this DBR, the following studies must be performed (Module 20-23):
1.  **Load Flow Study:** To ensure transformer/cable sizing.
2.  **Short Circuit Study:** To define switchgear breaking capacity.
3.  **Relay Coordination:** To ensure localized tripping.
4.  **Arc Flash Analysis:** To define PPE requirements.

---

## 8. Design Checklist
- [ ] Utility "Sanctioned Load" letter received?
- [ ] Is the PUE target (<1.4) achievable with the current cooling electrical load?
- [ ] Are the HT and LT rooms located above the 100-year flood level for Navi Mumbai?
- [ ] Does the earthing design meet both IS 3043 and IEEE 1100 (Electronic Grounding)?

---
## 📚 References
### Standards
* **IEEE 3001.2:** Recommended Practice for Evaluating the Reliability of Industrial and Commercial Power Systems.
* **TIA-942-C:** Telecommunications Infrastructure Standard for Data Centers.
* **CEA 2023:** Measures relating to Safety and Electric Supply.

### Research Papers
* **Schneider Electric WP #513:** "AI Impact on Data Center Design."
* **Uptime Institute:** "Tier Standard: Topology."

### Revision History
* 1.0: Initial Release for L&T Vyoma Mahape Project.