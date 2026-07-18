# Title: Project Overview - 40 MW AI-Ready Hyperscale DC
## Purpose: To define the technical scope and strategic objectives of the Mahape Data Centre project.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #ProjectOverview #40MW #Mahape #LTVyoma #NVIDIA
## Related Files: [[Design_Basis_Report.md]], [[Client_Requirements.md]]
## Standards Covered: Uptime Tier III, TIA-942-C, CEA 2023

---

## 1. Project Introduction
The L&T Vyoma project at Mahape, Navi Mumbai, is a state-of-the-art 40 MW IT-load hyperscale data centre. Unlike traditional enterprise data centres, this facility is designed "AI-first," meaning it is engineered to support the extreme power densities and thermal requirements of NVIDIA GPU clusters (H100, B200, and Blackwell architectures).

## 2. Key Technical Specifications
* **Total IT Power:** 40 MW.
* **Location:** Mahape, Navi Mumbai (Coastal/Humid Environment).
* **Power Density:** 
    * Standard Zones: 10-15 kW/rack.
    * AI Zones: 40 kW to 120 kW/rack (Liquid Cooled).
* **Redundancy:** Uptime Tier III (Concurrent Maintainability).
* **Incoming Utility:** 33kV or 110kV (Dedicated Substation).
* **Power Usage Effectiveness (PUE) Target:** < 1.4 (Annualized).

## 3. The AI Shift: Legacy vs. AI-Ready
As a Senior Engineer at L&T, you must understand that the "AI-Ready" label changes three primary electrical domains:
1.  **Step Loads:** AI training runs create massive, instantaneous swings in power demand.
2.  **Harmonics:** High-density SMPS in GPU servers increase THD-I (Total Harmonic Distortion - Current).
3.  **Cooling Integration:** Transition from Air-Cooled (Fans/Chillers) to Liquid-Cooled (CDUs/Pumps) shifts the motor-load profile.

## 4. Engineering Workflow for Mahape
The design follows a sequential "Outside-In" approach:
1.  **Utility Interface:** Securing 40MW+ capacity from MSEDCL/Tata Power.
2.  **HT Yard:** 33kV/110kV Substation design per CEA norms.
3.  **Transformation:** 33kV/415V or 11kV/415V transformation.
4.  **Backup:** N+1 or 2N Diesel Generator sets with 24-48 hour fuel autonomy.
5.  **Conditioning:** UPS systems with Lithium-ion Battery Energy Storage (BESS).
6.  **Distribution:** Busduct-heavy distribution to handle high currents (4000A-6000A).

## 5. Design Checklist (Initial Phase)
- [ ] Confirm Utility Fault Level at Mahape Substation.
- [ ] Define IT/Mechanical/Electrical Load Split.
- [ ] Establish Redundancy Topology (e.g., Block Redundant vs. 2N).
- [ ] Assess Site Seismic Zone (Zone III for Mumbai) for Switchgear mounting.

---
## 📚 References
### Standards
* **Uptime Institute:** Tier Standard: Topology.
* **CEA 2023:** Measures relating to Safety and Electric Supply.

### Manufacturer Documents
* **NVIDIA:** "Data Center Infrastructure Readiness for AI."

### Revision History
* 1.0: Initial Project Definition.