# Title: Harmonics Analysis & Mitigation Strategies
## Purpose: To define the engineering approach for identifying, calculating, and mitigating harmonic distortion caused by non-linear AI server loads in a 40 MW facility.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #Harmonics #THDi #IEEE519 #PowerQuality #ActiveHarmonicFilter #NVIDIA #LTVyoma
## Related Files: [[Transformer_Design.md]], [[UPS_System_Design.md]], [[Power_Quality.md]], [[Load_Flow.md]]
## Standards Covered: IEEE 519-2022, IEC 61000-3-2/3-4, CEA 2023, IS 14700

---

## 1. Overview
In a 40 MW AI-ready data centre, the primary load consists of thousands of Switched Mode Power Supplies (SMPS) within NVIDIA GPU power shelves. These are **non-linear loads** that draw current in pulses, creating Harmonic Distortion. If unmanaged, harmonics lead to overheating of transformers, premature failure of capacitors, skin-effect heating in busbars, and "ghost" tripping of sensitive protection relays.

## 2. Theory: Current vs. Voltage Harmonics
*   **THDi (Current Distortion):** Injected into the system by the AI servers (the "source" of the pollution).
*   **THDv (Voltage Distortion):** Created when the distorted current flows through the system impedance ($V = I_{harmonic} \times Z_{sys}$). High system impedance (weak grid/small transformers) makes THDv worse.
*   **Triplen Harmonics (3rd, 9th, 15th):** These are zero-sequence harmonics that do not cancel out in the neutral. In a 3-phase 4-wire system, they add up mathematically in the neutral conductor ($I_n \approx 3 \times I_{h3}$).

## 3. Engineering Calculations: THD and Neutral Loading

### 3.1 Total Harmonic Distortion (THD) Formula
$$THD = \frac{\sqrt{\sum_{h=2}^{\infty} I_h^2}}{I_1} \times 100\%$$
*   $I_1$: Fundamental current (50 Hz).
*   $I_h$: Harmonic component at order $h$.

### 3.2 Estimating Neutral Current ($I_n$)
For an AI cluster with a 3rd harmonic content of 30%:
*   $I_{phase} = 100A$
*   $I_{h3} = 30A$
*   $I_{neutral} \approx \sqrt{(3 \times 30)^2} = 90A$ (assuming balanced fundamental).
*   **Critical Rule:** If the 3rd harmonic exceeds 33%, the neutral current will exceed the phase current.

## 4. CEA 2023 & IEEE 519 Limits (At PCC)
As an L&T engineer, you must ensure the 40 MW plant meets these statutory limits at the Point of Common Coupling (PCC) with MSEDCL:

| Harmonic Order | Individual Limit (%) | Total Harmonic Distortion (THD) |
| :--- | :--- | :--- |
| **Voltage (THDv)** | 3.0% | 5.0% |
| **Current (THDi)** | Depends on $I_{sc}/I_L$ ratio | Typically 5.0% to 8.0% |

## 5. Mitigation Strategies for AI Facilities

### 5.1 K-Factor Transformers
*   Specify **K-13** or **K-20** transformers. These are designed with oversized neutrals and specialized windings to handle the extra eddy-current heating caused by high-frequency harmonic components.

### 5.2 Active Harmonic Filters (AHF)
*   **Technology:** Power electronics that monitor the load current and inject "counter-harmonics" in real-time to cancel out the distortion.
*   **Placement:** Installed in parallel at the Main LV Bus or at the PDU level.
*   **Benefit:** Also provides reactive power (VAR) compensation for power factor correction.

### 5.3 UPS Integration
*   Modern Double-Conversion UPS acts as a "Harmonic Firewall." The rectifier ensures the THDi reflected back to the Utility is $< 3\%$, regardless of the IT load's distortion.

### 5.4 Phase Shifting
*   Using Delta-Wye and Delta-Delta transformer configurations in parallel can cancel out the 5th and 7th harmonics.

## 6. AI-Ready Design Considerations
1.  **Skin Effect:** Harmonics are higher frequency (3rd = 150Hz, 5th = 250Hz). This increases the resistance of conductors due to the skin effect. Oversize busbars by 15-20% in AI zones.
2.  **Resonance Risk:** Large data centres have massive capacitance (UPS filters/Cables). This can react with system inductance to create **Parallel Resonance**, magnifying specific harmonics to dangerous levels.
3.  **Neutral Sizing:** 200% Neutral busducts and cables are non-negotiable in AI rows to prevent fire hazards from Triplen accumulation.

## 7. Commissioning & Testing
1.  **Power Quality Audit:** Use a Class A Power Quality Analyzer (PQA) during the Integrated Systems Test (IST).
2.  **Harmonic Profile Mapping:** Record the THDi at 25%, 50%, 75%, and 100% AI load. Distortion often increases at lower loads.
3.  **AHF Validation:** Turn the Active Harmonic Filter ON and OFF to verify the reduction in THDi at the transformer primary.

## 8. Failure Modes
*   **Neutral-to-Earth Voltage:** High harmonics increase the voltage between Neutral and Earth at the rack ($V_{N-E} > 2V$), which can crash NVIDIA GPU networking cards.
*   **Capacitor Explosion:** Harmonics cause over-current in PFC capacitor banks due to low impedance at high frequencies.
*   **Relay Maloperation:** Relays sensing "True RMS" may trip prematurely if the crest factor of the wave is too high.

---

## 9. Design Checklist
- [ ] Has a Harmonic Study been performed in ETAP?
- [ ] Are the transformers rated K-13 minimum for the AI zones?
- [ ] Is the Neutral busbar sized for 200% of the Phase?
- [ ] Are Active Harmonic Filters (AHF) included if THDi at PCC is $> 5\%$?
- [ ] Does the UPS have an Input THDi filter or Active Front End (AFE)?

---
## 📚 References
### Standards
* **IEEE 519-2022:** Standard Requirements for Harmonic Control in Electric Power Systems.
* **CEA 2023:** Technical Standards for Connectivity to the Grid (Clause 11).
* **IEC 61000-3-4:** Limits for harmonic currents in systems with rated current $> 16A$.

### Research Papers
* **NVIDIA Technical Brief:** "Power Supply Considerations for High-Density GPU Clusters."
* **Schneider Electric WP #102:** "Monitoring and Mitigating Harmonics in Data Centers."

### Revision History
* 1.0: Initial Harmonics Mitigation strategy for L&T Vyoma Mahape.

---
**Next File Recommendation:** `23_Power_Quality/Transient_and_Sag_Analysis.md` (Focusing on Voltage Sags, Swells, and the ITIC/CBEMA curve compliance).