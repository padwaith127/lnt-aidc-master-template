# Title: Substation Design Criteria & Layout Standards
## Purpose: To define the civil, electrical, and safety criteria for the on-site {{ cookiecutter.utility_voltage_kv }}kV Substation.
## Revision: 1.0
## Date: 24-May-2024
## Tags: #Substation #GIS #AIS #{{ cookiecutter.city }} #{{ cookiecutter.project_code }}
## Related Files: [[Utility_Interface.md]], [[HT_Switchgear.md]], [[Standard_Layouts.md]]
## Standards Covered: CBIP Manual 311, CEA 2023, IS 3043

---

## 1. Overview
The on-site substation bridges the utility grid and the data centre power train. For the {{ cookiecutter.city }} {{ cookiecutter.it_capacity_mw }} MW project, space optimization and safety under {{ cookiecutter.city }} industrial conditions dictate the substation topology.

## 2. Selection: GIS vs. AIS
*   **GIS (Gas Insulated Switchgear):** Selected for the {{ cookiecutter.utility_voltage_kv }}kV indoor setup. SF6 gas insulation reduces footprint by 70% compared to AIS, protecting equipment from {{ cookiecutter.city }}'s coastal/industrial salinity.
*   **AIS (Air Insulated Switchgear):** Utilized only in the outdoor gantry/yard where space permits, prior to the underground cable entry into the GIS room.

## 3. Substation Design Criteria
*   **Control Room:** Air-conditioned, dust-free environment maintained at positive pressure to prevent dust/salt ingress.
*   **Battery Backups:** Dedicated 110V DC / 48V DC switchgear trip battery banks with dual redundant chargers.
*   **Cable Trenches:** Water-proofed concrete trenches with sloped drainage to prevent monsoon flooding (critical for {{ cookiecutter.city }} topography).

---
## 📚 References
* **CBIP Manual Publication 311:** Manual on Substation Design.
* **CEA 2023:** Safety Regulations for Substation Clearances.
