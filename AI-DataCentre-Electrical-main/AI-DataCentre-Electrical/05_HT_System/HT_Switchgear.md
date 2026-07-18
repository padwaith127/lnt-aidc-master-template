# Title: HT Switchgear Design, Protection & Architecture
## Purpose: To define the engineering specifications and architectural layout of the Medium Voltage (HT) distribution system for a 40 MW AI facility.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #HTSwitchgear #VCB #RelayProtection #33kV #11kV #Hyperscale #LTVyoma
## Related Files: [[Utility_Interface.md]], [[Transformer_Design.md]], [[Protection_Relay.md]], [[SCADA.md]]
## Standards Covered: IEC 62271-200, IEC 62271-100, CEA 2023, IEEE 242, IS 13118

---

## 1. Overview
The HT (High Tension) Switchgear is the "Primary Distribution Hub" of the data centre. For a 40 MW load in Mahape, this system usually operates at 33kV (Incoming) and 11kV (Internal Distribution). It must facilitate **Concurrent Maintainability**, allowing any breaker or bus section to be serviced without dropping the IT load.

## 2. Engineering Philosophy: AI-Ready HT Architecture
In AI hyperscale design, we utilize a **Block Redundant** or **Distributed Redundant** architecture.
*   **Segmented Busbars:** The main HT bus is segmented using Bus Couplers to limit the "Blast Radius" of a fault.
*   **Rapid Re-configuration:** Use of Motorized VCBs (Vacuum Circuit Breakers) for automated transfer schemes (ATS) during utility failure.
*   **AI Transient Handling:** AI workloads can cause sudden load shedding or pickup. The HT protection must be "Stable" enough to ignore transients but "Sensitive" enough to clear internal faults in <100ms.

## 3. Equipment Selection & Specifications

| Feature | Specification | Reasoning |
| :--- | :--- | :--- |
| **Enclosure Type** | Metal-Clad (LSC-2B-PM) | Ensures maximum operator safety and compartmentation. |
| **Interruption Medium** | Vacuum (VCB) | Reliable, low maintenance, and environmentally friendly. |
| **Insulation** | Air-Insulated (AIS) or Gas (GIS) | GIS is preferred in Mahape due to coastal salt air/humidity. |
| **Busbar Material** | Electrolytic Copper (99.9%) | Lower losses and better thermal performance than Al. |
| **Protection Relay** | Numerical (IEC 61850 Compliant) | Enables high-speed GOOSE messaging for logic. |

## 4. Engineering Calculations

### 4.1 Short-Circuit Breaking Capacity ($I_{sc}$)
You must ensure the breaker can quench the arc during a fault.
*   **Formula:** $I_{sc} \geq \frac{S_{fault}}{\sqrt{3} \times V_{nominal}}$
*   **Worked Example (Mahape Utility Data):**
    *   Utility Fault Level: 1500 MVA at 33kV.
    *   $I_{sc} = \frac{1,500,000,000}{1.732 \times 33,000} \approx 26.24 \text{ kA}$
    *   **Selection:** 31.5 kA for 3 seconds (Standardized rating).

### 4.2 CT Ratio and Burden Sizing
Current Transformers (CT) must not saturate during a fault.
*   **Ratio Selection:** 120% of full load current.
*   **Protection Core:** 5P20 (5% error at 20 times rated current).
*   **Metering Core:** Class 0.2s (Revenue quality).

## 5. Protection Philosophy (The "Protection SLD")
Every HT feeder in the 40 MW plant must have:
1.  **Overcurrent & Earth Fault (50/51, 50N/51N):** Standard IDMT (Inverse Definite Minimum Time) curves.
2.  **Differential Protection (87T/87B):** For Transformers >10MVA and Main Busbars.
3.  **Restricted Earth Fault (64R):** To detect internal winding faults in transformers.
4.  **Under/Over Voltage (27/59):** To protect UPS/Cooling motors from grid instability.

## 6. Construction & Layout (L&T Execution Standards)
*   **Clearance:** Maintain minimum clearances per **CEA Schedule VI** (e.g., 33kV: Phase-Phase 320mm, Phase-Earth 220mm).
*   **Cable Entry:** Bottom entry via trench or Top entry via busduct. Ensure "Fire Sealing" (MCT) is applied to all entries.
*   **Room Environment:** HT rooms must be pressurized and air-conditioned to prevent the ingress of Mumbai’s humid/saline air, which causes "Tracking" on insulators.

## 7. Commissioning Sequence (SIT - Site Integration Testing)
1.  **Mechanical Check:** Verify alignment of VCB "Truck" and shutter operations.
2.  **Contact Resistance Test:** Verify <50 micro-ohms across breaker poles.
3.  **Secondary Injection:** Inject current into relays to verify trip times against the Coordination Study.
4.  **Primary Injection:** To verify CT polarity and ratio through the entire string.
5.  **Hi-Pot Test:** 60kV AC (for 33kV gear) or DC equivalent to check insulation integrity.

## 8. Failure Modes & AI-Specific Risks
*   **Partial Discharge (PD):** High humidity in Navi Mumbai leads to PD in cable terminations. *Mitigation:* Install permanent Online PD Monitoring sensors.
*   **Resonance:** Large AI sites have massive amounts of capacitance (UPS filters). This can cause "Ferroresonance" during switching. *Mitigation:* Use damping resistors on PTs.

---

## 9. Design Checklist
- [ ] Is the switchgear rated for an ambient of 50°C (de-rated from 40°C standard)?
- [ ] Are all relays communicating via **IEC 61850** to the EPMS?
- [ ] Does the "Arc Flash" study require the use of "Remote Racking" for operators?
- [ ] Are the VCBs rated for the "X/R Ratio" of the utility grid at Mahape?

---
## 📚 References
### Standards
* **IEC 62271-200:** High-voltage switchgear and controlgear - Part 200: AC metal-enclosed switchgear.
* **CEA 2023:** Safety measures for HV installations.
* **IEEE 242:** Protection and Coordination (Buff Book).

### Manufacturer Documents
* **ABB:** "UniGear ZS1 Technical Guide."
* **Siemens:** "NXAIR Medium Voltage Switchgear Manual."
* **Schneider Electric:** "MCSET Design Guide."

### Revision History
* 1.0: Initial release for Mahape 40MW HT System.

---
**Next File Recommendation:** `07_DG_System/Backup_Generation.md` (Focusing on the 40 MW Emergency Backup strategy).