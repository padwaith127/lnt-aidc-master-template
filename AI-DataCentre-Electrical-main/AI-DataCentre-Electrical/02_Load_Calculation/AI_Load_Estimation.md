# Title: AI Load Estimation & Power Density Calculation
## Purpose: To calculate the total facility power requirement for a {{cookiecutter.it_capacity_mw}} MW IT-load AI-ready data centre.
## Tags: #LoadCalculation #AI-Ready #{{cookiecutter.ai_silicon_vendor}} #CapacityPlanning #PUE

---

## 1. Overview
In an **AI-Ready {{cookiecutter.it_capacity_mw}} MW facility**, the calculation shifts toward **Cluster-Based Loading** to support the extreme power draw of {{cookiecutter.ai_silicon_vendor}} AI clusters.

## 2. Engineering Calculation: Total Facility Load (MVA)

### Step 1: IT Load
*   **Total Target IT Load:** {{cookiecutter.it_capacity_mw}} MW ({{cookiecutter.it_capacity_mw | float * 1000}} kW).

### Step 2: Cooling Load Calculation (Mechanical Load)
*   **Target PUE:** {{cookiecutter.target_pue}}
*   **Mechanical Load Formula:** $P_{mech} = P_{IT} \times (PUE - 1.0 - Loss_{elec})$
*   *Assuming electrical losses = 5% (0.05)*
*   $P_{mech} = {{cookiecutter.it_capacity_mw}} \times ({{cookiecutter.target_pue}} - 1.05) = {{ (cookiecutter.it_capacity_mw | float * (cookiecutter.target_pue | float - 1.05)) | round(2) }} \text{ MW}$.

### Step 3: Total Facility Active Power (MW)
$$P_{total} = P_{IT} + P_{mech} + P_{misc}$$
*   $P_{total} = {{ (cookiecutter.it_capacity_mw | float * cookiecutter.target_pue | float) | round(2) }} \text{ MW}$.

### Step 4: Total Apparent Power (MVA)
Assuming a worst-case Power Factor of 0.95 at the {{cookiecutter.utility_voltage_kv}} kV utility entry:
*   Total MVA = {{ (cookiecutter.it_capacity_mw | float * cookiecutter.target_pue | float / 0.95) | round(2) }} MVA.
