# Title: AI Load Estimation & Power Density Calculation
## Purpose: To calculate the total facility power requirement for a 40 MW IT-load AI-ready data centre.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #LoadCalculation #AI-Ready #NVIDIA #CapacityPlanning #PUE
## Related Files: [[Design_Basis_Report.md]], [[NVIDIA_Architecture.md]], [[Cooling_Electrical.md]]
## Standards Covered: IEEE 3001.2, TIA-942-C, ASHRAE TC 9.9

---

## 1. Overview
In a traditional data centre, load estimation is often based on an average density per rack (e.g., 5-10 kW). In an **AI-Ready 40 MW facility**, the calculation shifts toward **Cluster-Based Loading**. We must account for the extreme power draw of GPU clusters (NVIDIA H100/B200) and the specific auxiliary loads required to keep them operational (Liquid Cooling CDUs).

## 2. Theoretical Basis: AI Load Characteristics
AI workloads (Large Language Model training) differ from cloud workloads:
1.  **High Utilization:** AI clusters often run at 80-90% TDP (Thermal Design Power) for weeks.
2.  **Transients:** Power can swing from 10% to 100% in milliseconds during model "checkpointing."
3.  **Power Factor:** Modern AI power shelves use active PFC, resulting in a PF near 0.99.

## 3. Engineering Calculation: Total Facility Load (MVA)

To determine the utility transformer capacity, we use the "Inside-Out" method.

### Step 1: IT Load Breakdown
*   **Total Target IT Load:** 40,000 kW (40 MW).
*   **AI High-Density Zone (80%):** 32,000 kW (supporting ~320 racks at 100kW or ~800 racks at 40kW).
*   **Standard Compute Zone (20%):** 8,000 kW (supporting ~800 racks at 10kW).

### Step 2: Cooling Load Calculation (Mechanical Load)
For AI-ready sites, we assume a mix of Liquid Cooling (Direct-to-Chip) and Air Cooling.
*   **Target PUE (Power Usage Effectiveness):** 1.35
*   **Mechanical Load Calculation Formula:**
    $$P_{mech} = P_{IT} \times (PUE - 1.0 - Loss_{elec})$$
    *   *Assumption:* Electrical distribution losses ($Loss_{elec}$) are ~5% (0.05).
    *   $P_{mech} = 40,000 \times (1.35 - 1.0 - 0.05) = 40,000 \times 0.30 = 12,000 \text{ kW}$.

### Step 3: Total Facility Active Power (kW)
$$P_{total} = P_{IT} + P_{mech} + P_{admin/misc}$$
*   $P_{admin/misc} \approx 500 \text{ kW}$ (Lighting, Security, Elevators, BMS).
*   $P_{total} = 40,000 + 12,000 + 500 = 52,500 \text{ kW} (52.5 \text{ MW})$.

### Step 4: Total Apparent Power (MVA) for Transformer Sizing
Considering a worst-case operating Power Factor ($cos \phi$) of 0.95 at the utility entry:
$$S_{total} = \frac{P_{total}}{PF} = \frac{52,500}{0.95} \approx 55,263 \text{ kVA} \approx 55.3 \text{ MVA}$$

## 4. Equipment Selection & Diversity Factors
Unlike commercial buildings, Data Centres use very high diversity factors ($k$).

| Load Type | Diversity Factor ($k$) | Reasoning |
| :--- | :--- | :--- |
| **IT Load** | 1.0 | AI training runs at max capacity indefinitely. |
| **Cooling (CDUs/Pumps)** | 0.9 | High-density cooling must match IT heat output. |
| **Lighting/General** | 0.8 | Not all areas are occupied simultaneously. |

**Recommended Transformer Configuration for 40MW IT / 55MVA Total:**
*   **Option A:** 3 x 25/30 MVA Transformers (N+1 arrangement).
*   **Option B:** 4 x 20 MVA Transformers (N+1 arrangement).
*   *L&T Preference:* Option B is often preferred for better granularity and lower fault levels on the LV bus.

## 5. Worked Example: Single AI Rack Power Feed
**Scenario:** Sizing the feed for an NVIDIA Blackwell NVL72 Rack.
*   **Rack TDP:** 120 kW.
*   **Voltage:** 415V, 3-Phase.
*   **Current Calculation:**
    $$I = \frac{P}{\sqrt{3} \times V \times PF} = \frac{120,000}{1.732 \times 415 \times 0.99} \approx 169 \text{ Amperes}$$
*   **Circuit Breaker Selection:** 250A (to allow for 125% continuous load rating per NEC Art 645).
*   **Cable/Busway:** 250A or 400A overhead busway plug-in unit.

## 6. AI-Specific Considerations
1.  **Harmonic Distortion:** AI power supplies are non-linear. Add a 15-20% margin to neutral conductor sizing unless a 3rd harmonic filter is present.
2.  **Inrush Current:** When a 40MW AI cluster restarts after a power failure, the concurrent inrush of thousands of power shelves can trip sensitive protection. Use "Sequential Start" logic in the EPMS.

## 7. Design Checklist
- [ ] Has the mechanical team confirmed the CDU (Coolant Distribution Unit) power requirements?
- [ ] Is the diversity factor for AI racks set to 1.0?
- [ ] Does the total MVA include a 10-15% margin for future GPU TDP increases?
- [ ] Have you accounted for Battery Charging current in the total UPS input load?

---
## 📚 References
### Standards
* **IEEE 3001.2:** Recommended Practice for Load Analysis.
* **ASHRAE TC 9.9:** Thermal Guidelines for Data Processing Environments.

### Research Papers
* **NVIDIA White Paper:** "Powering the Next Era of AI - Blackwell Infrastructure."
* **Schneider Electric WP #513:** "AI Impact on Data Center Design."

### Revision History
* 1.0: Initial Load Estimation for Mahape 40MW AI DC.