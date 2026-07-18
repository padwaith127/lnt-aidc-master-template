# Title: UPS System Design for AI-Ready Hyperscale Facilities
## Purpose: To define the engineering specifications, topology selection, and performance criteria for the UPS system supporting the {{cookiecutter.it_capacity_mw}} MW IT load.
## Project: {{cookiecutter.project_name}}
## Tags: #UPS #PowerQuality #LithiumIon #BESS #AI-Infrastructure #DoubleConversion

---

## 1. Overview
In an AI-ready facility like {{cookiecutter.project_name}}, the UPS is no longer just a "battery backup"; it is a dynamic power conditioner. AI workloads ({{cookiecutter.ai_silicon_vendor}} clusters) exhibit extreme load swings. The UPS must protect the upstream HT/LT distribution from these transients while ensuring the IT load sees a "Class 1" power quality environment.

## 2. UPS Topology: Double Conversion (VFI)
For hyperscale, the only acceptable topology is **Voltage and Frequency Independent (VFI)** (Double Conversion).
*   **Normal Mode:** Rectifier converts AC to DC; Inverter converts DC back to clean AC.
*   **AI Requirement:** The UPS must have a **High Fault-Clearing Capacity** to trip downstream breakers in high-density racks without dropping into bypass.

## 3. Engineering Philosophy: AI-Ready Design
### 3.1 Handling AI Step Loads
AI training involves "bursty" compute cycles.
*   **Problem:** Rapid transitions from 10% to 100% load can cause DC bus voltage dips in the UPS.
*   **Solution:** Specify UPS with **Wide Input Voltage Windows** and **Dynamic Response Time < 20ms** for 0-100% load steps.

### 3.2 Efficiency vs. Protection
*   **Double Conversion Mode:** 96-97% efficiency. Provides maximum isolation.
*   **ECO Mode / ESS Mode:** 99% efficiency. UPS stays on bypass until a fault is detected.
*   **Strategy:** In {{cookiecutter.ai_silicon_vendor}} zones, stay in **Double Conversion**. The risk of a millisecond transfer lag in ECO mode is too high for multi-million dollar GPU racks.

## 4. Engineering Calculations
### 4.1 UPS Sizing Formula
$$S_{ups} = \frac{P_{IT} \times SF}{PF_{out} \times \eta}$$
*   $SF$: Safety Factor (typically 1.1).
*   $PF_{out}$: Rated Output Power Factor (typically 1.0).
*   $\eta$: Efficiency (0.97).

### 4.2 Heat Dissipation (BTU/hr)
Necessary for HVAC sizing.
$$Heat_{loss} = P_{load} \times (\frac{1 - \eta}{\eta}) \times 3412.14$$
*Ensure the cooling plant is sized to reject this heat at {{cookiecutter.max_ambient_temp}}°C ambient conditions.*

## 5. Battery Energy Storage System (BESS) Integration
*   **Chemistry:** Lithium-ion (LFP preferred) is mandatory to save space and weight.
*   **Autonomy:** 5 to 10 minutes at full load.
*   **C-Rating:** AI UPS require high-rate discharge batteries (typically 4C to 6C) due to the high power-to-energy ratio required for brief DG bridging.

## 6. AI-Specific Considerations
1.  **Rectifier Walk-in:** Program the UPS to ramp up its input current over 15-30 seconds when switching from Battery to Generator to prevent DG frequency instability.
2.  **Harmonic Mitigation:** Ensure Input THDi < 3% to avoid overheating upstream K-rated transformers.

## 7. Failure Modes
*   **Static Switch Failure:** UPS cannot transfer to bypass; load is lost. *Mitigation:* Use dual-redundant power supplies for UPS internal logic.
*   **Thermal Runaway:** Battery overheating. *Mitigation:* Use Li-ion cabinets with built-in BMS and integrated fire suppression.

## 8. Design Checklist
- [ ] Is the UPS rated for Output Power Factor 1.0?
- [ ] Does the UPS support Lithium-ion communication (BMS integration)?
- [ ] Has the input breaker been sized for **125%** to account for battery charging + full load?
- [ ] Are the internal fans redundant?
