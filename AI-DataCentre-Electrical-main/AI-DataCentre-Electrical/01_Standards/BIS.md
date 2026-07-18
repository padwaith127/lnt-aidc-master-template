# Title: Indian Standards (BIS) for Data Centre Design
## Purpose: To provide a localized regulatory framework for electrical installations in India.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #BIS #ISStandards #Compliance #India #Earthing
## Related Files: [[CEA.md]], [[Grounding_Grid_Design.md]]
## Standards Covered: IS 732, IS 3043, IS 60947, IS 2026

---

## 1. Overview
While global standards (IEEE/IEC) provide the technical "how-to," the Bureau of Indian Standards (BIS) and the National Building Code (NBC) provide the legal "must-do" for the {{ cookiecutter.project_name }} {{ cookiecutter.city }} project. Non-compliance results in failure to receive the "Electrical Inspectorate (CEIG) Approval."

## 2. Core IS Standards for Data Centres

### 2.1 Earthing (IS 3043: 2018)
*   **Significance:** Data centres require a "Clean Earth" for sensitive electronics and a "Power Earth" for safety.
*   **Key Requirement:** Use of maintenance-free chemical earthing or traditional pipe/plate earthing. For {{ cookiecutter.it_capacity_mw }}MW, a grid-based approach is mandatory.
*   **Mentoring Tip:** Always design for a ground resistance of < 1 Ohm for the overall grid.

### 2.2 Low Voltage Installations (IS 732: 2019)
*   **Significance:** Governs the selection of cables, conduits, and protection devices.
*   **AI Context:** Focus on Clause 5 regarding "Harmonic Currents" which are prevalent in AI power shelves.

### 2.3 Transformers (IS 2026)
*   **Significance:** Defines the testing and performance of Power and Distribution Transformers.
*   **Requirement:** Since {{ cookiecutter.city }} may have specific environmental challenges, specify "Corrosion Protection" and "Hermetically Sealed" or "Cast Resin" (Dry Type) for indoor units.

## 3. Comparison: IS vs. IEC
| Feature | IS (Indian Standard) | IEC (International) | Application in {{ cookiecutter.city }} |
| :--- | :--- | :--- | :--- |
| **Voltage** | 230/415V (+/- 6% or 10%) | 230/400V | Use IS for Utility Interface |
| **Color Coding** | Red, Yellow, Blue | Brown, Black, Grey | Follow IS for local safety |
| **Earthing** | TNS / TT preferred | Multiple options | TNS is mandatory for DC |

## 4. Statutory Approvals Workflow
1.  **Drawing Submission:** Submit SLDs and Earthing Layouts to the Electrical Inspector.
2.  **Site Inspection:** Inspector verifies clearance distances per **NBC 2016**.
3.  **Charging Permission:** Granted only after IS compliance is certified.

---
## 📚 References
### Standards
* **IS 3043 (2018):** Code of Practice for Earthing.
* **IS 732 (2019):** Code of Practice for Electrical Wiring Installations.
* **NBC 2016:** National Building Code of India.

### Revision History
* 1.0: Mapped core IS standards for Indian Hyperscale projects.
