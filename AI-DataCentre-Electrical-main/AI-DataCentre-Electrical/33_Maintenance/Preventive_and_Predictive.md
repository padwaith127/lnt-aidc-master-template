# Title: Preventive & Predictive Maintenance for Critical Power Systems
## Purpose: To define the technical maintenance lifecycle and condition-monitoring strategies for a 40 MW AI-ready facility to ensure near-zero unplanned downtime.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #Maintenance #PreventiveMaintenance #PredictiveMaintenance #NFPA70B #Thermography #PartialDischarge #LTVyoma
## Related Files: [[Standard_Operating_Procedures.md]], [[Failure_Analysis.md]], [[UPS_System_Design.md]], [[Transformer_Design.md]]
## Standards Covered: NFPA 70B (2023), IEEE 3007.2, IS 10028, NETA ATS/MTS, ISO 55001

---

## 1. Overview
In a 40 MW facility like Mahape, the cost of an outage is measured in millions of dollars per hour. Traditional "Run-to-Failure" or even simple "Time-Based" maintenance is inadequate. For the L&T Vyoma project, we implement an **NFPA 70B-compliant** maintenance program that balances **Preventive Maintenance (PM)** with **Predictive Maintenance (PdM)** using real-time data from the SCADA/EPMS.

## 2. Maintenance Strategies

| Strategy | Methodology | Application in 40MW DC |
| :--- | :--- | :--- |
| **Preventive (PM)** | Scheduled, time-based tasks (e.g., Annual, Quarterly). | Filter changes, physical cleaning, bolt tightening. |
| **Predictive (PdM)** | Condition-based monitoring using sensors. | Oil analysis, Partial Discharge (PD), IR thermography. |
| **Corrective** | Reactive repair after a fault or anomaly. | Replacing a faulty breaker trip unit found during PM. |

## 3. Maintenance Schedule for Critical Assets

### 3.1 Transformers (HT Yard & Distribution)
*   **Quarterly:** Visual inspection for oil leaks/cracks in bushings; silica gel color check.
*   **Annual:** Dissolved Gas Analysis (DGA) for oil-filled units; Insulation Resistance (IR) test.
*   **PdM:** Permanent **Fiber Optic Temperature Sensors** in windings to detect hotspots during AI surges.

### 3.2 HT & LT Switchgear
*   **Annual:** Contact Resistance (Ductor) test; Vacuum integrity check for VCBs.
*   **PdM:** **Online Partial Discharge (PD) Monitoring** (especially for Mahape's humid coastal environment) to detect insulation tracking before a flashover.
*   **Cleaning:** Use specialized non-conductive vacuums to remove industrial dust (common in Mahape MIDC).

### 3.3 UPS & Battery Systems (BESS)
*   **Monthly:** Visual check of Lithium-ion cabinets; BMS alarm log review.
*   **Semi-Annual:** Battery Impedance/Internal Resistance testing (for any VRLA units) or SoC/SoH validation (for Li-ion).
*   **Annual:** UPS Capacitor Bank health check (ripple current analysis).

### 3.4 Diesel Generators (DGs)
*   **Weekly:** No-load test run (5-10 mins).
*   **Monthly:** Load bank test at 30% load (minimum) to prevent "Wet Stacking."
*   **Annual:** Full "Black Start" test and fuel polishing to remove Mumbai moisture/sediment.

## 4. Engineering Calculations: Reliability & MTBF

To justify the maintenance budget, we calculate the **Mean Time Between Failures (MTBF)**.
*   **Formula:** $MTBF = \frac{\text{Total Operating Time}}{\text{Number of Failures}}$
*   **Availability ($A$):** $A = \frac{MTBF}{MTBF + MTTR}$
    *   *MTTR:* Mean Time To Repair.
*   **Design Goal:** For a Tier III facility, we target $A = 99.982\%$. Effective maintenance reduces $MTTR$ and increases $MTBF$.

## 5. Specialized AI-Ready PdM Techniques

### 5.1 Infrared (IR) Thermography
*   **Why:** AI clusters run at 100% load for long durations.
*   **Method:** Perform IR scans of all Busduct joints and PDU breakers while the AI workload is at its **Peak TDP**.
*   **Criteria:** Any joint $> 10^\circ \text{C}$ above ambient or neighboring phases requires immediate re-torquing.

### 5.2 Power Quality Analysis (EPMS Driven)
*   Monitor **THDi** trends. If harmonics increase, it indicates the AI power shelves are aging or the UPS filters are degrading.

### 5.3 Acoustic Monitoring
*   Using ultrasonic sensors to listen for "arcing" or "hissing" in HT switchgear which is inaudible to humans.

## 6. Safety & Human Factors
*   **NETA Standards:** Use NETA-certified technicians for high-voltage testing.
*   **PPE:** Maintenance on energized equipment is prohibited unless absolutely necessary. If required, follow the **Arc Flash Labels** generated in Module 21.
*   **Lock-Out Tag-Out (LOTO):** Verify the "Dead" condition using a Proximity Voltage Detector before touching any terminal.

## 7. Spares Management (The "Critical Spares" List)
For the 40 MW Mahape site, L&T must stock:
1.  **ACBs/VCBs:** 1 spare of each frame size (3200A, 4000A).
2.  **Protection Relays:** Pre-configured with the project settings.
3.  **UPS Power Modules:** 5% of total module count.
4.  **Fuses & Lugs:** Comprehensive assortment of high-speed semiconductor fuses.
5.  **Liquid Cooling Spares:** CDU pump seals and control boards.

## 8. Commissioning to Maintenance Handover
The transition from L&T Construction to L&T Operations must include:
*   The **"Golden SLD"**: Final As-Built drawing.
*   **Baseline Data:** All IR/Vibration/PD readings taken during Level 5 Commissioning to serve as the "Normal" reference.

## 9. Failure Modes in Maintenance
*   **Over-Maintenance:** Increasing risk by frequently opening/closing breakers and introducing human error.
*   **Loose Connections:** Failure to use a calibrated torque wrench after cleaning.
*   **Inadequate Cleaning:** Dust on heat sinks causing UPS thermal shutdown under AI load.

---

## 10. Maintenance Checklist (Annual Shutdown/Swing)
- [ ] Visual inspection of all HT Yard insulators for salt buildup?
- [ ] Oil DGA results reviewed for all transformers?
- [ ] All Busway joints IR-scanned under full AI load?
- [ ] Relay secondary injection testing completed?
- [ ] UPS battery discharge test results within 5% of factory baseline?

---
## 11. References
### Standards
* **NFPA 70B (2023):** Standard for Electrical Equipment Maintenance (Now Mandatory).
* **IEEE 3007.2:** Recommended Practice for the Maintenance of Industrial and Commercial Power Systems.
* **NETA MTS:** Maintenance Testing Specifications for Electrical Power Distribution Equipment.

### Manufacturer Documents
* **Cummins:** "Generator Set Preventive Maintenance Guide."
* **Schneider Electric:** "Maintenance Strategies for Data Centers White Paper."
* **NVIDIA:** "Best Practices for Maintaining Liquid Cooled GPU Infrastructure."

### Revision History
* 1.0: Initial Maintenance Framework for L&T Vyoma Mahape project.

---
**Next File Recommendation:** `34_Failure_Analysis/Root_Cause_Methodology.md` (Defining how to investigate an outage using forensic engineering).