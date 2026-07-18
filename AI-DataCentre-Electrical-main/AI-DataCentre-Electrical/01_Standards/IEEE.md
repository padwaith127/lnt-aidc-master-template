# Title: IEEE Standards for Data Centre Power Systems
## Purpose: To provide a quick-reference guide to the IEEE "Color Book" series and the modern 3000 series standards applicable to hyperscale design.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #IEEE #PowerEngineering #Standards #ArcFlash #Earthing #Harmonics #{{ cookiecutter.project_code }}
## Related Files: [[BIS.md]], [[CEA.md]], [[Fault_Level_Calculations.md]], [[Grounding_Grid_Design.md]]
## Standards Covered: IEEE 3000 Series, IEEE 1584, IEEE 519, IEEE 1100, IEEE 80, IEEE 493

---

## 1. Overview
The **IEEE (Institute of Electrical and Electronics Engineers)** standards are the global mathematical and technical foundation for electrical engineering. For the {{ cookiecutter.project_name }} {{ cookiecutter.city }} project, IEEE standards provide the methodology for all core power studies (Short Circuit, Load Flow, Earthing, and Arc Flash).

## 2. Core IEEE Standards for AI Data Centres

### 2.1 The IEEE 3000 Series (Modernized Color Books)
IEEE has transitioned from the "Color Books" (e.g., Red, Brown, Green) to the 3000 series of "Recommended Practices."

| Old Color | New Standard | Focus Area | Application at {{ cookiecutter.city }} |
| :--- | :--- | :--- | :--- |
| **Red Book** | **IEEE 3001.2** | Power Distribution | Sizing transformers and switchgear. |
| **Brown Book**| **IEEE 3002.2** | Load Flow Analysis | Voltage stability during AI training. |
| **Violet Book**| **IEEE 3002.3** | Short Circuit Analysis | Fault level calculations ({{ cookiecutter.fault_level_ka }}kA). |
| **Buff Book** | **IEEE 3004.1** | Protection Coordination | Relay settings and selectivity. |
| **Green Book**| **IEEE 3003.1** | System Grounding | Earthing of neutrals and equipment. |

### 2.2 IEEE 1584: Guide for Performing Arc-Flash Hazard Calculations
*   **Significance:** The global standard for calculating incident energy and flash boundaries.
*   **AI Context:** Mandatory for the {{ cookiecutter.it_capacity_mw }} MW site to determine PPE requirements for technicians working on high-ampacity LV switchgear.
*   **Edition:** 2018 (Latest).

### 2.3 IEEE 519: Harmonic Control in Electric Power Systems
*   **Significance:** Defines limits for THDv and THDi at the Point of Common Coupling (PCC).
*   **AI Context:** Critical for managing the "Pollution" injected into the {{ cookiecutter.city }} grid by thousands of GPU rectifiers.
*   **Edition:** 2022 (Latest).

### 2.4 IEEE 1100: The Emerald Book (Powering & Grounding)
*   **Significance:** The definitive guide for grounding sensitive electronic equipment.
*   **AI Context:** Essential for the **Signal Reference Grid (SRG)** design to prevent GPU packet loss and data corruption.

### 2.5 IEEE 80: Guide for Safety in AC Substation Grounding
*   **Significance:** Methodology for designing the HT Yard grounding mesh.
*   **Calculations:** Step and Touch potential safety limits.

## 3. Engineering Application: Using IEEE in Design
As an Engineer, you do not "choose" settings; you "IEEE-calculate" them.
*   **In ETAP/SKM:** Ensure the software "Calculation Method" is set to the specific IEEE standard mentioned above (e.g., use **IEEE 1584-2018** for Arc Flash, not the 2002 version).

## 4. Comparison: IEEE vs. IEC
| Feature | IEEE (North American/Global) | IEC (European/International) |
| :--- | :--- | :--- |
| **Philosophy** | Theoretical/Calculated | Empirical/Table-based |
| **Usage** | Power Studies & Analysis | Equipment Testing & Safety |
| **Application** | Used for ETAP calculations. | Used for Switchgear specs (IEC 61439). |

## 5. Design Checklist (IEEE Compliance)
- [ ] Has the Arc Flash study been performed per IEEE 1584-2018?
- [ ] Does the harmonic distortion meet IEEE 519-2022 limits at the PCC?
- [ ] Is the grounding grid designed to keep Step/Touch within IEEE 80 limits?
- [ ] Are the IT racks grounded per IEEE 1100 recommendations?

## 6. Failure Modes (Ignoring IEEE)
*   **PPE Mismatch:** Using IEEE 1584-2002 (Old) for Arc Flash, which underestimates incident energy, leading to improper PPE and potential injury.
*   **Harmonic Incompatibility:** Designing for 50Hz/60Hz only and ignoring the IEEE 519 requirements for high-frequency AI loads.

---

## 7. References
### Standards
* **IEEE 3000 Series:** Recommended Practices for Industrial Power Systems.
* **IEEE 1584-2018:** Arc Flash Hazard Calculations.
* **IEEE 519-2022:** Harmonic Control in Power Systems.

### Research Papers
* **IEEE Industry Applications Magazine:** Search for "Data Center Reliability Analysis."

### Revision History
* 1.0: Mapped core IEEE standards for {{ cookiecutter.project_name }} {{ cookiecutter.city }} project.
