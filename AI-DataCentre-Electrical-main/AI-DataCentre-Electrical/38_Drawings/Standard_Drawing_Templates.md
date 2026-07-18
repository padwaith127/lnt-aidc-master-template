# Title: Standard Engineering Drawing Templates & Documentation
## Purpose: To define the technical requirements, symbology, and structure for the electrical drawing package of a {{ cookiecutter.it_capacity_mw }} MW AI-ready facility.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #EngineeringDrawings #SLD #BIM #AutoCAD #Revit #LOD400 #{{ cookiecutter.project_code }}
## Related Files: [[HT_Switchgear.md]], [[LV_Switchgear.md]], [[Sizing_and_Routing.md]], [[Grounding_Grid_Design.md]]
## Standards Covered: IEC 60617, ISO 13567, IEEE 315, ANSI Y32.2, CEA 2023, NBC 2016

---

## 1. Overview
In a {{ cookiecutter.it_capacity_mw }} MW hyperscale project, drawings are the primary contract between the design office and the construction site. For the {{ cookiecutter.project_name }} {{ cookiecutter.city }} project, a standard 2D drawing approach is insufficient. We utilize a **BIM (Building Information Modeling)** workflow at **LOD 400 (Level of Development)** to ensure that electrical busducts, HT cables, and massive liquid cooling pipes do not clash.

## 2. The Drawing Hierarchy (The "Package")

| Drawing Type | Purpose | Level of Detail |
| :--- | :--- | :--- |
| **KSLD (Key Single Line Diagram)** | Shows the overall power flow from Utility to Rack. | Conceptual / Regulatory |
| **PSLD (Protection SLD)** | Shows CT/PT ratios, relay types, and trip logic. | Detailed Engineering |
| **Equipment Layout** | Physical placement of Switchgear, UPS, and DGs. | GFC (Good for Construction) |
| **Cable Trench/Tray Layout** | 2D/3D routing of HT and LT feeders. | GFC / Coordination |
| **Earthing & Lightning Layout** | Mesh design and down-conductor placement. | Regulatory (CEIG) |
| **Termination Drawings** | Details of lugs, glands, and pin-outs. | Shop Drawing |

## 3. Standards & Symbology
*   **Symbols:** Standardized on **IEC 60617** (Graphical Symbols for Diagrams). In Indian projects (L&T), IEC is the default; however, for US-based clients (Microsoft/Google), **ANSI Y32.2** symbols may be requested.
*   **Layer Management:** Standardized on **ISO 13567**. All CAD files must have distinct layers for Power, Control, Lighting, and Earthing to allow for easy X-Ref management.
*   **Units:** All dimensions in **Metric (mm)** as per NBC 2016.

## 4. Engineering Design Criteria: Clearance & Spacing

Drawings must reflect the mandatory clearances per **CEA 2023** and **NEC**.

### 4.1 Switchgear Room Clearances
*   **Front Clearance:** Minimum 1500mm to 2000mm (to allow for ACB/VCB withdrawal).
*   **Rear Clearance:** Minimum 1000mm (for maintenance of Form 4b panels).
*   **Height:** Minimum 1000mm clear space above the panel for busduct entry and heat dissipation.

### 4.2 Cable Tray Separation
*   **HT to LT:** 300mm vertical separation.
*   **Power to Data:** 600mm separation (Mandatory for AI GPU interconnect integrity).

## 5. BIM & 3D Coordination (LOD 400)
For the {{ cookiecutter.it_capacity_mw }} MW {{ cookiecutter.city }} site, all GFC drawings are derived from a **Revit 3D Model**.
1.  **Clash Detection:** Weekly Navisworks runs to identify "Hard Clashes" (e.g., Busduct hitting a Chilled Water Pipe).
2.  **Clearance Zones:** 3D "No-Fly Zones" modeled around breakers and valves to ensure maintenance accessibility.
3.  **Point Cloud Scanning:** After the civil shell is ready, the site is scanned to verify that the "As-Built" concrete matches the "As-Designed" electrical model.

## 6. AI-Ready Drawing Specifics
1.  **Busway Tap-off Schedules:** A dedicated drawing showing the exact X-Y coordinates of every 250A/400A tap-off for the {{ cookiecutter.ai_silicon_vendor }} racks.
2.  **Liquid Cooling Interface:** Combined MEP drawings showing the **CDU Electrical Feed** in proximity to the **Fluid Manifolds**.
3.  **Grounding Grid Detail:** Detailed drawing of the **Signal Reference Grid (SRG)** under the AI racks, including bonding details to the pedestal.

## 7. Drawing Creation Workflow (L&T Standard)
1.  **Drafting:** Engineer creates the mark-up; Draftsman generates the CAD/Revit file.
2.  **Internal Review:** Senior Design Consultant checks for technical accuracy and compliance with the **DBR**.
3.  **Inter-disciplinary Coordination (IDC):** Electrical, Mechanical, and Civil teams sign off on the layout.
4.  **Issue for Approval:** Sent to the Client and Regulatory Body (CEIG).
5.  **Issue for Construction (IFC/GFC):** Stamped and released to the site.

## 8. Maintenance & As-Builts
*   **Red-Line Markups:** Every change made on-site at {{ cookiecutter.city }} must be recorded on a paper copy in **Red Pen**.
*   **Final As-Built:** The BIM model is updated to reflect the site changes, providing the O&M team with a "Digital Twin" of the {{ cookiecutter.it_capacity_mw }} MW plant.

## 9. Common Mistakes in Drawings
*   **Missing Scale:** Drawings issued without a scale or "NTS" (Not to Scale) without dimensions.
*   **Text Size:** Too small to read when printed in A3 for site use.
*   **Revision Clouding:** New changes not clouded, leading to construction errors.
*   **Clearance Violations:** Modeling the equipment but forgetting the **Door Swing** or **Withdrawal Space**.

---

## 10. Design Checklist
- [ ] Are all symbols compliant with IEC 60617?
- [ ] Is the "Title Block" populated with the correct L&T Project Code?
- [ ] Have the CEIG clearance requirements been verified on the layout?
- [ ] Is the 3D model clash-free in the high-density AI zones?
- [ ] Are the cable tray fill-ratios visually represented in sections?

---
## 11. References
### Standards
* **IEC 60617:** Graphical Symbols for Diagrams.
* **ISO 13567:** Technical product documentation - Organization and naming of layers for CAD.
* **CEA 2023:** Safety and Clearance requirements for layouts.
* **IEEE 315:** Graphic Symbols for Electrical and Electronics Diagrams.

### Software Tools
* **Autodesk Revit:** For 3D BIM Modeling.
* **Autodesk Navisworks:** For Clash Coordination.
* **AutoCAD Electrical:** For 2D Schematics and SLDs.

### Revision History
* 1.0: Initial Drawing Standards for {{ cookiecutter.project_name }} {{ cookiecutter.city }} project.

---
**Next File Recommendation:** `Bill_of_Quantities_Preparation.md` (Focusing on the estimation, procurement specifications, and quantification of the {{ cookiecutter.it_capacity_mw }} MW facility).
