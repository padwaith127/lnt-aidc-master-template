# Title: NFPA Standards for Data Centre Fire, Life Safety & BESS
## Purpose: To define the National Fire Protection Association (NFPA) requirements for electrical safety, IT equipment protection, and battery energy storage.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #NFPA #FireSafety #ElectricalSafety #BESS #NFPA70E #NFPA855 #LTVyoma
## Related Files: [[BIS.md]], [[Battery_Energy_Storage.md]], [[Detection_and_Suppression.md]]
## Standards Covered: NFPA 70, NFPA 70E, NFPA 75, NFPA 76, NFPA 855, NFPA 110

---

## 1. Overview
In a 40 MW AI-ready facility, the concentration of energy (BESS) and the value of equipment (NVIDIA GPUs) make fire and life safety paramount. While Indian NBC 2016 provides the baseline, global hyperscalers (Microsoft, Meta, Google) mandate **NFPA** compliance. These standards go beyond basic fire-fighting into technical "Fire Prevention" and "Safe Working Practices" for high-voltage environments.

## 2. Core NFPA Standards for the Mahape Project

### 2.1 NFPA 70 (National Electrical Code - NEC)
*   **Significance:** The global benchmark for safe electrical design.
*   **Article 645:** Specifically addresses Information Technology Equipment. It governs the requirements for disconnects (EPO), wiring under raised floors, and cabling in air plenums.

### 2.2 NFPA 70E: Standard for Electrical Safety in the Workplace
*   **Significance:** Mandatory for L&T Operational Safety. It defines how to perform "Live Work" and determines the **Arc Flash PPE** requirements.
*   **Mahape Application:** Every panel in the 40 MW site must have an NFPA 70E-compliant label indicating the Boundary and Incident Energy.

### 2.3 NFPA 75: Standard for Fire Protection of IT Equipment
*   **Significance:** Defines the construction of the "Data Hall." 
*   **Key Requirement:** Requires non-combustible materials and specialized smoke detection (VESDA) for high-airflow environments.

### 2.4 NFPA 855: Standard for the Installation of Stationary Energy Storage Systems
*   **Significance:** The "Bible" for Lithium-ion Battery (BESS) safety.
*   **AI Context:** Since Mahape uses high-density Li-ion banks, NFPA 855 dictates the spacing (3 ft / 914mm) between battery cabinets and the requirement for **Explosion Deflagration Venting**.

### 2.5 NFPA 110: Standard for Emergency and Standby Power Systems
*   **Significance:** Governs the installation and maintenance of Diesel Generators (DGs).
*   **Classification:** For Data Centres, we typically design to **Level 1** (where failure could lead to loss of life or serious injury—interpreted as "Critical Mission Loss").

## 3. Engineering Application: AI-Ready Fire Mitigation
1.  **Aspirating Smoke Detection (VESDA):** Per NFPA 76, high-airflow AI zones must use air-sampling detection because traditional spot detectors are ineffective in the "Wind Tunnel" effect of high-density cooling.
2.  **EPO (Emergency Power Off):** NFPA 70 Art 645 requires an EPO at the exit doors. For hyperscale, L&T often implements "Selective EPO" to prevent a minor incident from dropping all 40 MW.

## 4. NFPA vs. Indian Standards (NBC 2016)
| Feature | NFPA (Global) | NBC 2016 (Indian) |
| :--- | :--- | :--- |
| **BESS Safety** | Highly Detailed (NFPA 855) | General Guidelines |
| **Arc Flash** | Mandatory Analysis (70E) | Not explicitly detailed |
| **IT Fire** | Specialized (NFPA 75) | Part of Building Fire Code |

## 5. Design Checklist (NFPA Compliance)
- [ ] Is the BESS room layout compliant with NFPA 855 spacing?
- [ ] Are all cables in air plenums (above ceiling/below floor) Plenum-rated or in metal conduit?
- [ ] Has an Arc Flash study been completed to define PPE per NFPA 70E?
- [ ] Does the FACP (Fire Alarm Control Panel) support cross-zoning for gas release?
- [ ] Is the EPO button protected against accidental activation?

---

## 6. References
### Standards
* **NFPA 70 (2023):** National Electrical Code.
* **NFPA 855 (2023):** Standard for Energy Storage Systems.
* **NFPA 70E (2024):** Standard for Electrical Safety.

### Revision History
* 1.0: Mapped NFPA requirements for L&T Vyoma Mahape project.