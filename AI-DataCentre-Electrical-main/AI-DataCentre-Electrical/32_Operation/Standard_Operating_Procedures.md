# Title: Standard Operating Procedures (SOP) & Operational Excellence
## Purpose: To define the operational framework, procedures (SOP/EOP/MOP), and human-factor management for the electrical infrastructure of a 40 MW AI-ready facility.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #Operations #SOP #EOP #MOP #DataCentreOps #LTVyoma #UptimeStandard
## Related Files: [[Commissioning_Testing.md]], [[Maintenance.md]], [[Failure_Analysis.md]], [[SCADA.md]]
## Standards Covered: Uptime Institute Operational Sustainability, ISO 27001, NFPA 70E, IEEE 3007.3

---

## 1. Overview
In a 40 MW AI-ready facility, the "Design" and "Construction" phases (where L&T is currently focused) represent only a fraction of the facility's life. The **Operations** phase is where the 99.999% availability is won or lost. For the Mahape project, we must transition from an engineering mindset to an operational one, where **Human Error** (the cause of >70% of DC outages) is mitigated through rigorous documentation: SOPs, EOPs, and MOPs.

## 2. The Operational Document Hierarchy

| Document Type | Meaning | Application |
| :--- | :--- | :--- |
| **SOP** | Standard Operating Procedure | Routine, low-risk tasks (e.g., Daily inspections, logging). |
| **MOP** | Method of Procedure | High-risk scripts for specific maintenance (e.g., Transferring UPS to Bypass). |
| **EOP** | Emergency Operating Procedure | "Battle Drills" for unplanned events (e.g., Utility failure, Fire, Leak). |

## 3. Standard Operating Procedures (SOP) - Routine
Routine operations ensure the "Health" of the 40 MW site is visible.
1.  **Daily Shift Rounds:** Physical inspection of the HT Yard, Transformer noise levels, UPS battery room temperatures, and CDU (Coolant Distribution Unit) pressures.
2.  **Logbook Management:** Hourly recording of kWh, PUE, and Phase Balance at the 33kV and LT Incomer levels.
3.  **Fuel Management:** Weekly testing of diesel quality (for Mumbai humidity) and fuel level verification.

## 4. Method of Procedure (MOP) - High-Risk Execution
A MOP is a step-by-step "Flight Plan" that must be peer-reviewed and signed before execution.
*   **Sample MOP Workflow (Transferring a 1.5 MW UPS to Maintenance Bypass):**
    1.  Verify the secondary source is synchronized (Check Sync Bus).
    2.  Transfer UPS to Internal Static Bypass via HMI.
    3.  Close External Maintenance Bypass Breaker (MBB).
    4.  Open UPS Output Breaker (UOB).
    5.  Open UPS Input Breaker (UIB).
    6.  **Verify Zero Voltage** at the UPS terminals before technician entry.

## 5. Emergency Operating Procedures (EOP) - Critical AI Response
When a 40 MW AI cluster experiences a power disturbance, the EOP must be instinctual.
1.  **Total Utility Outage (EOP-01):** Verify Auto-Start of all 20+ DG sets. If one fails to start, initiate manual sync.
2.  **CDU Pump Failure (EOP-02):** Manual override of the secondary cooling loop to ensure GPU cold-plate flow is maintained.
3.  **Fire in Electrical Room (EOP-03):** Gas suppression deployment and selective isolation of the affected power block.

## 6. AI-Ready Operational Considerations
1.  **NVIDIA "Training Day" Coordination:** When an AI model begins training, the IT load can jump from 5 MW to 40 MW in seconds. Operations must coordinate with the client to ensure the **Cooling Plant** is in "Pre-compute" mode (ramped up) before the power spike.
2.  **Transient Monitoring:** Operators must use the EPMS (Module 25) to review transient events after every AI "Training Run" to identify potential weak points in the distribution (e.g., loose busbar joints).
3.  **Liquid Cooling Chemistry:** Part of electrical operations includes monitoring the **Coolant Conductivity**. If conductivity rises, it indicates potential ion buildup, which increases the risk of an electrical short if a leak occurs.

## 7. Safety: NFPA 70E & LOTO
*   **Lock-Out Tag-Out (LOTO):** Mandatory for every maintenance task in the Mahape facility. L&T site engineers must be trained "Authorized Persons."
*   **Arc Flash Boundaries:** Operators must never enter the "Prohibited Space" of 33kV switchgear without the correct Category 4 PPE, as defined in the **Arc Flash Study** (Module 21).

## 8. Training & Drills (The "Human Element")
*   **Tabletop Exercises:** Monthly walk-throughs of EOPs with the shift team.
*   **Simulation Drills:** Quarterly "Failure Injection" tests (non-load-impacting) to ensure the team knows how to react to a DG failure or a cooling leak.

## 9. Failure Modes in Operations
*   **Procedural Deviation:** A technician "thinks" they know the step and skips the MOP. *Result:* Dropped IT load.
*   **Alarm Fatigue:** Ignoring a "Low Battery Voltage" alarm for months until the grid fails. *Mitigation:* Daily "Active Alarm" audit.
*   **Poor Handover:** Shift A doesn't tell Shift B about a bypassed protection relay.

---

## 10. Operational Checklist (Daily)
- [ ] Are all UPS systems in "Normal Mode" (Not on Bypass)?
- [ ] Is the PUE within the target range (<1.4)?
- [ ] Are the battery room temperatures between 20°C and 25°C?
- [ ] Has the fuel system been checked for leaks or water contamination?
- [ ] Are all SCADA/BMS workstations functional and showing "Live" data?

---
## 11. References
### Standards
* **Uptime Institute:** Operational Sustainability Standard (Gold/Silver/Bronze).
* **ISO 27001:** Information Security (includes physical facility security/operations).
* **NFPA 70E:** Standard for Electrical Safety in the Workplace.
* **IEEE 3007.3:** Recommended Practice for Electrical Power System Operations and Maintenance.

### Research/White Papers
* **Uptime Institute:** "Annual Outage Analysis - The Role of Human Error."
* **Schneider Electric WP #110:** "Standardized Procedures for Data Center Operations."

### Revision History
* 1.0: Initial Operational Strategy for L&T Vyoma Mahape project.

---
**Next File Recommendation:** `33_Maintenance/Preventive_and_Predictive.md` (Focusing on the technical maintenance of HT/LT gear, Transformers, and DGs).