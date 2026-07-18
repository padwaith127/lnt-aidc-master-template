# Title: UPS System Design for AI-Ready Hyperscale Facilities
## Purpose: To define the engineering specifications, topology selection, and performance criteria for the Uninterruptible Power Supply (UPS) system supporting 40 MW of AI IT load.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #UPS #PowerQuality #LithiumIon #BESS #AI-Infrastructure #DoubleConversion #Efficiency
## Related Files: [[AI_Load_Estimation.md]], [[Battery_System.md]], [[Generator_Sync.md]], [[NVIDIA_Architecture.md]]
## Standards Covered: IEC 62040-3, IEEE 1100, IEEE 3001.2, NFPA 70 Art 645

---

## 1. Overview
In an AI-ready facility like L&T Mahape, the UPS is no longer just a "battery backup"; it is a dynamic power conditioner. AI workloads (NVIDIA H100/B200 clusters) exhibit extreme load swings. The UPS must protect the upstream HT/LT distribution from these transients while ensuring the IT load sees a "Class 1" power quality environment.

## 2. UPS Topology: Double Conversion (VFI)
For 40 MW Hyperscale, the only acceptable topology is **Voltage and Frequency Independent (VFI)**, also known as Double Conversion.
*   **Normal Mode:** Rectifier converts AC to DC; Inverter converts DC back to clean AC.
*   **Bypass Mode:** Static switch transfers load to utility if the UPS fails.
*   **AI Requirement:** The UPS must have a **High Fault-Clearing Capacity** to trip downstream breakers in high-density racks without dropping into bypass.

## 3. Engineering Philosophy: AI-Ready Design

### 3.1 Handling AI Step Loads
AI training involve "bursty" compute cycles.
*   **Problem:** Rapid transitions from 10% to 90% load can cause DC bus voltage dips in the UPS.
*   **Solution:** Specify UPS with **Wide Input Voltage Windows** and **Dynamic Response Time < 20ms** for 0-100% load steps.

### 3.2 Efficiency vs. Protection
*   **Double Conversion Mode:** 96-97% efficiency. Provides maximum isolation.
*   **ECO Mode / ESS Mode:** 99% efficiency. UPS stays on bypass until a fault is detected.
*   **L&T Strategy:** In AI zones, stay in **Double Conversion** or "Active-Filter" modes. The risk of a millisecond transfer lag in ECO mode is too high for $500k NVIDIA racks.

## 4. Equipment Selection: Modular vs. Monolithic

| Feature | Modular UPS | Monolithic (Large) UPS |
| :--- | :--- | :--- |
| **Capacity** | 50kW - 600kW Modules | 1000kW - 1600kW units |
| **Redundancy** | Internal N+1 | Unit-level N+1 or 2N |
| **Footprint** | Compact (Vertical scaling) | Larger (Horizontal scaling) |
| **Maintenance** | Hot-swappable | Requires bypass/shutdown |
| **Suitability** | AI Edge / RPP Level | Hyperscale Core / Centralized |

*Recommendation for Mahape:* **Large Modular UPS (e.g., 1.2MW to 1.5MW frames)** to allow for granular scaling as AI clusters are deployed.

## 5. Engineering Calculations

### 5.1 UPS Sizing Formula
$$S_{ups} = \frac{P_{IT} \times SF}{PF_{out} \times \eta}$$
*   $P_{IT}$: IT Load (e.g., 2500 kW per block).
*   $SF$: Safety Factor (typically 1.1 or 1.2).
*   $PF_{out}$: Rated Output Power Factor of UPS (typically 1.0).
*   $\eta$: Efficiency (0.97).

**Worked Example (2.5 MW IT Block):**
$$S_{ups} = \frac{2500 \times 1.1}{1.0 \times 0.97} \approx 2835 \text{ kVA}$$
*Configuration:* 3 x 1500 kVA UPS in N+1 (Total capacity 4500 kVA, redundant capacity 3000 kVA).

### 5.2 Heat Dissipation (BTU/hr)
Necessary for HVAC sizing.
$$Heat_{loss} = P_{load} \times (\frac{1 - \eta}{\eta}) \times 3412.14$$
For a 1.5 MW UPS at 97% efficiency:
$$1500 \times (0.03/0.97) \times 3412.14 \approx 158,230 \text{ BTU/hr}$$

## 6. Battery Energy Storage System (BESS) Integration
*   **Chemistry:** Lithium-ion (LiFePO4 or NMC) is mandatory for Mahape to save space and weight.
*   **Autonomy:** 5 to 10 minutes.
*   **C-Rating:** AI UPS require high-rate discharge batteries (typically 4C or higher).

## 7. AI-Specific Considerations
1.  **Rectifier Walk-in:** Program the UPS to ramp up its input current over 15-30 seconds when switching from Battery to Generator to prevent DG frequency instability.
2.  **Harmonic Mitigation:** Ensure Input THDi < 3% to avoid overheating upstream transformers.
3.  **Operation at Altitude/Temp:** Navi Mumbai is sea level, but ensure the 45°C ambient doesn't derate the UPS capacity.

## 8. Commissioning & Testing
*   **Factory Acceptance Test (FAT):** Witness 100% load bank testing, unbalanced load testing, and transient response.
*   **Burn-in Test:** 24-hour continuous run at full load at the site.
*   **Battery Discharge Test:** Validate the actual runtime vs. the design runtime using a calibrated load bank.

## 9. Failure Modes
*   **Static Switch Failure:** UPS cannot transfer to bypass; load is lost. *Mitigation:* Use dual-redundant power supplies for UPS internal logic.
*   **Thermal Runaway:** Battery overheating. *Mitigation:* Use Li-ion cabinets with built-in BMS and fire suppression (Novec 1230/Aerosol).

---

## 10. Design Checklist
- [ ] Is the UPS rated for Output Power Factor 1.0?
- [ ] Does the UPS support Lithium-ion communication (BMS integration)?
- [ ] Has the input breaker been sized for **125%** to account for battery charging + full load?
- [ ] Is the "Cold Start" feature enabled for starting without utility power?
- [ ] Are the internal fans redundant?

---
## 📚 References
### Standards
* **IEC 62040-3:** UPS - Method of specifying the performance and test requirements.
* **IEEE 1100:** Emerald Book (Powering and Grounding Electronic Equipment).
* **NFPA 70E:** Standard for Electrical Safety in the Workplace.

### Manufacturer Documents
* **Schneider Electric:** "Galaxy VL Series Technical Specifications."
* **Vertiv:** "Liebert EXL S1 UPS Datasheet."
* **Eaton:** "Power Xpert 9395P UPS White Paper."

### Revision History
* 1.0: Initial UPS strategy for 40 MW Mahape AI DC.

---
**Next File Recommendation:** `09_Battery_System/Battery_Energy_Storage.md` (Focusing on Lithium-ion chemistry, fire safety, and BMS for the 40 MW plant).