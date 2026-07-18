# Title: Transformer Design & Selection for AI Data Centres
## Purpose: To define the technical specifications, sizing, and selection criteria for transformers in a {{cookiecutter.it_capacity_mw}} MW AI-ready hyperscale facility.
## Project: {{cookiecutter.project_name}}
## Tags: #Transformers #Magnetics #K-Factor #{{cookiecutter.utility_voltage_kv}}kV #AI-Infrastructure
## Standards Covered: IEC 60076, IEEE C57.110, Local AHJ Codes

---

## 1. Overview
Transformers are the primary bottleneck for power delivery. In a {{cookiecutter.it_capacity_mw}} MW AI facility like {{cookiecutter.project_name}}, we deal with two types:
1.  **Main Power Transformers (MPT):** Stepping down from {{cookiecutter.utility_voltage_kv}} kV to Medium Voltage (e.g., 11kV / 22kV).
2.  **Distribution Transformers (DT):** Stepping down to Low Voltage (415V/480V) for the IT and Cooling loads.

AI loads introduce **non-sinusoidal currents**, leading to increased eddy current losses and skin effect, necessitating specific design adjustments (K-Rating).

## 2. Technical Selection Criteria

| Feature | Specification for AI Data Centres | Reasoning |
| :--- | :--- | :--- |
| **Type** | Cast Resin Dry Type (CRT) / VPI | Preferred for indoor DC use; Fire safe (Class F/H). |
| **Cooling** | AN (Air Natural) / AF (Air Forced) | AF allows for 25% temporary overloading during failure scenarios. |
| **Vector Group** | Dyn11 (or local standard) | Standard for distribution; provides neutral for LV. |
| **K-Factor** | K-13 (Minimum) | Handles harmonic heating from {{cookiecutter.ai_silicon_vendor}} Power Shelves. |
| **Impedance (Z%)** | 6% to 8% | Balance between fault level ({{cookiecutter.fault_level_ka}} kA) and voltage drop. |
| **Efficiency** | Highest Local Tier (e.g., NEMA Premium) | High efficiency is critical for the <{{cookiecutter.target_pue}} PUE target. |

## 3. Engineering Calculations

### 3.1 Sizing the Transformer for a Compute Block
In a block-redundant architecture, we typically feed standardized blocks (e.g., 2.5 MW IT load).

**Formula:**
$$S_{rating} = \frac{P_{total}}{PF \times \text{Loading Factor}}$$

**Worked Example (For a 2.5 MW Block):**
*   IT Load: 2500 kW
*   Cooling Load: ~750 kW
*   Target Operating Load: 75% (to allow for N+1 redundancy)
$$S = \frac{3250 \text{ kW}}{0.95 \times 0.75} \approx 4561 \text{ kVA}$$
*Standard Selection:* Use **2 x 2500 kVA** transformers in a 2N configuration or **3 x 2000 kVA** in N+1 per block.

### 3.2 K-Factor Calculation (IEEE C57.110)
{{cookiecutter.ai_silicon_vendor}} servers produce high 3rd, 5th, and 7th harmonics.
$$K = \sum I_h^2 h^2$$
Where $I_h$ is the per-unit current at harmonic $h$.
*If $K$ is not specified, the transformer must be heavily derated.* We specify **K-13** to ensure the transformer runs cool even with 100% non-linear AI loads.

## 4. Design Philosophy: AI-Ready Features
1.  **Electrostatic Shield:** A copper shield between Primary and Secondary windings to attenuate common-mode noise/transients from the grid.
2.  **Increased Neutral Sizing:** The neutral busbar and bushing must be rated for **200% of the phase current** to handle additive 3rd harmonics (Triplens).
3.  **Temperature Monitoring:** PT100 sensors in every winding linked to the BMS/EPMS.

## 5. Construction & Installation ({{cookiecutter.city}} Context)
*   **Corrosion:** Based on the {{cookiecutter.city}} environment, external hardware must be appropriately coated (e.g., SS316 or Hot-Dip Galvanized for coastal/industrial).
*   **Enclosure:** IP23/NEMA 1 for indoor Cast Resin units; IP55/NEMA 3R+ for outdoor units.
*   **Fire Mitigation:** Indoor transformers must be in fire-rated rooms per local AHJ. Oil-filled units require soak pits and active fire suppression.

## 6. Failure Modes
*   **Harmonic Overheating:** Winding insulation degrades due to undetected harmonic currents from AI rectifiers.
*   **Partial Discharge:** Voids in the cast resin of dry-type transformers leading to eventual flashover. *Mitigation:* Demand Factory Acceptance Testing (FAT) for PD.

## 7. Design Checklist
- [ ] Is the K-factor specified based on the expected THD-i of the {{cookiecutter.ai_silicon_vendor}} racks?
- [ ] Does the transformer room have sufficient airflow (CFM) to dissipate heat at {{cookiecutter.max_ambient_temp}}°C ambient?
- [ ] Are the cable/busduct terminations flexible (braided) to prevent vibration transfer?
