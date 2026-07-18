# Title: Load Flow & System Stability Analysis for AI Clusters
## Purpose: To define the methodology for analyzing steady-state power flow and transient stability in a {{cookiecutter.it_capacity_mw}} MW AI-ready facility.
## Project: {{cookiecutter.project_name}}
## Tags: #LoadFlow #SystemStability #StepLoad #ETAP #{{cookiecutter.ai_silicon_vendor}}
## Standards Covered: IEEE 399 (Brown Book), IEEE 3002.2

---

## 1. Overview
In a traditional data centre, Load Flow analysis is a routine check to ensure cables aren't overloaded. In a **{{cookiecutter.it_capacity_mw}} MW facility**, this analysis is a high-stakes simulation of **system resilience**. {{cookiecutter.ai_silicon_vendor}} AI workloads do not draw constant power; they draw power in massive "steps." We must ensure the grid remains stable when thousands of GPUs synchronize compute cycles.

## 2. Theory: Steady-State vs. Dynamic Stability
1.  **Steady-State Load Flow:** Determines voltage magnitudes and real/reactive power flows under normal conditions.
2.  **Transient Stability:** Analyzes the system's ability to remain in synchronism when subjected to a sudden disturbance (e.g., a massive AI training burst or a Generator taking over).

## 3. Engineering Philosophy: The "AI Step-Load" Challenge
{{cookiecutter.ai_silicon_vendor}} racks transition from "Idle" to "Full Compute" in microseconds.
*   **The Problem:** This creates a $di/dt$ (rate of change of current) that can cause significant voltage dips ($V_{dip} = L \cdot di/dt$) at the UPS output.
*   **Strategy:** We perform "Dynamic Step-Load Modeling" in ETAP/SKM, treating the AI cluster not as a static kW value, but as a time-varying load profile.

## 4. Engineering Calculations
### 4.1 The Power Flow Equation
For every bus $i$ in the {{cookiecutter.project_name}} grid:
$$S_i = V_i \sum_{j=1}^{N} Y_{ij}^* V_j^*$$
*   **Goal:** Solve for $V$ and $\theta$ to ensure voltage stays within $\pm 5\%$ of nominal.

### 4.2 Voltage Drop Assessment
For long runs from the HT Yard to the Data Halls:
$$V_{drop} \approx I(R \cos \phi + X \sin \phi)$$
*   **Constraint:** In AI zones, voltage drop must be kept $< 2\%$ at the PDU input to allow for dynamic "headroom" during GPU bursts.

## 5. Modeling Workflow (ETAP/SKM)
1.  **Define Load Categories:** 
    *   Category A (Static): Cooling pumps, lighting.
    *   Category B (Dynamic): {{cookiecutter.ai_silicon_vendor}} GPU Clusters.
2.  **Run Contingency Analysis (N+1):** Simulate the failure of one main transformer. Does the remaining unit handle the {{cookiecutter.it_capacity_mw}} MW without exceeding its emergency rating?
3.  **Run Step-Load Analysis:** Simulate the simultaneous startup of the liquid cooling plant and AI compute. Verify voltage dip $< 15\%$.

## 6. AI-Ready Design Considerations
1.  **Transformer Tap Settings:** Use Load Flow to determine the optimal Fixed Tap or OLTC setting to maintain nominal voltage at the UPS input.
2.  **Generator Step-Loading:** If the utility fails, the DGs must pick up the {{cookiecutter.it_capacity_mw}} MW load. Use Stability Analysis to prove the DGs won't stall when the first "Block" of AI load hits the bus.

## 7. Design Checklist
- [ ] Has the N-1 contingency analysis been performed for both HT and LT layers?
- [ ] Does the system maintain $\pm 5\%$ voltage during a 50% AI load step?
- [ ] Has the Chiller/CDU pump inrush been modeled alongside peak AI IT load?
