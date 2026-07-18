# Title: CEIG {{ cookiecutter.state }} - Statutory Approval & Inspection Workflow
## Purpose: Mandatory checklist for Electrical Inspectorate approval in {{ cookiecutter.city }}.
## Revision: 1.0
## Date: 24-May-2024
## Tags: #CEIG #{{ cookiecutter.state }} #Statutory #{{ cookiecutter.project_code }} #{{ cookiecutter.city }}
## Standards: CEA 2023, {{ cookiecutter.state }} Electrical Acts

---

## 1. Pre-Construction Stage
1.  **Drawing Submission:** Submit HT SLD, Earthing Layout, and Substation Layout to the **Chief Electrical Inspector (CEIG), {{ cookiecutter.state }} PWD.**
2.  **Scrutiny Fees:** Payment based on total kVA ({{ (cookiecutter.it_capacity_mw | float * cookiecutter.target_pue | float / 0.95) | round(2) }} MVA for this project).

## 2. Construction Stage
1.  **Equipment Reports:** All {{ cookiecutter.utility_voltage_kv }}kV Switchgear and Transformers must have **Type Test Reports** (CPRI/NABL).
2.  **Contractor License:** Ensure electrical sub-contractors hold a valid "A-Class" {{ cookiecutter.state }} Electrical License.

## 3. Final Inspection Checklist
1.  **Earthing:** Every pit must be numbered; Earth-Link to Body/Neutral must be visible.
2.  **Relay Testing:** Witnessing of Secondary Injection tests by the Inspector.
3.  **Clearances:** Verifying Phase-to-Phase and Phase-to-Earth clearances in the {{ cookiecutter.utility_voltage_kv }}kV Yard.
4.  **Permit to Charge:** Receipt of the formal letter "Permission to Energize" before the utility breaker is closed.

---
## 📚 References
* **CEA 2023:** Safety Regulations.
* **PWD {{ cookiecutter.state }}:** Electrical Inspectorate Guidelines.
