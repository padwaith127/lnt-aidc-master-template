# Title: Master Index & Repository Navigation Map
## Purpose: To provide a centralized navigation hub for the complete 40 MW AI-Ready Data Centre Electrical Engineering Knowledge Base.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #Index #Navigation #EngineeringWiki #LTVyoma #DataCentreDesign
## Related Files: All Repository Files
## Standards Covered: ISO 9001 (Documentation Control), TIA-942-C

---

## 1. Overview
This repository is designed as a **Modular Engineering Handbook**. It follows the logical lifecycle of the **L&T Vyoma Mahape 40 MW Project**, moving from global standards and utility interface down to the micro-details of NVIDIA Blackwell GPU power shelves. 

Use this map to navigate the cross-linked Markdown files.

---

## 2. The Repository Core (Phase 1: Foundations)

### 00_Project: The Mission Profile
*   [[Project_Overview.md]] — The 40 MW Mahape Scope.
*   [[Design_Basis_Report.md]] — Technical "Laws" of the project.
*   [[Client_Requirements.md]] — NVIDIA & Hyperscale SLAs.

### 01_Standards: Regulatory Compliance
*   [[CEA.md]] — Indian Statutory Safety (2023 Regs).
*   [[BIS.md]] — IS 3043, IS 732, and Indian Codes.
*   [[IEEE.md]] — Global Power Engineering Standards.
*   [[IEC.md]] — Switchgear and Transformer Codes.
*   [[Uptime.md]] — Tier III/IV Topology & Sustainability.
*   [[ASHRAE.md]] — Thermal Envelopes (TC 9.9).

---

## 3. The Power Train (Phase 2: Infrastructure Design)

### 02_Load_Calculation to 06_Transformers
*   [[AI_Load_Estimation.md]] — Sizing for 40 MW + Cooling.
*   [[Utility_Interface.md]] — 33kV/110kV Grid Connectivity.
*   [[HT_Switchgear.md]] — GIS and VCB Specifications.
*   [[Transformer_Design.md]] — K-Factor and Cast Resin Units.

### 07_DG_System to 11_Switchgear
*   [[Backup_Generation.md]] — DCC-Rated 3.25MVA units.
*   [[UPS_System_Design.md]] — Double Conversion & AI Step-loads.
*   [[Battery_Energy_Storage.md]] — Lithium-ion (LFP/NMC) BESS.
*   [[Static_Transfer_Switches.md]] — Path Redundancy (<4ms).
*   [[LV_Switchgear.md]] — Form 4b PCCs and ATS Logic.

---

## 4. Power Distribution (Phase 3: The White Space)

### 12_Busduct to 15_Rack_Power
*   [[Busbar_Distribution.md]] — Sandwich & Track Busway.
*   [[Power_Distribution_Units.md]] — Floor-mount PDU Sizing.
*   [[Remote_Power_Panels.md]] — Network & Mgmt Power.
*   [[Rack_Level_Distribution.md]] — 120kW NVIDIA Power Shelves.

---

## 5. Technical Studies & Safety (Phase 4: Engineering Analysis)

### 16_Cable_Design to 23_Power_Quality
*   [[Sizing_and_Routing.md]] — XLPE De-rating and Trays.
*   [[Grounding_Grid_Design.md]] — IEEE 80 and Signal Reference Grid.
*   [[Lightning_Protection_Systems.md]] — IS/IEC 62305 Risk Levels.
*   [[Relay_Coordination_and_Selectivity.md]] — TCC Curves & Selectivity.
*   [[System_Stability_Analysis.md]] — Load Flow and Step-loads.
*   [[Fault_Level_Calculations.md]] — 50kA/65kA Withstand.
*   [[Harmonics_Mitigation.md]] — THDi and AHF Sizing.
*   [[Transient_and_Sag_Analysis.md]] — ITIC/CBEMA Compliance.

---

## 6. Systems Integration (Phase 5: Automation & Environment)

### 24_SCADA to 30_Lighting
*   [[Supervisory_Control.md]] — PLC Logic & IEC 61850.
*   [[Power_Monitoring_System.md]] — Energy Analytics & PUE.
*   [[BMS_Integration.md]] — Thermal-Electrical Interlock.
*   [[HVAC_Power_Integration.md]] — Motor Control & VFDs.
*   [[CDU_and_Pump_Electrical.md]] — Liquid Cooling Critical Power.
*   [[Detection_and_Suppression.md]] — Gas Release & VESDA.
*   [[Emergency_and_General_Lighting.md]] — Lux Levels & Egress.

---

## 7. Lifecycle & Intelligence (Phase 6: O&M and AI)

### 31_Commissioning to 37_NVIDIA_Architecture
*   [[Level_1_to_Level_5_Testing.md]] — FAT to IST.
*   [[Standard_Operating_Procedures.md]] — MOPs and EOPs.
*   [[Preventive_and_Predictive.md]] — Thermal/PD Monitoring.
*   [[Root_Cause_Methodology.md]] — Forensic Investigations.
*   [[Hyperscale_Outage_Lessons.md]] — Global Case Studies.
*   [[High_Density_Thermal_Management.md]] — 120kW Thermal Sync.
*   [[GPU_Infrastructure_Requirements.md]] — NVIDIA Blackwell Specs.

---

## 8. Documentation & Reference (Phase 7: The Engineer's Library)

### 38_Drawings to 44_Reference_Index
*   [[Standard_Drawing_Templates.md]] — SLDs and 3D BIM.
*   [[Bill_of_Quantities_Preparation.md]] — Specifications & BOQ.
*   [[Master_Formula_Reference.md]] — Technical "Cheat Sheet."
*   [[Annotated_Bibliography.md]] — The "Must-Read" Research.
*   [[Terminology_Index.md]] — The Industry Glossary.

---

## 9. How to Maintain this Repository
1.  **Updates:** When NVIDIA releases a new "Gold Site Survey" for the next GPU architecture (e.g., Rubin/R100), update [[NVIDIA_Architecture.md]].
2.  **Versioning:** Always log changes in the `Revision History` table at the end of each file.
3.  **Local Context:** For future L&T projects outside Mumbai, update the `Environmental Conditions` in [[Design_Basis_Report.md]].

---

## 10. Final Sign-Off
This repository constitutes the full set of industry-standard documents required to design, review, and execute a modern 40 MW AI-ready facility. 

**Consultant Status:** *Knowledge Base Generation Complete.*

---
### Revision History
* 1.0: Initial Master Index Release for L&T Vyoma Mahape project.