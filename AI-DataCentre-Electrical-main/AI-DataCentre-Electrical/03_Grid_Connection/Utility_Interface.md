# Title: Utility Interface & Grid Connection (HT Incoming)
## Purpose: To define the engineering requirements for connecting a 55 MVA facility to the local electrical grid in Mahape, Navi Mumbai.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #GridConnection #UtilityInterface #HT-Yard #MSEDCL #TataPower #33kV #110kV
## Related Files: [[CEA.md]], [[Substation_Design.md]], [[Protection_Relay.md]]
## Standards Covered: CEA 2023, IEEE 1547, CBIP Publication 311, IS 2026, IEC 62271

---

## 1. Overview
For the L&T Vyoma 40 MW project, the utility interface is the most critical single point of failure. At 55-60 MVA total demand, the connection is typically made at **33kV (Multiple Circuits)** or **110kV/132kV (Dedicated Substation)** depending on the availability of the Mahape/MSEDCL/Tata Power infrastructure. This file covers the transition from the Utility Point of Common Coupling (PCC) to the Data Centre HT Yard.

## 2. Grid Connection Options (Mahape Context)
Based on Maharashtra State Electricity Distribution Co. Ltd (MSEDCL) and MERC guidelines:

| Voltage Level | Capacity Limit | Infrastructure Required | Redundancy |
| :--- | :--- | :--- | :--- |
| **33 kV** | Up to 15-20 MVA per ckt | Overhead/Underground Cables | N+1 Circuits required |
| **110/132 kV** | 50 MVA + | AIS/GIS Substation on-site | Preferred for 40MW IT Load |

*Decision for Mahape:* 110kV GIS (Gas Insulated Substation) is the hyperscale standard to minimize footprint in land-expensive Mumbai and ensure high reliability.

## 3. Technical Requirements at PCC (Point of Common Coupling)

### 3.1 Power Quality Limits (IEEE 519 / CEA)
As a large consumer, the DC must not pollute the grid.
*   **Voltage THD:** < 3%.
*   **Current THD:** < 5%.
*   **Voltage Unbalance:** < 1%.

### 3.2 Short Circuit Levels
*   **Design Basis:** Assume a 3-Phase symmetrical fault level of **25kA or 31.5kA for 3 seconds** at 33kV/110kV.
*   **Action:** All HT breakers (SF6 or Vacuum) must be rated to interrupt this fault level.

## 4. Engineering Workflow for Grid Integration

### Step 1: Load Sanction & Feasibility Study
*   Submit the **A-Form** to MSEDCL/Tata Power.
*   Conduct a **Load Flow & Grid Stability Study** to ensure the 40MW step-loads don't cause a voltage dip on the utility's 110kV bus.

### Step 2: HT Yard / Substation Design
*   **Type:** Outdoor AIS (Air Insulated) or Indoor GIS (Gas Insulated).
*   **Components:** 
    1.  **Lightning Arrestors (LA):** Station Class, Gapless ZnO type.
    2.  **Isolators:** With Earth Switch (Motorized for remote SCADA operation).
    3.  **Instrument Transformers:** CTs (Accuracy Class 0.2s for metering) and PTs.
    4.  **HT Metering:** Check Meter and Standby Meter as per CEA Metering Regulations.

### Step 3: Protection & Coordination
*   **Main Protection:** Differential Protection (87T) and Distance Protection (21).
*   **Backup:** Overcurrent (50/51) and Earth Fault (50N/51N).
*   **Inter-tripping:** A dedicated fiber optic link (OPGW/Underground) between the DC and the Utility Substation for "Transfer Trip" signals.

## 5. Drawings Required
1.  **Key Single Line Diagram (KSLD):** Shows the connectivity from the Utility Gantry to the Main HT Breakers.
2.  **Substation Layout:** Physical placement of gantries, insulators, and transformers.
3.  **Earthing Grid Layout:** IEEE 80-compliant mesh design for the HT Yard.
4.  **Protection SLD:** Detailed relay logic and CT/PT core allocations.

## 6. AI-Ready Infrastructure Considerations
*   **Fast Transient Recovery:** High-density AI training causes massive load fluctuations. The utility transformer tap changers (OLTC) must be high-speed or stabilized via the UPS to prevent "Utility Flicker" complaints from neighbors in Mahape.
*   **Renewable Energy (Open Access):** Most hyperscalers (Google/Meta) require green power. The utility interface must support **Open Access** billing to credit solar/wind energy generated off-site.

## 7. Construction & Commissioning Sequence
1.  **Civil Foundation:** Casting of Transformer pads and GIS room.
2.  **Equipment Erection:** Installation of Breakers and CT/PTs.
3.  **Cable Termination:** Stress-cone terminations for HT XLPE cables.
4.  **Pre-commissioning Tests:**
    *   Insulation Resistance (Megger).
    *   Contact Resistance (Ductor test).
    *   Hi-Pot Test (Power frequency voltage withstand).
    *   CT/PT Ratio and Polarity.
5.  **Final Inspection:** CEIG (Chief Electrical Inspector) site visit.

## 8. Failure Modes & Risks
*   **Insulation Flashover:** Due to Mumbai's saline/industrial pollution. *Mitigation:* Use polymer insulators with higher creepage distance (31mm/kV).
*   **Cable Dig-up:** External contractors hitting the 33kV/110kV lines. *Mitigation:* Use concrete encasement and "Danger" marker tiles.

---

## 📚 References
### Standards
* **CEA 2023:** Regulations for Grid Connectivity.
* **IEEE 1547:** Standard for Interconnecting Distributed Resources.
* **CBIP 311:** Manual on Design of Substations.

### Research Papers
* **CIGRE TB 787:** Power Quality in Data Centres.
* **Hitachi Energy:** "GIS Solutions for Urban Hyperscale Data Centres."

### Revision History
* 1.0: Initial setup for L&T Vyoma Grid Interface.

---
**Next File Recommendation:** `06_Transformers/Transformer_Design.md` (Focusing on the 33kV/415V or 110kV/11kV Power Transformers).