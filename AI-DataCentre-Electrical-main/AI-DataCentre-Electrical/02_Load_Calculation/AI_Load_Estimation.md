# Title: AI Load Estimation & Power Density Calculation
## Purpose: To calculate the total facility power requirement for a {{cookiecutter.it_capacity_mw}} MW IT-load AI-ready data centre.
## Tags: #LoadCalculation #AI-Ready #{{cookiecutter.ai_silicon_vendor}} #CapacityPlanning #PUE
## Standards Covered: IEEE 3001.2, TIA-942-C, ASHRAE TC 9.9

---

## 1. Overview
In a traditional data centre, load estimation is often based on an average density per rack (e.g., 5-10 kW). In the **{{cookiecutter.project_name}} ({{cookiecutter.it_capacity_mw}} MW facility)**, the calculation shifts toward **Cluster-Based Loading**. We must account for the extreme power draw of {{cookiecutter.ai_silicon_vendor}} GPU clusters and the auxiliary loads required to keep them operational (e.g., Liquid Cooling CDUs).

## 2. Theoretical Basis: AI Load Characteristics
AI workloads (Large Language Model training) differ vastly from cloud workloads:
1.  **High Utilization:** AI clusters often run at 80-90% TDP (Thermal Design Power) continuously for weeks.
2.  **Transients:** Power can swing from 10% to 100% in milliseconds during model "checkpointing" or initialization.
3.  **Power Factor:** Modern AI power shelves use active PFC, resulting in a PF near 0.99 at the rack, but mechanical loads pull the facility PF down.

## 3. Engineering Calculation: Total Facility Load (MVA)
To determine the utility transformer capacity for {{cookiecutter.project_name}}, we use the "Inside-Out" method.

### Step 1: IT Load Breakdown
*   **Total Target IT Load:** {{cookiecutter.it_capacity_mw}} MW ({{cookiecutter.it_capacity_mw | float * 1000}} kW).
*   **AI High-Density Zone (Assumed 80%):** {{ (cookiecutter.it_capacity_mw | float * 0.8) | round(2) }} MW.
*   **Standard Compute/Network Zone (Assumed 20%):** {{ (cookiecutter.it_capacity_mw | float * 0.2) | round(2) }} MW.

### Step 2: Cooling Load Calculation (Mechanical Load)
For AI-ready sites, we assume a mix of Liquid Cooling (Direct-to-Chip) and Air Cooling.
*   **Target PUE (Power Usage Effectiveness):** {{cookiecutter.target_pue}}
*   **Mechanical Load Calculation Formula:**
    $$P_{mech} = P_{IT} \times (PUE - 1.0 - Loss_{elec})$$
    *   *Assumption:* Electrical distribution losses ($Loss_{elec}$) are ~5% (0.05).
    *   $P_{mech} = {{cookiecutter.it_capacity_mw}} \times ({{cookiecutter.target_pue}} - 1.0 - 0.05) = {{ (cookiecutter.it_capacity_mw | float * (cookiecutter.target_pue | float - 1.05)) | round(2) }} \text{ MW}$.

### Step 3: Total Facility Active Power (MW)
$$P_{total} = P_{IT} + P_{mech} + P_{admin/misc}$$
*   $P_{admin/misc} \approx 0.5 \text{ MW}$ (Lighting, Security, Elevators, BMS).
*   $P_{total} = {{cookiecutter.it_capacity_mw}} + {{ (cookiecutter.it_capacity_mw | float * (cookiecutter.target_pue | float - 1.05)) | round(2) }} + 0.5 = {{ (cookiecutter.it_capacity_mw | float * cookiecutter.target_pue | float) | round(2) }} \text{ MW}$.

### Step 4: Total Apparent Power (MVA) for Transformer Sizing
Considering a worst-case operating Power Factor ($cos \phi$) of 0.95 at the {{cookiecutter.utility_voltage_kv}}kV utility entry:
$$S_{total} = \frac{P_{total}}{PF} = \frac{ {{ (cookiecutter.it_capacity_mw | float * cookiecutter.target_pue | float) | round(2) }} }{0.95} \approx {{ (cookiecutter.it_capacity_mw | float * cookiecutter.target_pue | float / 0.95) | round(2) }} \text{ MVA}$$

## 4. Equipment Selection & Diversity Factors
Unlike commercial buildings, AI Data Centres use very high diversity factors ($k$).

| Load Type | Diversity Factor ($k$) | Reasoning |
| :--- | :--- | :--- |
| **IT Load** | 1.0 | AI training runs at max capacity indefinitely. |
| **Cooling (CDUs/Pumps)** | 0.9 | High-density cooling must instantly match IT heat output. |
| **Lighting/General** | 0.8 | Not all areas are occupied simultaneously. |

## 5. AI-Specific Considerations
1.  **Harmonic Distortion:** AI power supplies are non-linear. Add a 15-20% margin to neutral conductor sizing unless a 3rd harmonic active filter is present.
2.  **Inrush Current:** When a {{cookiecutter.it_capacity_mw}} MW AI cluster restarts after a power failure, the concurrent inrush of thousands of power shelves can trip sensitive protection. Use "Sequential Start" logic in the EPMS.

## 6. Design Checklist
- [ ] Has the mechanical team confirmed the CDU (Coolant Distribution Unit) electrical power requirements?
- [ ] Is the diversity factor for AI racks set strictly to 1.0?
- [ ] Does the total MVA include a 10-15% margin for future GPU TDP increases by {{cookiecutter.ai_silicon_vendor}}?
- [ ] Have you accounted for BESS Battery Charging current in the total UPS input load?
