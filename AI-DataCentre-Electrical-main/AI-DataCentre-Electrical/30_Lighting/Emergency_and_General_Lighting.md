# Title: General & Emergency Lighting Systems for AI Data Centres
## Purpose: To define the engineering requirements for illumination, emergency egress lighting, and smart lighting controls in a 24/7 hyperscale facility.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #LightingDesign #LED #EmergencyLighting #LuxLevels #LTVyoma #NBC2016
## Related Files: [[BMS_Integration.md]], [[Operation.md]], [[Maintenance.md]]
## Standards Covered: NBC 2016 (Part 8, Sec 1), IS 3646, IS 10322, NFPA 101, EN 12464-1, ASHRAE 90.1

---

## 1. Overview
In a 40 MW AI facility, lighting is often overlooked, yet it is vital for operational safety and maintenance precision. In the Mahape data centre, which houses high-density NVIDIA GPU clusters and complex liquid cooling manifolds, lighting must provide high visibility for technical tasks while minimizing energy consumption to support the facility's PUE (Power Usage Effectiveness) goals.

## 2. Design Philosophy: Performance over Aesthetics
1.  **Uniformity:** High uniformity (Emin/Eavg > 0.6) is required in Data Halls to prevent shadows during server hot-swapping.
2.  **Reliability:** 100% LED-based systems for long life and low maintenance.
3.  **Autonomous Emergency:** Independent battery-backed emergency lighting for critical aisles and egress paths.
4.  **AI Zone Specifics:** Higher vertical lux levels are required for liquid cooling CDU maintenance and high-density rack cable management.

## 3. Engineering Design Criteria (Lux Levels)

Based on **IS 3646** and **NBC 2016**, the following levels are mandatory for the L&T Mahape site:

| Area | Average Lux (lx) | Height of Measurement | Purpose |
| :--- | :--- | :--- | :--- |
| **Data Hall (White Space)** | 500 lx | 1.0m (Rack Front) | Precision cable/fiber work. |
| **HT / LT Rooms** | 300 lx | Floor Level | Safe switching operations. |
| **UPS / Battery Rooms** | 300 lx | Floor Level | Terminal inspection. |
| **Mechanical / Pump Rooms** | 200 lx | Floor Level | Valve and CDU maintenance. |
| **Office / SOC** | 500 lx | Desk Level | Operational monitoring. |
| **Emergency Egress** | 10 lx (min) | Floor Level | Safe evacuation (IS 3217). |

## 4. Engineering Calculations: The Lumen Method

### 4.1 Average Illuminance Calculation
$$E = \frac{\Phi \times n \times CU \times LLF}{A}$$
*   $E$: Average Illuminance (Lux).
*   $\Phi$: Initial Luminous Flux of one lamp (Lumens).
*   $n$: Number of lamps.
*   $CU$: Coefficient of Utilization (depends on room reflectances and geometry).
*   $LLF$: Light Loss Factor (typically 0.8 for clean DC environments).
*   $A$: Area of the room ($m^2$).

### 4.2 Spacing to Height Ratio (SHR)
To ensure uniformity, the spacing between fixtures ($S$) must not exceed the manufacturer's recommended SHR relative to the mounting height ($H$).
*   **Rule of Thumb:** $S \approx 1.2 \times H$ for standard LED battens.

## 5. Emergency & Exit Lighting (NFPA 101)
*   **Autonomy:** Minimum 90 minutes of operation during total power failure.
*   **Central Battery System (CBS) vs. Self-Contained:** For a 40 MW facility, a **Central Battery System** is preferred for ease of testing and maintenance.
*   **Exit Signage:** Green "EXIT" signs with internal LEDs and directional arrows, placed at every change of direction in the egress path.
*   **Placement:** Emergency lights must be positioned to illuminate the faces of HT/LT switchgear and the main valves of the liquid cooling system.

## 6. AI-Ready Design Requirements
1.  **Vertical Illuminance:** In high-density racks (52U), vertical lux at the top and bottom of the rack is more important than horizontal lux on the floor. Use wide-beam optics.
2.  **CRI (Color Rendering Index):** Specify **CRI > 80**. This is critical for identifying color-coded fiber optic patches and multi-colored internal wiring in NVIDIA power shelves.
3.  **Flicker-Free Drivers:** Essential for high-speed security cameras and technicians using high-speed diagnostic tools.

## 7. Controls & Energy Efficiency (ASHRAE 90.1)
*   **Motion Sensors:** PIR (Passive Infrared) or Dual-Tech sensors in every aisle. Lighting should dim to 10% when unoccupied.
*   **BMS Integration:** Lighting controllers should communicate via **DALI (Digital Addressable Lighting Interface)** to the BMS for scheduling and fault reporting.
*   **Daylight Harvesting:** Implementation in SOC (Security Operations Centre) and Office areas to reduce energy consumption.

## 8. Construction & Installation (L&T Standards)
*   **Mounting:** Fixtures in Data Halls are typically mounted to the **Under-side of the Cable Tray** or specialized lighting trunking to keep the ceiling void clear for airflow.
*   **Circuiting:** Lighting circuits must be separate from IT power. Emergency lighting should be on a dedicated "Non-UPS Essential" circuit backed by the DG set.
*   **Wiring:** Use FR-LSH copper wires in GI conduits or trunking.

## 9. Commissioning & Testing
1.  **Lux Mapping:** Use a calibrated Lux Meter to measure levels at 1m intervals across the Data Hall.
2.  **Emergency Duration Test:** Discharge the emergency system for 90 minutes to verify battery health.
3.  **Sensor Tuning:** Adjust time-delay and sensitivity of motion sensors to prevent "dark aisles" while technicians are working quietly.
4.  **DALI Addressing:** Verify every fixture is individually addressable and controllable from the BMS HMI.

## 10. Failure Modes
*   **Driver Failure:** The most common failure point in LEDs. *Mitigation:* Use high-quality drivers with 50,000-hour L70 ratings.
*   **Shadowing:** Caused by placing lighting directly above cable trays or HVAC ducts. *Mitigation:* Coordinate layout in 3D BIM.
*   **Battery Sulfation:** In self-contained units if not exercised. *Mitigation:* Automated monthly testing via DALI.

---

## 11. Design Checklist
- [ ] Are lux levels $\geq$ 500 lx at the rack face?
- [ ] Is the CRI $\geq$ 80 for fiber identification?
- [ ] Do emergency lights have 90-minute autonomy?
- [ ] Is DALI control integrated with the BMS?
- [ ] Are motion sensors positioned to cover the full length of the aisles?

---
## 12. References
### Standards
* **NBC 2016:** National Building Code of India (Part 8, Sec 1).
* **IS 3646:** Code of Practice for Interior Illumination.
* **NFPA 101:** Life Safety Code.
* **IS 10322:** Specification for Luminaires.

### Manufacturer Documents
* **Philips / Signify:** "Data Center Lighting Application Guide."
* **Wipro Lighting:** "Industrial and Commercial LED Solutions Catalogue."
* **Zumtobel:** "Lighting for Data Centers - Design and Technology."

### Revision History
* 1.0: Initial Lighting Strategy for L&T Vyoma Mahape project.

---
**Next File Recommendation:** `31_Commissioning/Level_1_to_Level_5_Testing.md` (Crucial for proving the 40 MW plant is ready for NVIDIA deployment).