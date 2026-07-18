# Title: Transformer Design & Selection for AI Data Centres
## Purpose: To define the technical specifications, sizing, and selection criteria for transformers in a 40 MW AI-ready hyperscale facility.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #Transformers #Magnetics #K-Factor #StepDown #Substation #AI-Infrastructure
## Related Files: [[Utility_Interface.md]], [[HT_System.md]], [[Harmonics.md]]
## Standards Covered: IS 2026, IEC 60076, IEEE C57.110, NBC 2016, CEA 2023

---

## 1. Overview
Transformers are the primary bottleneck for power delivery. In a 40 MW AI facility like Mahape, we deal with two types:
1.  **Main Power Transformers (MPT):** Stepping down from 110kV/33kV to 11kV.
2.  **Distribution Transformers (DT):** Stepping down from 11kV/33kV to 415V for the IT and Cooling loads.

AI loads introduce **non-sinusoidal currents**, leading to increased eddy current losses and skin effect, necessitating specific design adjustments (K-Rating).

## 2. Technical Selection Criteria

| Feature | Specification for AI Data Centres | Reasoning |
| :--- | :--- | :--- |
| **Type** | Cast Resin Dry Type (CRT) / VPI | Preferred for indoor DC use; Fire safe (Class F/H). |
| **Cooling** | AN (Air Natural) / AF (Air Forced) | AF allows for 25% temporary overloading. |
| **Vector Group** | Dyn11 | Standard for distribution; provides neutral for LT. |
| **K-Factor** | K-13 (Minimum) | Handles harmonic heating from AI Power Shelves. |
| **Impedance (Z%)** | 6% to 8% | Balance between fault level and voltage drop. |
| **Efficiency** | IE EMA / IS 1180 Level 2/3 | High efficiency is critical for PUE targets. |

## 3. Engineering Calculations

### 3.1 Sizing the Transformer for a 2.5 MW Block
In a block-redundant or 2N architecture, we typically feed blocks of 2.5 MW IT load.

**Assumptions:**
*   IT Load: 2500 kW
*   Cooling Load (PUE 1.3): 750 kW
*   Total Load: 3250 kW
*   Target Operating Load: 75% (to allow for N+1 redundancy)

**Formula:**
$$S_{rating} = \frac{P_{total}}{PF \times \text{Loading Factor}}$$

**Worked Example:**
$$S = \frac{3250 \text{ kW}}{0.98 \times 0.75} = \frac{3250}{0.735} \approx 4421 \text{ kVA}$$
*Standard Selection:* Use **2 x 2500 kVA** transformers in a 2N configuration or **3 x 2000 kVA** in N+1.

### 3.2 K-Factor Calculation (IEEE C57.110)
AI servers produce high 3rd, 5th, and 7th harmonics.
$$K = \sum I_h^2 h^2$$
Where $I_h$ is the per-unit current at harmonic $h$.
*If $K$ is not specified, the transformer must be derated.* For the L&T Mahape project, we specify **K-13** to ensure the transformer runs cool even with 100% non-linear AI loads.

## 4. Design Philosophy: AI-Ready Features
1.  **Electrostatic Shield:** A copper shield between Primary and Secondary windings to attenuate common-mode noise/transients from the grid.
2.  **Increased Neutral Sizing:** The neutral busbar and bushing must be rated for **200% of the phase current** to handle additive 3rd harmonics (Triplens).
3.  **Temperature Monitoring:** PT100 sensors in every winding linked to the BMS/EPMS.
4.  **Inrush Current Management:** High-density AI power shelves have high capacitance. Transformers must be designed to withstand frequent inrush during "Return to Utility" events.

## 5. Construction & Installation (Mumbai Specific)
*   **Corrosion:** Since Mahape is near the coast, all external hardware, bolts, and marshaling boxes must be **Stainless Steel (SS316)** or Hot-Dip Galvanized.
*   **Enclosure:** IP23 for indoor Cast Resin units; IP55/65 for outdoor oil-filled units.
*   **Fire Mitigation (Regulation 48 of CEA):**
    *   Indoor transformers must be in a 2-hour fire-rated room.
    *   If oil-filled (>2000L), a soak pit and NIFPS (Nitrogen Injection) are mandatory.

## 6. Testing Requirements (IS 2026 / IEC 60076)
Before accepting a unit from ABB, Siemens, or Schneider, witness these tests:
1.  **Routine Tests:** Ratio, Polarity, Insulation Resistance, No-load/Load losses.
2.  **Type Tests:** Temperature rise test (Critical for K-factor validation).
3.  **Special Tests:** Partial Discharge (for CRT), Noise Level test (Max 65-70 dB).

## 7. Failure Modes
*   **Harmonic Overheating:** Winding insulation degrades due to undetected harmonic currents.
*   **Insulation Breakdown:** Due to high humidity in Mumbai during the monsoon.
*   **Partial Discharge:** Voids in the cast resin of dry-type transformers leading to eventual flashover.

---

## 8. Design Checklist
- [ ] Is the K-factor specified based on the expected THD-i of the NVIDIA racks?
- [ ] Does the transformer room have sufficient airflow (CFM) to dissipate 2% of the transformer's heat (Losses)?
- [ ] Are the cable/busduct terminations flexible (braided) to prevent vibration transfer?
- [ ] Has the Vector Group (Dyn11) been confirmed for local earthing compatibility?

---
## 📚 References
### Standards
* **IS 2026:** Power Transformers (Indian Standard).
* **IEC 60076:** Power Transformers (International).
* **IEEE C57.110:** Recommended Practice for Establishing Liquid-Filled and Dry-Type Power Transformer Capability when Supplying Nonsinusoidal Load Currents.

### Manufacturer Documents
* **Schneider Electric:** "Trihal Cast Resin Transformer Technical Guide."
* **ABB:** "Transformers for Data Centers - Application Guide."

### Revision History
* 1.0: Initial spec for 40 MW AI DC Transformer strategy.

---
**Next File Recommendation:** `05_HT_System/HT_Switchgear.md` (Focusing on the 33kV/11kV Protection and Distribution).