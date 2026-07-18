# Title: Earthing & Grounding Grid Design for AI Data Centres
## Purpose: To define the engineering requirements for a comprehensive earthing system that ensures personnel safety (Power Earth) and signal integrity (Clean Earth) for high-density AI clusters.
## Project: {{cookiecutter.project_name}}
## Tags: #Earthing #Grounding #IEEE80 #SignalReferenceGrid #CleanEarth #{{cookiecutter.city}}
## Standards Covered: IEEE 80, IEEE 81, IEEE 1100 (Emerald Book), Local Electrical Codes

---

## 1. Overview
In a {{cookiecutter.it_capacity_mw}} MW hyperscale facility, the earthing system is not merely a safety requirement; it is a fundamental component of the high-speed data environment. For {{cookiecutter.ai_silicon_vendor}} GPU clusters, electromagnetic interference (EMI) and high-frequency noise can lead to "Silent Data Corruption" or GPU link failures. We utilize a **Common Bonding Network (CBN)** with a dedicated **Signal Reference Grid (SRG)** to ensure equipotentiality across the entire facility.

## 2. Design Philosophy: The "Dual-Purpose" Earth
For the {{cookiecutter.project_name}}, the system fulfills two distinct roles:
1.  **Safety Earthing (Power Earth):** To provide a low-impedance path for fault currents (50/60Hz) to prevent electric shock (Step/Touch Potential).
2.  **Functional Earthing (Clean/Signal Earth):** To provide a high-frequency reference (MHz) for sensitive AI electronics, minimizing noise between the GPU chassis and the networking fabric.

## 3. Engineering Calculations: Grid Sizing (IEEE 80)
To design the grid for the {{cookiecutter.it_capacity_mw}} MW site, we follow the IEEE 80 process.

### 3.1 Step 1: Soil Resistivity ($\rho$)
*   **Measurement Technique:** Wenner Four-Pin Method (per IEEE 81) conducted at the {{cookiecutter.city}} site.
*   **Design Value:** Use the worst-case (highest) resistivity from the soil model (accounting for seasonal dry/wet variations in {{cookiecutter.state}}).

### 3.2 Step 2: Fault Current Sizing ($I_G$)
The conductor must not melt during a {{cookiecutter.utility_voltage_kv}}kV fault ({{cookiecutter.fault_level_ka}} kA).
*   **Formula:** $A_{mm^2} = I \times \frac{1}{\sqrt{\frac{TCAP \times 10^{-4}}{t_c \cdot \alpha_r \cdot \rho_r} \ln \left( \frac{K_0 + T_m}{K_0 + T_a} \right)}}$
*   **Sizing:** Select appropriate Copper or Galvanized Steel flats based on the {{cookiecutter.fault_level_ka}} kA / 1s requirement.

### 3.3 Step 3: Tolerable Touch ($E_{touch}$) and Step ($E_{step}$) Voltages
Calculated based on human body weight and surface layer resistivity (e.g., crushed rock).
*   **Goal:** $E_{mesh} < E_{touch}$ and $E_s < E_{step}$.

## 4. Signal Reference Grid (SRG) for AI Racks
AI servers communicate at extremely high speeds. High-frequency noise is common-mode; it travels on the grounding system.
*   **Design:** A mesh of 2' x 2' or 4' x 4' copper strips laid under the raised floor.
*   **Integration:** Every {{cookiecutter.ai_silicon_vendor}} rack is bonded to the SRG at multiple points using short, flat, braided copper jumpers.
*   **Target Resistance:** Overall system resistance must be **< 1.0 $\Omega$** (Hyperscale Standard).

## 5. Equipment & Materials Selection
*   **Main Grid Conductor:** Buried at 600mm - 1000mm depth.
*   **Earth Electrodes:** Copper Bonded Steel for superior corrosion resistance.
*   **Joints:** Exothermic Welding (Cadweld). Mechanical clamps are prohibited for buried joints in hyperscale DCs.

## 6. Failure Modes & Risks
*   **Step/Touch Potential Hazard:** Occurs if the grid is too small for the {{cookiecutter.fault_level_ka}} kA fault current, leading to GPR (Ground Potential Rise).
*   **Ground Loops:** Caused by multiple paths between SRG and Power Earth. *Mitigation:* Use a Single-Point Grounding (SPG) window for sensitive instrument subsystems.

## 7. Design Checklist
- [ ] Has the soil resistivity been measured on-site at {{cookiecutter.city}}?
- [ ] Is the overall resistance calculated to be < 1.0 $\Omega$?
- [ ] Are all joints below-grade exothermically welded?
- [ ] Is there an SRG mesh provided in the {{cookiecutter.ai_silicon_vendor}} white space?
