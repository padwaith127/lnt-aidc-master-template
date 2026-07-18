# Title: Master Electrical Engineering Formula Reference
## Purpose: A centralized "Cheat Sheet" of every engineering formula required to design, validate, and troubleshoot a {{ cookiecutter.it_capacity_mw }} MW AI-ready hyperscale facility.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #Calculations #ElectricalEngineering #Formulas #DataCentreDesign #{{ cookiecutter.project_code }} #QuickReference
## Related Files: [[AI_Load_Estimation.md]], [[Fault_Level_Calculations.md]], [[Sizing_and_Routing.md]], [[Grounding_Grid_Design.md]]
## Standards Covered: IEEE, IEC, IS, NFPA

---

## 1. Fundamentals of Power (AC & DC)

### 1.1 Three-Phase Power (AC)
Used for Transformers, Generators, and Main Distribution.
*   **Apparent Power (S):** $S = \sqrt{3} \times V_L \times I_L$ (Unit: VA)
*   **Active Power (P):** $P = \sqrt{3} \times V_L \times I_L \times \cos \phi$ (Unit: Watts)
*   **Reactive Power (Q):** $Q = \sqrt{3} \times V_L \times I_L \times \sin \phi$ (Unit: VAR)
*   **Power Factor ($\cos \phi$):** $PF = \frac{P}{S}$

### 1.2 DC Power ({{ cookiecutter.ai_silicon_vendor }} Rack Backplane)
Used for 48V/54V DC Busbars in AI Racks.
*   **Power (P):** $P = V \times I$ (Unit: Watts)
*   **Current (I):** $I = \frac{P}{V}$ (Unit: Amperes)

---

## 2. Load Estimation & Efficiency (Data Centre Metrics)

### 2.1 Power Usage Effectiveness (PUE)
*   **PUE:** $\frac{\text{Total Facility Power}}{\text{IT Equipment Power}}$
*   **Partial PUE (pPUE):** Calculated for a specific subsystem (e.g., Cooling).

### 2.2 Cooling Load Conversion
*   **Heat (BTU/hr):** $kW \times 3412.14$
*   **Tons of Refrigeration (TR):** $\frac{BTU/hr}{12,000}$

---

## 3. Transformer & Short Circuit Analysis

### 3.1 Symmetrical Fault Current ($I_{sc}$)
*   **From Transformer Z%:** $I_{sc} = \frac{I_{flc} \times 100}{Z\%}$
*   **Per-Unit (PU) Method:** $I_{sc} = \frac{I_{base}}{Z_{pu}}$

### 3.2 Transformer K-Factor
Used to size transformers for non-linear AI loads.
*   **K-Factor:** $\sum (I_h^2 \times h^2)$
    *   $I_h$: Per-unit harmonic current at order $h$.
    *   $h$: Harmonic order.

---

## 4. Cable Design & Voltage Drop

### 4.1 Voltage Drop ($\Delta V$)
*   **Three-Phase:** $\Delta V = \sqrt{3} \times I \times (R \cos \phi + X \sin \phi) \times L$
*   **Percentage Drop:** $\% \Delta V = \frac{\Delta V}{V_{nominal}} \times 100$

### 4.2 Short Circuit Withstand (Cable Insulation)
*   **Cross Section (A):** $A = \frac{I_{sc} \times \sqrt{t}}{k}$
    *   $k$: Constant (143 for Copper/XLPE, 94 for Al/XLPE).
    *   $t$: Duration of fault (seconds).

---

## 5. Earthing & Safety (IEEE 80)

### 5.1 Soil Resistivity (Wenner Method)
*   **Resistivity ($\rho$):** $2 \times \pi \times a \times R$
    *   $a$: Electrode spacing (m).
    *   $R$: Measured resistance ($\Omega$).

### 5.2 Tolerable Touch Voltage ($E_{touch}$)
For a 50kg human:
*   **$E_{touch}$:** $(1000 + 1.5 \times C_s \times \rho_s) \times \frac{0.116}{\sqrt{t_s}}$
    *   $C_s$: Surface layer derating factor.
    *   $\rho_s$: Resistivity of surface material (e.g., crushed rock).

---

## 6. Protection & Relay Coordination

### 6.1 Relay Operating Time (IEC 60255 - Normal Inverse)
*   **Time (t):** $TMS \times \frac{0.14}{(I/I_s)^{0.02} - 1}$
    *   $TMS$: Time Multiplier Setting.
    *   $I/I_s$: Multiple of Pickup Current.

---

## 7. AI-Specific Infrastructure Formulas

### 7.1 UPS Dynamic Step-Load
*   **Transient Voltage Deviation ($\Delta V_{tr}$):** $L \times \frac{di}{dt}$
    *   *Objective for AI:* Minimize $L$ (inductance) via short busway runs.

### 7.2 Battery Sizing (Discharge Amps)
*   **$I_{batt}$:** $\frac{P_{load(kW)}}{V_{dc(min)} \times \eta_{inverter}}$

---

## 8. Unit Conversion Table for Quick Reference

| To Convert | To | Multiply By |
| :--- | :--- | :--- |
| HP (Horsepower) | kW | 0.746 |
| sq.mm (Copper) | Circular Mils | 1973.5 |
| Celsius ($^\circ$C) | Fahrenheit ($^\circ$F) | $(^\circ$C $\times 1.8) + 32$ |
| kg/sq.m | lb/sq.ft | 0.2048 |
| Liters | Gallons (US) | 0.264 |

---

## 9. Design Checklist: Sanity Checks
- [ ] **Check 1:** Is the Neutral current in the AI zone $< 1.73 \times$ Phase current? (If higher, check 3rd harmonic content).
- [ ] **Check 2:** Is the Fault Level $\leq {{ cookiecutter.fault_level_ka }} \text{ kA}$? (If higher, switchgear costs will escalate exponentially).
- [ ] **Check 3:** Is the Voltage Drop to the Rack $< 5\%$? ({{ cookiecutter.ai_silicon_vendor }} requires tight tolerances).
- [ ] **Check 4:** Does the DG Fuel storage support 48 hours at 100% Load?

---
## 10. References
### Standards
* **IEEE 141:** Red Book (Power Distribution).
* **IEEE 142:** Green Book (Grounding).
* **IEC 60364:** Electrical Installations for Buildings.
* **IS 732:** Indian Standard for Wiring.

### Revision History
* 1.0: Compiled Master Formulas for {{ cookiecutter.project_name }} {{ cookiecutter.city }} project.

---
**Next File Recommendation:** `Standard_Layouts.md` (Visualizing the physical architecture of the {{ cookiecutter.it_capacity_mw }} MW plant).
