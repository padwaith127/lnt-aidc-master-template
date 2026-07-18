# Title: Harmonics Analysis & Mitigation Strategies
## Purpose: To define the engineering approach for identifying, calculating, and mitigating harmonic distortion caused by non-linear AI server loads.
## Project: {{cookiecutter.project_name}}
## Tags: #Harmonics #THDi #IEEE519 #PowerQuality #ActiveHarmonicFilter
## Standards Covered: IEEE 519, IEC 61000-3-4, Local Grid Codes

---

## 1. Overview
In a {{cookiecutter.it_capacity_mw}} MW AI-ready data centre, the primary load consists of thousands of Switched Mode Power Supplies (SMPS) within {{cookiecutter.ai_silicon_vendor}} power shelves. These are **non-linear loads** that draw current in pulses, creating Harmonic Distortion. If unmanaged, harmonics lead to transformer overheating, capacitor failure, and "ghost" tripping of relays.

## 2. Theory: Current vs. Voltage Harmonics
*   **THDi (Current Distortion):** Injected into the system by the AI servers (the "source").
*   **THDv (Voltage Distortion):** Created when distorted current flows through system impedance ($V = I_{harmonic} \times Z_{sys}$).
*   **Triplen Harmonics (3rd, 9th, 15th):** Zero-sequence harmonics that do not cancel out in the neutral. They add up mathematically ($I_n \approx 3 \times I_{h3}$).

## 3. Engineering Calculations: THD and Neutral Loading
### 3.1 THD Formula
$$THD = \frac{\sqrt{\sum_{h=2}^{\infty} I_h^2}}{I_1} \times 100\%$$
### 3.2 Estimating Neutral Current ($I_n$)
If the 3rd harmonic exceeds 33%, the neutral current will exceed the phase current.
*   **Critical Rule:** 200% Neutral busducts and cables are non-negotiable in AI rows to prevent fire hazards from Triplen accumulation.

## 4. IEEE 519 Limits (At PCC)
Ensure the {{cookiecutter.project_name}} plant meets these limits at the {{cookiecutter.utility_voltage_kv}}kV Point of Common Coupling (PCC) with {{cookiecutter.utility_provider}}:
*   **Voltage (THDv):** Individual < 3.0%, Total < 5.0%
*   **Current (THDi):** Typically 5.0% to 8.0% (Depends on $I_{sc}/I_L$ ratio).

## 5. Mitigation Strategies for AI Facilities
1.  **K-Factor Transformers:** Specify **K-13** or **K-20** transformers. They have oversized neutrals and specialized windings to handle eddy-current heating.
2.  **Active Harmonic Filters (AHF):** Power electronics that monitor load current and inject "counter-harmonics" in real-time to cancel distortion. Installed in parallel at the Main LV Bus.
3.  **UPS Integration:** Modern Double-Conversion UPS acts as a "Harmonic Firewall." The rectifier ensures the THDi reflected back to the Utility is $< 3\%$.

## 6. Failure Modes
*   **Neutral-to-Earth Voltage:** High harmonics increase the voltage between Neutral and Earth at the rack ($V_{N-E} > 2V$), which can crash high-speed AI networking cards.
*   **Capacitor Explosion:** Harmonics cause over-current in PFC capacitor banks due to low impedance at high frequencies.

## 7. Design Checklist
- [ ] Has a Harmonic Study been performed in ETAP?
- [ ] Are the transformers rated K-13 minimum for the AI zones?
- [ ] Is the Neutral busbar sized for 200% of the Phase?
- [ ] Are Active Harmonic Filters (AHF) included if THDi at PCC is $> 5\%$?
