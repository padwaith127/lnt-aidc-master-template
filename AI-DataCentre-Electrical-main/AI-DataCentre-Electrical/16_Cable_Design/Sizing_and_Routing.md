# Title: Cable Sizing, Selection & Routing Strategy
## Purpose: To define the engineering methodology for selecting, sizing, and routing HT and LT cables in the {{cookiecutter.it_capacity_mw}} MW AI-ready facility.
## Tags: #CableSizing #VoltageDrop #De-rating #XLPE #CableTray
## Standards Covered: IEC 60287, IEC 60364-5-52, Local Wire Regulations

---

## 1. Overview
In a {{cookiecutter.it_capacity_mw}} MW facility, cables are the "nervous system." Cable design must account for {{cookiecutter.city}}'s high ambient temperatures, the high-density nature of AI loads, and the thermal stress caused by harmonic currents. 

## 2. Selection Criteria
*   **Conductor:** Electrolytic Grade Aluminum (Main Feeders) or Copper (AI Racks/Control).
*   **Insulation:** XLPE (Cross-linked Polyethylene) - Rated for 90°C continuous/250°C short-circuit.
*   **Outer Sheath:** LSZH (Low Smoke Zero Halogen) or FR-LSH to meet strict data centre fire codes.

## 3. Engineering Calculations: The 4-Step Sizing Process
To size a cable correctly, it must pass **four independent checks**. 

### 3.1 Check 1: Continuous Current Carrying Capacity ($I_z$)
The cable must handle the load current ($I_b$) after applying derating factors ($k$).
*   **Formula:** $I_z \geq \frac{I_b}{k_1 \cdot k_2 \cdot k_3 \cdot k_4}$
*   **Derating Factors for {{cookiecutter.city}}:**
    *   $k_1$ (Ambient Temp): Based on {{cookiecutter.max_ambient_temp}}°C Air temp.
    *   $k_2$ (Grouping): Factor based on how many cables are touching on a tray.
    *   $k_3$ (Ground Temp): If buried in the HT yard.
    *   $k_4$ (Thermal Resistivity of Soil): Critical for buried cables.

### 3.2 Check 2: Voltage Drop ($\Delta V$)
High-density {{cookiecutter.ai_silicon_vendor}} racks are sensitive to undervoltage.
*   **Formula:** $\Delta V = \frac{\sqrt{3} \cdot I \cdot (R \cos \phi + X \sin \phi) \cdot L}{V_{sys} \cdot n}$
*   **Limit:** $< 3\%$ from Transformer to Main Panel; $< 5\%$ total to the Rack.

### 3.3 Check 3: Short Circuit Withstand
The cable insulation must not melt during a fault before the breaker trips.
*   **Formula:** $A = \frac{I_{sc} \cdot \sqrt{t}}{k}$
*   **Example:** For $I_{sc} = {{cookiecutter.fault_level_ka}} kA$ and $t = 0.1s$.

### 3.4 Check 4: Harmonic Adjustment (The AI Factor)
AI loads generate high THDi. Per **IEC 60364-5-52**, if THD is $> 15\%$, the Neutral conductor must be sized as a phase conductor. If THD is $> 33\%$, the cable must be upsized to account for extreme Neutral heating.

## 4. Routing & Containment Strategy
Spatial coordination is a massive challenge due to the density of Liquid Cooling pipes.
*   **Separation:** 
    *   Maintain 300mm gap between HV and LV trays.
    *   Maintain 600mm gap between Power and Data (Fiber/Copper) to prevent EMI on the AI compute fabric.
*   **Fill Ratio:** Maximum 40-50% fill to allow for airflow and heat dissipation.

## 5. Construction Best Practices
1.  **Bending Radius:** Strictly enforce $12 \times D$ to prevent XLPE insulation stress.
2.  **Fire Sealing:** Every tray penetration through a wall must be sealed using **UL-listed Fire Stop Mortar** or **MCT (Multi-Cable Transits)**.
3.  **Terminations:** Use double-compression brass lugs and bimetallic washers when connecting Aluminum cables to Copper busbars to prevent galvanic corrosion.

## 6. Design Checklist
- [ ] Have ambient temperature derating factors ({{cookiecutter.max_ambient_temp}}°C) been strictly applied?
- [ ] Is the short-circuit rating coordinated with the breaker trip time?
- [ ] Has the Neutral conductor been sized for 200% or 100% based on THDi?
- [ ] Are bimetallic lugs specified for Al-to-Cu joints?
