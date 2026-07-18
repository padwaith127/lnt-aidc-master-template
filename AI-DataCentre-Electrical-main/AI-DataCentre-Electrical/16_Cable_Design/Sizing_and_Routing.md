# Title: Cable Sizing, Selection & Routing Strategy
## Purpose: To define the engineering methodology for selecting, sizing, and routing HT and LT cables in a 40 MW AI-ready facility.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #CableSizing #VoltageDrop #De-rating #XLPE #CableTray #LTVyoma #NaviMumbai
## Related Files: [[LV_Switchgear.md]], [[Busbar_Distribution.md]], [[Short_Circuit.md]], [[Voltage_Drop.md]]
## Standards Covered: IS 7098 (Part 1 & 2), IEC 60287, IEC 60364-5-52, IS 732, IS 1255, CEA 2023

---

## 1. Overview
In a 40 MW facility, cables are the "nervous system." For the L&T Mahape project, cable design must move beyond basic current-carrying capacity. We must account for Mumbai's high ambient temperatures, the high-density nature of AI loads, and the thermal stress caused by harmonic currents. This module covers both HT (11kV/33kV) and LT (0.415kV) cabling.

## 2. Selection Criteria: The "L&T Standard"
For hyperscale AI DCs, we standardize on the following:
*   **Conductor:** Electrolytic Grade Aluminum (Main Feeders) or Copper (AI Racks/Control).
*   **Insulation:** XLPE (Cross-linked Polyethylene) - Rated for 90°C continuous/250°C short-circuit.
*   **Outer Sheath:** FR-LSH (Flame Retardant Low Smoke Low Halogen) or LSZH (Low Smoke Zero Halogen) to meet NBC 2016 safety norms.
*   **Armouring:** Galvanized Steel Wire/Strip (for multi-core) or Aluminum (for single-core) to prevent mechanical damage and provide an earth path.

## 3. Engineering Calculations: The 4-Step Sizing Process

To size a cable correctly, it must pass **four independent checks**. If it fails one, you must increase the size.

### 3.1 Check 1: Continuous Current Carrying Capacity ($I_z$)
The cable must handle the load current ($I_b$) after applying derating factors ($k$).
*   **Formula:** $I_z \geq \frac{I_b}{k_1 \cdot k_2 \cdot k_3 \cdot k_4}$
*   **Derating Factors for Mahape:**
    *   $k_1$ (Ambient Temp): 0.82 (for 50°C Air temp, baseline 40°C).
    *   $k_2$ (Grouping): 0.70 (if 6 cables are laid touching on a tray).
    *   $k_3$ (Ground Temp): 0.85 (if buried).
    *   $k_4$ (Thermal Resistivity of Soil): Critical for HT cables in Mahape industrial soil.

### 3.2 Check 2: Voltage Drop ($\Delta V$)
High-density AI racks are sensitive to undervoltage.
*   **Formula:** $\Delta V = \frac{\sqrt{3} \cdot I \cdot (R \cos \phi + X \sin \phi) \cdot L}{V_{sys} \cdot n}$
*   **Limit:** $< 3\%$ from Transformer to Main Panel; $< 5\%$ total to the Rack.
*   $n$ = Number of runs per phase.

### 3.3 Check 3: Short Circuit Withstand
The cable insulation must not melt during a fault before the breaker trips.
*   **Formula:** $A = \frac{I_{sc} \cdot \sqrt{t}}{k}$
*   **Example:** For $I_{sc} = 50kA$ and $t = 0.1s$ (breaker trip time), and $k=143$ for Copper/XLPE:
    $$A = \frac{50,000 \cdot \sqrt{0.1}}{143} \approx 110.5 \text{ sq.mm per run.}$$

### 3.4 Check 4: Harmonic Adjustment (The AI Factor)
AI loads generate high THDi. Per **IEC 60364-5-52**, if THD is $> 15\%$, the Neutral conductor must be sized as a phase conductor. If THD is $> 33\%$, the cable must be upsized to account for Neutral heating.

