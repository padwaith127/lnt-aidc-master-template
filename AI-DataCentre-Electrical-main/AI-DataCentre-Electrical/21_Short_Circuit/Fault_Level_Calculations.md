# Title: Short Circuit Analysis & Arc Flash Safety
## Purpose: To define the methodology for calculating maximum fault currents to ensure equipment withstand ratings and Arc Flash safety for the {{cookiecutter.project_name}}.
## Project: {{cookiecutter.project_name}}
## Tags: #ShortCircuit #FaultLevel #IEC60909 #IEEE551 #ArcFlash #IEEE1584
## Standards Covered: IEC 60909, IEEE 551, IEEE 1584-2018, OSHA/NESC

---

## 1. Overview
Short circuit analysis ensures that every breaker and busbar can withstand the violent mechanical forces generated during a fault. Because the {{cookiecutter.it_capacity_mw}} MW facility uses large, low-impedance transformers operated in parallel, fault levels can easily hit the {{cookiecutter.fault_level_ka}} kA design limit.

## 2. Theory: The Nature of a Fault
*   **Symmetrical Fault Current ($I_{sc}$):** The steady-state AC component.
*   **Asymmetrical Peak Current ($i_p$):** The initial "sub-transient" burst that creates maximum mechanical stress. Driven by the **X/R Ratio** of the system.
*   **Mechanical Force ($F$):** In a busbar, $F \propto i_p^2$.

## 3. Engineering Calculations: The "Per-Unit" (PU) Method
To calculate fault levels in a complex grid (Utility -> HT -> Transformer -> LT):
### Step 1: Establish Base Values
*   $S_{base} = 100 \text{ MVA}$
*   $V_{base} = \text{Nominal voltage (e.g., 0.415 kV or 0.480 kV)}$.

### Step 2: Calculate Fault Level ($I_{sc}$) at LT Bus
Assuming a "Strong Grid" at the {{cookiecutter.utility_voltage_kv}}kV entry:
$$I_{sc(sym)} = \frac{I_{base}}{Z_{total(pu)}}$$
**Requirement:** The switchgear must be rated for at least **{{cookiecutter.fault_level_ka}} kA**. If transformers are paralleled, the fault level may double, which is typically avoided through "Open-Tie" configurations.

## 4. Equipment Withstand & Breaking Capacity
*   **$I_{cu}$ (Ultimate Breaking Capacity):** The max fault a breaker can interrupt once.
*   **$I_{cs}$ (Service Breaking Capacity):** Must be **100% of $I_{cu}$** for Data Centres.

## 5. Arc Flash Boundary & Safety Limitations
Arc Flash incident energy calculations define the PPE required by technicians.
*   **LV & MV Switchgear (Up to 15kV):** Utilize **IEEE 1584-2018** to calculate the incident energy (cal/cm²) based on symmetrical fault current and clearing time.
*   **The {{cookiecutter.utility_voltage_kv}}kV Utility Entrance Limitation:** If your utility voltage is >15kV, **you cannot use IEEE 1584-2018**. The mathematical model has a strict validated boundary of 15kV. 
*   **Mitigation:** To calculate incident energy at the {{cookiecutter.utility_voltage_kv}}kV HT yard, use OSHA guidelines, **ARCPRO software**, or NESC tables. 

## 6. AI-Ready Design Considerations
1.  **UPS Contribution:** When in **Bypass Mode**, the UPS passes the full utility fault current through to the AI racks. Model the "Bypass" condition as the worst-case scenario.
2.  **Motor Contribution:** Large liquid cooling pumps act as generators for a few cycles during a fault. Add $4 \times I_{flc}$ of all running motors.

## 7. Design Checklist
- [ ] Is the $I_{cs}$ rating 100% of $I_{cu}$ for all critical breakers?
- [ ] Is the system operated with "Open Ties" to keep fault levels $\leq$ {{cookiecutter.fault_level_ka}} kA?
- [ ] Has ARCPRO or NESC been used instead of IEEE 1584 for the {{cookiecutter.utility_voltage_kv}}kV arc flash analysis?
