# Title: Power Quality - Transient, Sag (Dip), and Swell Analysis
## Purpose: To define the engineering parameters for maintaining voltage stability and immunity against power quality disturbances in an AI-ready facility.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #PowerQuality #VoltageSag #VoltageSwell #Transients #ITIC #CBEMA #IEEE1159 #LTVyoma
## Related Files: [[UPS_System_Design.md]], [[Harmonics.md]], [[EPMS.md]], [[NVIDIA_Architecture.md]]
## Standards Covered: IEEE 1159, ITIC (CBEMA) Curve, SEMI F47, IEC 61000-4-30 Class A, IEEE 1100

---

## 1. Overview
In a 40 MW AI data centre, "Power Quality" (PQ) goes beyond harmonics. AI GPU clusters are highly sensitive to **Voltage Sags (Dips)** and **Transients**. A voltage sag lasting only 50 milliseconds can trip the high-speed under-voltage protection in an NVIDIA power shelf, causing a multi-million dollar training job to fail. This module covers the analysis of non-steady-state voltage events.

## 2. Definitions & AI Impact

| Event Type | Duration | Definition | Impact on AI Infrastructure |
| :--- | :--- | :--- | :--- |
| **Transient (Impulse)** | < 50 ns to 1 ms | Sudden "spike" (Lightning/Switching). | Can puncture semiconductor insulation in GPUs. |
| **Voltage Sag (Dip)** | 0.5 cycles to 1 min | Decrease in RMS voltage (80% to 90% nom). | Trips DC power shelves; forces UPS to Battery. |
| **Voltage Swell** | 0.5 cycles to 1 min | Increase in RMS voltage (>110% nom). | Stresses capacitor banks and MOV protection. |
| **Flicker** | Continuous | Rapid, repetitive voltage variations. | Can cause cooling VFDs to behave erratically. |

## 3. The ITIC (CBEMA) Curve
The **Information Technology Industry Council (ITIC)** curve is the design benchmark for Data Centres.
*   **Design Goal:** Ensure that the power delivered to the AI rack stays within the "No Interruption" zone of the curve.
*   **Ride-Through:** Modern AI power shelves typically have a **10ms to 20ms** hold-up time (capacitance) to survive very short sags without restarting.

## 4. Engineering Calculations: Sag Magnitude & Duration

### 4.1 Voltage Sag Magnitude at Bus ($V_{sag}$)
When a large motor (e.g., 500kW Chiller) starts at Mahape:
$$V_{sag} = V_{pre-fault} \times \frac{Z_{fault}}{Z_{source} + Z_{transformer} + Z_{fault}}$$
*   **L&T Strategy:** Ensure the sag at the UPS input never drops below 80% of nominal to prevent the UPS from "hunting" between Utility and Battery.

### 4.2 Transient Recovery Time
Following an AI load step-up (0 to 20 MW):
*   **Requirement:** The voltage must recover to $\pm 1\%$ of nominal within **20ms** (1 cycle).
*   **UPS Role:** The UPS inverter's dynamic response is the primary defense here.

## 5. Mitigation Strategies for AI-Ready Sites

### 5.1 Surge Protective Devices (SPD) - Cascaded Logic
*   **Category C (Service Entrance):** High energy handling (HT Yard).
*   **Category B (Distribution):** Medium energy (Main PCCs/UPS Rooms).
*   **Category A (Point of Use):** Low energy/High speed (Inside NVIDIA Racks).

### 5.2 Dynamic Voltage Restorers (DVR) or Active Conditioning
*   For the 40 MW Mahape site, the **Double-Conversion UPS** acts as the ultimate PQ conditioner, effectively decoupling the AI load from grid sags/swells.

### 5.3 Capacitor Bank Tuning
*   If using APFC (Automatic Power Factor Correction) for the mechanical plant, ensure they are **Detuned (with reactors)** to prevent magnifying switching transients.

## 6. AI-Specific Considerations
1.  **Fast Step Loads:** AI training starts/stops create "In-house" transients. The distribution system must have enough **Capacitive Headroom** and low inductance (short busduct runs) to minimize $L \cdot di/dt$ spikes.
2.  **SEMI F47 Compliance:** Ensure all critical liquid cooling pumps and CDUs are tested to **SEMI F47** standards (Voltage Sag Immunity) to ensure cooling doesn't stop during a grid dip.

## 7. Monitoring & Measurement (The EPMS)
*   **Class A Meters:** Install IEC 61000-4-30 Class A meters at the 33kV Incoming and Main LT Incomers.
*   **Event Capture:** Meters must support **Waveform Capture** (1024 samples/cycle) to allow L&T engineers to perform Root Cause Analysis (RCA) after a trip.
*   **Visualization:** The EPMS should automatically plot PQ events on the ITIC curve for immediate impact assessment.

## 8. Commissioning & Testing
1.  **Sag Injection Testing:** Use a specialized test rig to simulate sags at the PDU level and verify the NVIDIA rack survives.
2.  **Switching Simulation:** Perform "Utility to Generator" transfers and monitor the transient spikes at the UPS output bus.
3.  **Grounding Check:** High PQ issues are often caused by poor grounding. Verify the $V_{N-E}$ (Neutral to Earth) is $< 1V$ under full AI load.

## 9. Failure Modes
*   **Insulation Puncture:** Repetitive low-level transients degrading transformer winding insulation over time.
*   **Nuisance BESS Discharge:** UPS switching to batteries too frequently due to "tight" sag settings, leading to premature Lithium-ion battery aging.
*   **Data Corruption:** High-frequency transients causing bit-errors in high-speed NVLink GPU interconnects.

---

## 10. Design Checklist
- [ ] Are Class A PQ meters installed at all primary entry points?
- [ ] Do all SPDs have local and remote monitoring (dry contacts)?
- [ ] Has the UPS transient response been verified for a 100% load step?
- [ ] Are all mechanical/cooling controls compliant with SEMI F47 sag immunity?
- [ ] Is the ITIC curve plot integrated into the EPMS dashboard?

---
## 📚 References
### Standards
* **IEEE 1159:** Recommended Practice for Monitoring Electric Power Quality.
* **IEEE 1100:** Emerald Book (Powering/Grounding).
* **SEMI F47:** Specification for Semiconductor Processing Equipment Voltage Sag Immunity.
* **IEC 61000-4-30:** Testing and measurement techniques – Power quality measurement methods.

### Research Papers
* **EPRI Paper:** "Power Quality Requirements for High-Density Data Centers."
* **Vertiv White Paper:** "Comparing Surge Protection Standards: IEEE vs IEC."

### Revision History
* 1.0: Initial Power Quality strategy for L&T Vyoma Mahape.

---
**Next File Recommendation:** `24_SCADA/Supervisory_Control.md` (Focusing on the automation and high-level control of the 40 MW facility).