# Title: Standard Layouts & Spatial Planning for AI-Ready DCs
## Purpose: To define the physical architecture, equipment placement logic, and spatial coordination requirements for a {{ cookiecutter.it_capacity_mw }} MW AI-ready hyperscale facility.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #DataCentreLayout #SpatialPlanning #SubstationLayout #WhiteSpace #AIRack #{{ cookiecutter.project_code }} #{{ cookiecutter.city }}
## Related Files: [[HT_Switchgear.md]], [[LV_Switchgear.md]], [[Transformer_Design.md]], [[GPU_Infrastructure_Requirements.md]]
## Standards Covered: TIA-942-B, CEA 2023, NBC 2016, ASHRAE TC 9.9

---

## 1. Overview
Spatial planning in a {{ cookiecutter.it_capacity_mw }} MW AI facility is a multi-dimensional puzzle. For the {{ cookiecutter.project_name }} {{ cookiecutter.city }} project, the layout must minimize "Electrical Impedance" by keeping high-density AI racks close to their power source, while managing the massive footprint of the mechanical cooling plant. This module defines the "Gold Standard" layouts for each major zone of the facility.

## 2. Spatial Logic: The "Power-to-Load" Proximity Rule
In high-density AI design, long LT (415V/480V) cable or busduct runs are the enemy. They increase voltage drop and $I^2R$ heat losses.
*   **The Vertical Strategy:** If the DC is a multi-story building, transformers and UPS systems are placed on the floor directly above or below the Data Hall.
*   **The Modular Block:** The {{ cookiecutter.it_capacity_mw }} MW facility is divided into 2.5 MW or 5 MW "Power Blocks." Each block has its own dedicated Transformer, UPS, and Battery room.

## 3. Zone 1: HT Yard & Substation (The Utility Entry)
In {{ cookiecutter.city }}, due to local environmental conditions (e.g., humidity, dust, or coastal salt air), **GIS (Gas Insulated Switchgear)** is the standard to prevent flashovers.
*   **Layout:**
    *   Utility Gantry ({{ cookiecutter.utility_voltage_kv }}kV).
    *   Primary Power Transformers (Oil-filled, located outdoors).
    *   GIS Room (Indoor, pressurized, air-conditioned).
    *   **Clearance:** Minimum 6-meter road access around the yard for fire tenders and transformer replacement.

## 4. Zone 2: The Power Train (Transformer & UPS Rooms)
Each 2.5 MW IT block typically follows this layout:
*   **Transformer Room:** 2-hour fire-rated walls. Transformer positioned for direct busduct exit.
*   **LV Switchgear (PCC) Room:** Adjacent to the transformer to minimize "Low Voltage" run lengths.
*   **UPS Room:** Separated from the Battery room. Air-conditioned to 25°C.
*   **Battery (BESS) Room:** Strictly controlled to 20°C - 23°C. Lithium-ion cabinets require 900mm spacing between rows per **NFPA 855**.

## 5. Zone 3: The AI Data Hall (White Space)
For {{ cookiecutter.ai_silicon_vendor }} infrastructure, the layout shifts from "Air-First" to "Liquid-First."

| Component | Placement Logic |
| :--- | :--- |
| **AI Racks** | Arranged in Hot/Cold Aisle Containment. |
| **CDU (Coolant Unit)** | Placed at the end of every row (EoR) or integrated in-row. |
| **Overhead Busway** | Mounted directly above the rack power shelves (Source A & B). |
| **CRAH Units** | Peripheral placement for air-cooling the non-liquid heat (20%). |
| **Cable Trays** | Multi-tier: Data on top, Fiber in the middle, Control on the bottom. |

### 5.1 The "Aisle" Geometry
*   **Cold Aisle:** 1200mm to 1500mm wide (to allow for CDU maintenance and rack maneuvering).
*   **Hot Aisle:** 1200mm wide (primarily for rear-access DC busbar maintenance).

## 6. Engineering Criteria: Floor Loading & Clearance

### 6.1 Weight Management (Structural-Electrical Interface)
{{ cookiecutter.ai_silicon_vendor }} racks weigh ~2,500 kg.
*   **Layout Requirement:** If using a raised floor, the pedestals must be on a 600mm x 600mm grid with heavy-duty "Bolted Stringers." 
*   **Preferred Design:** "Slab-on-Grade" (no raised floor) with overhead distribution is the current hyperscale trend for {{ cookiecutter.it_capacity_mw }} MW+ sites to handle the extreme floor loading.

### 6.2 Regulatory Clearances (CEA 2023)
*   **Main PCCs:** Front clearance of 2000mm is mandatory for 4000A ACB withdrawal.
*   **Working Space:** A minimum of 1000mm clear working space around all live parts.

## 7. AI-Ready Design Features
1.  **Pressure Relief Vents:** In rooms with Gas Suppression (Module 29), the layout must include "Over-pressure Vents" to prevent structural damage during a gas discharge.
2.  **Drip-Zone Avoidance:** The electrical layout must be "Zoned" such that no water/coolant pipes pass directly over Switchgear or UPS systems.
3.  **Expansion Gaps:** Leave 15% physical "White Space" for future "Compute Density Upgrades" (e.g., swapping legacy GPUs for next-gen {{ cookiecutter.ai_silicon_vendor }}).

## 8. Construction & Coordination (BIM Workflow)
*   **LOD 400 Modeling:** All layouts must be verified in 3D.
*   **Pull Zones:** In the 3D model, represent the "Breaker Pull Zone" and "Module Pull Zone" as transparent red boxes to ensure no pipes are routed through them.

## 9. Failure Modes in Layouts
*   **Thermal Recirculation:** Placing CRAH units such that they "short-circuit" their own cold air back to the return.
*   **Bottlenecking:** Narrow corridors ( < 2m) preventing the replacement of a failed 2.5 MW transformer or a 1.5 MW UPS frame.
*   **EMI Interference:** Placing high-power transformers too close to the "Network Core" room, causing magnetic interference with fiber-optic transceivers.

---

## 10. Design Checklist
- [ ] Are HT and LT rooms located above the 100-year flood level?
- [ ] Does the Data Hall layout support the weight of 2500kg AI racks?
- [ ] Is there a clear path for equipment replacement (Rigging Path)?
- [ ] Are transformer rooms 2-hour fire-rated?
- [ ] Is the "Drip Zone" rule enforced in the MEP coordination?

---
## 11. References
### Standards
* **TIA-942-B:** Telecommunications Infrastructure Standard for Data Centers.
* **NBC 2016:** National Building Code of India (Building Planning & Electrical).
* **ASHRAE TC 9.9:** Data Center Thermal Guidelines.
* **CEA 2023:** Safety measures for electrical layouts.

### Manufacturer Documents
* **Schneider Electric:** "Optimizing Data Center Layouts for High Density."
* **Vertiv:** "Standard Reference Designs for Hyperscale Facilities."

### Revision History
* 1.0: Initial Layout Standards for {{ cookiecutter.project_name }} {{ cookiecutter.city }} project.

---
**Next File Recommendation:** `Annotated_Bibliography.md` (A curated list of the must-read technical papers to master the AI DC domain).
