# Title: ASHRAE TC 9.9 Thermal Guidelines for Data Centres
## Purpose: To define the thermal and environmental envelopes required to keep {{ cookiecutter.it_capacity_mw }} MW of AI equipment operational and efficient.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #ASHRAE #ThermalManagement #LiquidCooling #PUE #A1-A4 #W1-W5 #{{ cookiecutter.project_code }}
## Related Files: [[Building_Management_Integration.md]], [[CDU_and_Pump_Electrical.md]], [[High_Density_Thermal_Management.md]]
## Standards Covered: ASHRAE TC 9.9 (2023), ASHRAE 90.4

---

## 1. Overview
In a {{ cookiecutter.it_capacity_mw }} MW facility, thermal management is an electrical problem. The **ASHRAE (American Society of Heating, Refrigerating and Air-Conditioning Engineers) TC 9.9** committee defines the "Operating Envelope" of the data centre. For the {{ cookiecutter.project_name }} {{ cookiecutter.city }} project, these guidelines dictate the temperature and humidity settings that our Electrical Control (BMS) and Cooling Plant must maintain.

## 2. Air Cooling: The Environmental Envelopes
ASHRAE classifies data centres by their "Recommended" and "Allowable" ranges:
*   **Class A1:** For mission-critical servers (Standard IT).
*   **Recommended Range:** 18°C to 27°C (64.4°F to 80.6°F).
*   **Allowable Range:** Up to 32°C (A1).

## 3. Liquid Cooling: The W-Classes (Critical for AI)
Since {{ cookiecutter.city }} is AI-ready, we utilize **Direct-to-Chip (D2C)** cooling. ASHRAE classifies the temperature of the facility water entering the CDU:

| Class | Primary Water Temp | Cooling Technology |
| :--- | :--- | :--- |
| **W1/W2** | 2°C to 27°C | Requires Chillers. |
| **W3** | 2°C to 32°C | Partial Free Cooling (Dry Coolers). |
| **W4/W5** | 2°C to 45°C+ | 100% Free Cooling / High Efficiency. |

**{{ cookiecutter.city }} Target:** **Class W3/W4** to minimize Chiller power consumption and improve PUE.

## 4. Engineering Impact of ASHRAE TC 9.9
1.  **Humidity Control:** ASHRAE 2023 updates allow for lower relative humidity (as low as 8%), reducing the electrical load of humidifiers in the site.
2.  **Dew Point Management:** The BMS must ensure that the liquid coolant entering an {{ cookiecutter.ai_silicon_vendor }} rack is always above the **Room Dew Point** to prevent condensation on the 48V DC busbars.
3.  **PUE (ASHRAE 90.4):** This standard defines the "Energy Standard for Data Centers," mandating minimum efficiencies for transformers and UPS systems.

## 5. Design Checklist (ASHRAE Compliance)
- [ ] Is the BMS programmed with ASHRAE 2023 "Recommended" envelopes?
- [ ] Does the CDU secondary loop maintain the W3/W4 temperature class?
- [ ] Are temperature sensors located at the "Rack Inlet" (not the CRAC return)?
- [ ] Is the dew point monitoring integrated into the pump-stop logic?
- [ ] Are the transformers and UPS units compliant with ASHRAE 90.4 efficiency levels?

---

## 6. References
### Standards
* **ASHRAE TC 9.9 (2023):** Thermal Guidelines for Data Processing Environments.
* **ASHRAE 90.4:** Energy Standard for Data Centers.

### Revision History
* 1.0: Mapped ASHRAE thermal requirements for {{ cookiecutter.project_name }} {{ cookiecutter.city }} project.