## 4. Worked Example: Sizing a 1.5 MW UPS Input
*   **Load:** 1500 kW at 415V, PF 0.95.
*   **Current ($I_b$):** $\approx 2200 \text{ A}$.
*   **Cable:** 3.5C x 300 sq.mm Aluminum XLPE FR-LSH.
*   **Base Rating (on tray):** ~450 A per cable.
*   **Derated Rating:** $450 \cdot 0.82 \text{ (Temp)} \cdot 0.75 \text{ (Grouping)} \approx 276 \text{ A}$.
*   **Number of Runs Required:** $2200 / 276 \approx 8 \text{ runs}$.
*   **Selection:** 8 Runs of 3.5C x 300 sq.mm Aluminum XLPE cable per phase.

## 5. Routing & Containment Strategy
In Mahape, spatial coordination is the biggest challenge due to the density of liquid cooling pipes.
*   **Cable Trays:** Use Hot-Dip Galvanized (HDG) Ladder trays for power and Perforated trays for control/signal.
*   **Separation:** 
    *   Maintain 300mm gap between HV (11kV) and LV (415V) trays.
    *   Maintain 600mm gap between Power and Data (Fiber/Copper) to prevent EMI.
*   **Fill Ratio:** Maximum 40-50% fill (as per NEC) to allow for airflow and heat dissipation.
*   **Vertical Risers:** Use "Cable Cleats" every 1 meter to support the weight of XLPE cables in shafts.

## 6. AI-Ready Construction Best Practices
1.  **Bending Radius:** XLPE cables are stiff. Strictly enforce $12 \times D$ (where D is overall diameter) to prevent insulation stress.
2.  **Fire Sealing:** Every tray penetration through a wall must be sealed using **UL-listed Fire Stop Mortar** or **MCT (Multi-Cable Transits)**.
3.  **Phase Identification:** Strictly follow Red-Yellow-Blue-Black (Neutral) and Green/Yellow (Earth) per IS 732.
4.  **Terminations:** Use double-compression brass lugs and bimetallic washers when connecting Aluminum cables to Copper busbars to prevent galvanic corrosion.

## 7. Commissioning & Testing
1.  **Continuity & Phasing:** Ensure L1-L2-L3 consistency across the facility.
2.  **Insulation Resistance (Megger):**
    *   LV (415V): Use 1kV Megger (Target > 100 MΩ).
    *   HV (11kV): Use 5kV Megger (Target > 2000 MΩ).
3.  **Hi-Pot Test (for HT):** Very low frequency (VLF) AC testing is now preferred over DC Hi-pot to prevent XLPE water-treeing.

## 8. Failure Modes
*   **Thermal Meltdown:** Occurs when derating factors are ignored in a high-density AI room.
*   **Termination Failure:** Loose lugs leading to "Hot Spots."
*   **Cable Strike:** Accidental drilling/digging. *Mitigation:* Clear labeling and "Danger" tiles for buried cables.

---

## 9. Design Checklist
- [ ] Have ambient temperature derating factors (50°C) been applied?
- [ ] Is the short-circuit rating coordinated with the breaker trip time?
- [ ] Has the Neutral conductor been sized for 200% or 100% based on THDi?
- [ ] Are bimetallic lugs specified for Al-to-Cu joints?
- [ ] Is the cable tray loading within structural limits?

---
## 📚 References
### Standards
* **IS 7098:** XLPE Insulated PVC Sheathed Cables.
* **IS 1255:** Code of Practice for Installation and Maintenance of Power Cables.
* **IEC 60287:** Electric cables - Calculation of the current rating.
* **IS 732:** Code of Practice for Electrical Wiring Installations.

### Manufacturer Documents
* **Polycab / Finolex / Havells:** "Technical Handbook on Power Cables."
* **Prysmian / Nexans:** "Data Center High Performance Cabling Guide."

### Revision History
* 1.0: Initial setup for L&T Vyoma Mahape Cable Infrastructure.

---
**Next File Recommendation:** `17_Earthing/Grounding_Grid_Design.md` (Focusing on the critical "Clean Earth" and "Power Earth" grid for the 40 MW plant).