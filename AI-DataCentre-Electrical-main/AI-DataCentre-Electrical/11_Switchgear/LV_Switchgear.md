# Title: Low Voltage (LV) Switchgear Design & PCC Architecture
# Purpose: To define the technical specifications for Main Low Voltage Panels (PCCs) and the logic for power distribution in a 40 MW AI-ready facility.
# Revision: 1.0
# Date: 24-May-2024
# Version: 1.0
# Tags: #LVSwitchgear #PCC #ACB #ATS #IEC61439 #Selectivity #Form4b
# Related Files: [[Transformer_Design.md]], [[Busbar_Distribution.md]], [[Protection_Relay.md]], [[Short_Circuit.md]]
# Standards Covered: IEC 61439-1 & 2, IS 8623, IEEE 241, NBC 2016, CEA 2023

---

## 1. Overview
In the L&T Mahape 40 MW plant, the LV Switchgear (Power Control Centres - PCC) acts as the primary clearinghouse for electricity stepped down from the transformers. It houses the Air Circuit Breakers (ACBs) that manage the Main-Tie-Main (MTM) configurations and the Automatic Transfer Schemes (ATS) that switch between Utility and Generator power.

## 2. Engineering Philosophy: Concurrent Maintainability
To meet Uptime Tier III/IV standards, the LV Switchgear must support "Concurrent Maintainability."
*   **Segmented Busbars:** Each Main PCC is divided into sections.
*   **Form of Separation:** **Form 4b (Type 7)** is mandatory. This ensures that the busbars, functional units (breakers), and cable terminations are all in separate compartments, allowing an engineer to work on one feeder while the rest of the panel is live.
*   **Withdrawable Design:** All ACBs and critical MCCBs must be of the "Fully Withdrawable" type for rapid replacement.

## 3. Equipment Selection & Typical Ratings

| Component | Specification for 40 MW AI DC | Reasoning |
| :--- | :--- | :--- |
| **Main Breakers (Incomers)** | Air Circuit Breakers (ACB) | High ampacity (3200A-6300A) and high Icu/Ics. |
| **Out-feeders** | MCCB or ACB | Based on load (MCCB for <630A, ACB for >800A). |
| **Breaking Capacity ($I_{cu}$)** | 50kA / 65kA / 85kA | Must exceed the calculated fault level from 2.5MVA+ transformers. |
| **Service Breaking ($I_{cs}$)** | 100% of $I_{cu}$ | Critical for DC; breaker must be reusable after a fault. |
| **Busbar Material** | Electrolytic Copper (Silver/Tin plated) | Superior conductivity and corrosion resistance in Mumbai. |

## 4. Engineering Calculations

### 4.1 ACB Sizing for a 2.5 MVA Transformer
*   **Full Load Current ($I_{flc}$):**
    $$I_{flc} = \frac{2,500,000 \text{ VA}}{\sqrt{3} \times 415 \text{ V}} \approx 3478 \text{ Amperes}$$
*   **Breaker Selection:**
    Standard ACB frame sizes are 3200A or 4000A.
    **Selection:** **4000A ACB** (to allow for continuous loading at 100% capacity + harmonic heating margin).

### 4.2 Short Circuit Rating Verification
If the transformer has 6% impedance ($Z$):
*   **Fault Current ($I_{sc}$):**
    $$I_{sc} = \frac{I_{flc}}{Z} = \frac{3478}{0.06} \approx 57,966 \text{ Amperes (58 kA)}$$
*   **Selection:** The switchgear and all internal components must be rated for **65 kA for 1 second**.

## 5. Automatic Transfer Scheme (ATS) Logic
The PCC manages the transition between Utility and DG power.
1.  **Condition:** Utility voltage drops below 80% for >2 seconds.
2.  **Action:** Incomer 1 (Utility) trips.
3.  **Action:** "Start Signal" sent to DG Plant.
4.  **Condition:** DG reaches 95% voltage and frequency.
5.  **Action:** Incomer 2 (DG) closes.
6.  **Safety:** Electrical and Mechanical interlocks must prevent Utility and DG from ever being paralleled (unless specifically designed for "Closed Transition").

## 6. AI-Ready Design Considerations
1.  **Harmonic Derating:** The Neutral busbar must be **100% or 200%** of the Phase busbar capacity to handle 3rd harmonic currents from AI servers.
2.  **Thermal Management:** 40 MW of power creates massive heat within the switchgear room. Use **Internal Temperature Sensors** on busbar joints (connected to SCADA).
3.  **Electronic Trip Units:** Specify **LSIG** (Long time, Short time, Instantaneous, Ground fault) micro-processor based releases with integrated power metering.

## 7. Layout & Installation (L&T Standards)
*   **Rear Access:** Mandatory for Form 4b panels to allow cable termination without opening the front breaker compartment.
*   **Cable Alley:** Sufficient width (min 400mm-600mm) to accommodate multiple runs of 3.5C x 300 sq.mm XLPE cables or Busduct entries.
*   **Base Channel:** Panels must be mounted on a 75mm or 100mm ISMC base channel, grouted to the floor.

## 8. Commissioning & Testing
1.  **Insulation Resistance (Megger):** Phase-Phase and Phase-Earth (Target >100 MΩ).
2.  **High-Voltage (Hi-Pot) Test:** 2.5 kV for 1 minute for LT gear.
3.  **Contact Resistance:** <10 micro-ohms across ACB poles.
4.  **Secondary Injection:** Testing the Trip Unit curves (L-S-I-G) using a test kit (e.g., Schneider STR or ABB Ekip).
5.  **Interlock Verification:** Testing the "Main-Tie-Main" logic to ensure zero accidental paralleling.

## 9. Failure Modes
*   **Nuisance Tripping:** Inrush current from thousands of AI power supplies trips the "Instantaneous" (I) setting. *Mitigation:* Fine-tune coordination based on actual AI server inrush data.
*   **Busbar Flashover:** Dust and humidity in Mahape lead to tracking. *Mitigation:* Use insulated busbars (Heat-shrink sleeves) and maintain room IP rating.

---

## 10. Design Checklist
- [ ] Is the form of separation Form 4b?
- [ ] Is the $I_{cs}$ rated at 100% of $I_{cu}$?
- [ ] Are the ACBs 4-pole or 3-pole with an overlapped neutral (based on earthing design)?
- [ ] Has the panel been de-rated for 50°C ambient temperature?
- [ ] Are the protection relays IEC 61850 compliant for EPMS integration?

---
## 📚 References
### Standards
* **IEC 61439-1 & 2:** Low-voltage switchgear and controlgear assemblies.
* **IS 8623:** Specification for LV Switchgear.
* **IEEE 241:** Recommended Practice for Electric Power Systems in Commercial Buildings.

### Manufacturer Documents
* **L&T Switchgear:** "Ti-Series Main PCC Technical Catalogue."
* **Schneider Electric:** "Okken/BlokSeT Technical Manual."
* **ABB:** "Emax 2 Air Circuit Breaker Technical Guide."

### Revision History
* 1.0: Initial release for Mahape 40MW LV Switchgear strategy.

---
**Next File Recommendation:** `10_STS/Static_Transfer_Switches.md` (Crucial for millisecond-level power path switching for dual-corded AI servers).