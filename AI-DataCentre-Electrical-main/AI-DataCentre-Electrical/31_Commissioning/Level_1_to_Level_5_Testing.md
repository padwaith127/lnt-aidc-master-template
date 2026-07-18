# Title: Data Centre Commissioning - Level 1 to Level 5 (IST)
## Purpose: To define the 5-level commissioning process required to validate the electrical and mechanical integrity of a {{ cookiecutter.it_capacity_mw }} MW AI-ready facility.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #Commissioning #Cx #IST #Level5Testing #LoadBank #{{ cookiecutter.project_code }} #UptimeStandard
## Related Files: [[Design_Basis_Report.md]], [[Standard_Operating_Procedures.md]], [[Fault_Level_Calculations.md]], [[System_Stability_Analysis.md]]
## Standards Covered: ASHRAE Standard 202, ASHRAE Guideline 0, ACG Commissioning Guideline, Uptime Institute Operational Sustainability

---

## 1. Overview
In a {{ cookiecutter.it_capacity_mw }} MW AI-ready facility, commissioning (Cx) is the process of proving that the "As-Built" facility performs exactly as intended in the "Design Basis." For the {{ cookiecutter.project_name }} {{ cookiecutter.city }} project, this is the most critical phase before handing over the keys to the end-user. We follow the industry-standard **5-Level Commissioning Model** to systematically mitigate risk from the factory to the full-load Integrated Systems Test (IST).

## 2. The 5 Levels of Commissioning

| Level | Name | Description | Stakeholders |
| :--- | :--- | :--- | :--- |
| **Level 1** | **FAT (Factory Acceptance)** | Witnessing equipment testing at the manufacturer’s plant. | Design Team, Vendor |
| **Level 2** | **Site Receipt / QAQC** | Inspection of equipment upon arrival; verification of no transit damage. | Site PM, QA Team |
| **Level 3** | **Pre-Functional / PFT** | Energization of individual components; "Cold" and "Static" checks. | Electrical Contractor |
| **Level 4** | **Functional / FPT** | System-level testing (e.g., UPS running on Battery, DG Sync). | Commissioning Agent (CxA) |
| **Level 5** | **IST (Integrated Systems)** | "Pull the Plug" test; Full facility stress test under simulated load. | All Teams / Client |

## 3. Level 1: Factory Acceptance Testing (FAT)
Before the transformers or UPS units leave the factory:
*   **Checklist:** Verify winding resistance, insulation class, and primary/secondary injection.
*   **AI Requirement:** For UPS units, witness the **Step Load Response** (0% to 100%) to ensure it matches the {{ cookiecutter.ai_silicon_vendor }} transient requirements.

## 4. Level 4: Functional Performance Testing (FPT)
Testing the "interaction" of components within a single system.
*   **DG System:** 24-hour load bank test for each generator at 100% load.
*   **UPS System:** Battery discharge test at full design load until the "Low Battery" cutoff.
*   **ATS/MTM:** Verify the automatic transfer logic works without manual intervention.

## 5. Level 5: Integrated Systems Test (IST) - The "Pull the Plug"
This is the final exam. We simulate {{ cookiecutter.it_capacity_mw }} MW of IT load using **Server Simulators (Load Banks)** placed inside the racks.

### 5.1 Test Scenarios for {{ cookiecutter.city }} {{ cookiecutter.it_capacity_mw }}MW
1.  **Total Utility Failure:** Simulating a grid blackout. Verify all DGs start and take the load in < 15s.
2.  **Redundancy Failure:** While on load, trip one "A-Feed" UPS. Verify the "B-Feed" continues to power the AI racks without interruption.
3.  **Cooling Failure:** Trip the primary pumps. Verify the secondary/backup pumps start immediately and liquid flow to the GPUs is maintained.
4.  **The "Black Start":** Starting the entire {{ cookiecutter.it_capacity_mw }} MW facility from a completely de-energized state using only the DGs.

## 6. AI-Ready Specialized Commissioning
1.  **Thermal Imaging (IR):** During the 100% load IST, perform an IR scan of every busbar joint, cable termination, and PDU breaker. AI loads are continuous; hot spots will appear only after 4-8 hours of sustained load.
2.  **Transient Power Analysis:** Use high-speed power quality analyzers to record the voltage dip when the {{ cookiecutter.it_capacity_mw }} MW load is transferred from Utility to DG.
3.  **Liquid Cooling Stress Test:** Verify the CDU (Coolant Distribution Unit) flow rates at peak IT load. Ensure the "Secondary Loop" pressure stays within {{ cookiecutter.ai_silicon_vendor }} specifications during pump transitions.

## 7. Engineering Calculations: Load Bank Sizing
To simulate {{ cookiecutter.it_capacity_mw }} MW, you need to coordinate the load bank delivery.
*   **Formula:** $N_{loadbanks} = \frac{P_{total}}{P_{unit}}$
*   **Calculation:** If using 100kW portable load banks for {{ cookiecutter.it_capacity_mw }} MW:
    $$N = \frac{ {{ (cookiecutter.it_capacity_mw | float * 1000) | round(0) }} }{100} = {{ (cookiecutter.it_capacity_mw | float * 10) | round(0) }} \text{ units.}$$
*   **Strategy:** Use rack-mounted "Server Simulators" (3kW to 7kW each) for precise thermal testing in the aisles.

## 8. Documentation & Handover
The Cx process is not complete until the **Final Commissioning Report** is signed off.
*   **As-Built Drawings:** Updated with every red-line made during Level 3 and 4.
*   **Relay Settings:** Final "As-Commissioned" settings file from the protection study.
*   **Training:** Minimum 40 hours of operator training for the {{ cookiecutter.project_name }} O&M team.

## 9. Failure Modes during Commissioning
*   **Nuisance Tripping:** Often caused by incorrect protection settings not accounting for actual load bank inrush.
*   **Phase Rotation Mismatch:** Discovered at Level 3. *Correction:* Swap two phases at the source.
*   **Communication Lag:** BMS/SCADA points not updating fast enough during an IST. *Mitigation:* Optimize the polling rates of Modbus/BACnet gateways.

---

## 10. Commissioning Checklist (Level 5)
- [ ] Load banks installed and balanced across phases?
- [ ] Thermal cameras calibrated and operators briefed?
- [ ] Fuel tanks filled to 100% for the 24-hour burn?
- [ ] "Safety Officers" stationed at every HT/LT room with radios?
- [ ] "Scenario Script" reviewed and signed by engineering and client representatives?

---
## 11. References
### Standards
* **ASHRAE Standard 202:** Commissioning Process for Buildings and Systems.
* **ASHRAE Guideline 0:** The Commissioning Process.
* **ACG:** AABC Commissioning Group - Commissioning Guideline.

### Manufacturer Documents
* **Schneider Electric:** "Commissioning Services for Data Centers White Paper."
* **Vertiv:** "Standard for Testing and Commissioning High Availability Power Systems."

### Revision History
* 1.0: Initial Commissioning Framework for {{ cookiecutter.project_name }} {{ cookiecutter.city }} project.

---
**Next File Recommendation:** `Standard_Operating_Procedures.md` (Defining the day-to-day electrical management of the {{ cookiecutter.it_capacity_mw }} MW facility).
