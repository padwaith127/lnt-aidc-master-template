# Title: BMS Integration & Environmental Control
## Purpose: To define the integration between electrical systems and the Building Management System (BMS) for environmental monitoring, cooling control, and safety in an AI-ready facility.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #BMS #HVAC #LiquidCooling #Integration #BACnet #DCIM #{{ cookiecutter.project_code }}
## Related Files: [[Supervisory_Control.md]], [[Electrical_Power_Monitoring.md]], [[CDU_and_Pump_Electrical.md]], [[Detection_and_Suppression.md]]
## Standards Covered: ASHRAE Guideline 13, ISO 16484, BACnet (ANSI/ASHRAE 135), TIA-942-C

---

## 1. Overview
In the {{ cookiecutter.project_name }} {{ cookiecutter.city }} {{ cookiecutter.it_capacity_mw }} MW AI facility, the Building Management System (BMS) is the orchestrator of the facility's "Physical Health." While the SCADA system manages the power train, the BMS manages the cooling, environment, and life-safety systems. For AI infrastructure, the BMS plays a critical role in managing the **Direct-to-Chip (D2C) Liquid Cooling** loops and ensuring that the high-density heat ({{ cookiecutter.rack_density_kw }}kW/rack) does not lead to "Thermal Runaway" in the white space.

## 2. Architecture: High-Level Interface (HLI)
The BMS at {{ cookiecutter.city }} utilizes a distributed architecture with a centralized supervisory layer.
*   **Protocols:** Standardized on **BACnet/IP** for mechanical systems and **Modbus TCP/IP** for electrical system integration.
*   **Integration Layer:** The BMS pulls summary data (kW, Amps, Alarms) from the EPMS/SCADA via a High-Level Interface (HLI) to provide a "Single Pane of Glass" for the facility manager.

## 3. Key Monitoring & Control Domains

| Domain | Integration Points | Purpose |
| :--- | :--- | :--- |
| **Cooling Plant** | Chillers, Pumps, Cooling Towers. | Maintaining secondary loop temperature for CDUs. |
| **Liquid Cooling (CDU)** | Flow Rate, Pressure, Inlet/Outlet Temp. | Critical for GPU cluster thermal health. |
| **Environment** | Temp/Humidity sensors (3 per AI rack). | ASHRAE TC 9.9 compliance. |
| **Leak Detection** | Sensing cables under CDUs and piping. | Immediate shutdown of fluid loops if a leak is detected. |
| **Fire/Smoke** | VESDA, Smoke detectors, Fire Dampers. | Life safety and equipment protection. |

## 4. Engineering Calculations: Cooling-Electrical Interdependency

### 4.1 Heat Load Conversion
The BMS must translate electrical power draw (kW) into cooling demand (Tons of Refrigeration - TR).
*   **Formula:** $Q_{cooling} = \frac{P_{IT(kW)} \times 3412.14}{12,000}$
*   **Worked Example:** For a 1.2 MW AI Cluster:
    $$Q = \frac{1,200 \times 3412.14}{12,000} \approx 341 \text{ TR (Tons of Refrigeration)}$$
*   **AI Context:** The BMS uses "Feed-Forward" logic—when the SCADA sees a spike in GPU power consumption, the BMS pre-emptively ramps up pump speeds before the water temperature rises.

## 5. AI-Ready Design Requirements
1.  **High-Resolution Thermal Mapping:** Standard DCs use 1 sensor per 3 racks. AI zones in {{ cookiecutter.city }} require **3 sensors per rack** (Bottom, Middle, Top) on the air-intake side to detect localized hot spots.
2.  **CDU (Coolant Distribution Unit) Integration:** The BMS must monitor the "Approach Temperature" (the difference between the primary chilled water and the secondary GPU coolant). If this gap narrows, it indicates heat exchanger fouling.
3.  **Variable Frequency Drive (VFD) Coordination:** The BMS manages the VFDs of the massive cooling pumps. It must ensure that the "Ramp Rate" of these motors is coordinated with the DG synchronization logic to prevent voltage dips.

## 6. Environmental Design Criteria (ASHRAE TC 9.9)
The facility targets the following operating envelope for AI zones:
*   **Dry Bulb Temperature:** 18°C to 27°C (Allowable up to 32°C).
*   **Relative Humidity:** 8% to 60% (Dew point dependent).
*   **Liquid Coolant Inlet:** Typically 30°C to 45°C (Class W3/W4).

## 7. Commissioning & Testing
1.  **Graphics Verification:** Ensure the 3D dashboard correctly reflects the physical layout of the {{ cookiecutter.city }} Data Hall.
2.  **Sensor Calibration:** Verify BMS temperature readings against a calibrated handheld psychrometer.
3.  **Interlock Testing:** 
    *   Simulate a "Leak Detected" alarm; verify the CDU pump shuts down and the solenoid valve closes.
    *   Simulate a "Fire" alarm; verify that the HVAC fire dampers close and CRAC units shut down.
4.  **Network Latency Check:** Verify that an alarm reaches the workstation in **< 2 seconds**.

## 8. Failure Modes
*   **Sensor Drift:** An AI rack is overheating, but the BMS shows it as "Cool" due to a faulty sensor. *Mitigation:* Use 2-out-of-3 (2oo3) voting logic for critical rack inlets.
*   **BACnet Broadcast Storms:** Excessive network traffic crashing the BMS controllers. *Mitigation:* Segment the BMS network using VLANs and routers (not just switches).
*   **Manual Override Neglect:** A pump is left in "Hand" (Manual) mode after maintenance, leading to a loss of automated cooling control. *Mitigation:* Alarm in BMS if any critical device is "Not in Auto."

---

## 9. Design Checklist
- [ ] Are there leak detection probes at every CDU and pipe joint?
- [ ] Does the BMS HMI provide a 3D thermal map of the AI racks?
- [ ] Is the BMS integrated with the Fire Alarm Control Panel (FACP)?
- [ ] Are there 3 temperature sensors per AI rack (Inlet side)?
- [ ] Is the "Feed-Forward" cooling logic implemented based on UPS load data?

---
## 10. References
### Standards
* **ASHRAE Guideline 13:** Specifying Building Automation Systems.
* **ISO 16484:** Building automation and control systems (BACS).
* **ANSI/ASHRAE 135:** BACnet - A Data Communication Protocol for Building Automation.

### Manufacturer Documents
* **Schneider Electric:** "EcoStruxure Building Operation Technical Manual."
* **Johnson Controls:** "Metasys for Data Centers Design Guide."
* **Honeywell:** "Experion PKS for Industrial Infrastructure."

### Revision History
* 1.0: Initial BMS Integration strategy for {{ cookiecutter.project_name }} {{ cookiecutter.city }}.

---
**Next File Recommendation:** `HVAC_Power_Integration.md` (Focusing on the electrical distribution and motor control for the mechanical plant).
