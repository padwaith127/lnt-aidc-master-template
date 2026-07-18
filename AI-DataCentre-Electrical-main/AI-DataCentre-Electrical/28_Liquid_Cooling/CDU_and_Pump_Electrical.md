# Title: Liquid Cooling (CDU) & Secondary Loop Electrical Requirements
## Purpose: To define the specialized electrical distribution and control requirements for Coolant Distribution Units (CDUs) and secondary cooling loops essential for {{ cookiecutter.ai_silicon_vendor }} AI infrastructure.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #LiquidCooling #CDU #{{ cookiecutter.ai_silicon_vendor }} #SecondaryLoop #PumpControl #{{ cookiecutter.project_code }}
## Related Files: [[HVAC_Power_Integration.md]], [[Building_Management_Integration.md]], [[Rack_Level_Distribution.md]], [[GPU_Infrastructure_Requirements.md]]
## Standards Covered: ASHRAE TC 9.9 (2023), IEC 60364-7-706, NFPA 70, UL 62368-1

---

## 1. Overview
In a {{ cookiecutter.it_capacity_mw }} MW AI facility supporting {{ cookiecutter.ai_silicon_vendor }} clusters, air cooling is insufficient. The facility utilizes **Direct-to-Chip (D2C)** liquid cooling. The **Coolant Distribution Unit (CDU)** is the heartbeat of this system, acting as the heat exchanger between the Facility Water System (FWS) and the Technology Cooling System (TCS). Electrically, CDUs are "Critical Loads" that require the same level of availability as the IT racks themselves.

## 2. Theory: The CDU Electrical Profile
A CDU contains circulating pumps, a control system, and motorized valves. 
*   **In-Row CDUs:** Typically 10kW to 30kW electrical load.
*   **Floor-Mount (Centralized) CDUs:** 50kW to 150kW electrical load.
*   **Load Type:** Primarily inductive (VFD-driven pumps) and sensitive electronics (controllers).

## 3. Engineering Philosophy: The "Zero Thermal Buffer" Rule
Unlike chilled water loops that have thermal inertia (storage tanks), the secondary liquid loop in an AI rack has almost **zero thermal buffer**. 
*   **Mandatory:** CDUs must be powered by the **UPS**. 
*   **Consequence:** If a CDU loses power for even 5-10 seconds while GPUs are at full TDP, the GPUs will overheat and shut down, potentially causing hardware stress.

## 4. Engineering Calculations: CDU Power Sizing

### 4.1 Pump Power Requirement
The electrical draw of a CDU is dominated by the pump motor required to move coolant through the micro-channels of the GPU cold plates.
*   **Formula:** $P_{elec} = \frac{Q \times H \times \rho \times g}{\eta_{pump} \times \eta_{motor}}$
    *   $Q$: Flow rate ($m^3/s$)
    *   $H$: Head/Pressure drop (m)
    *   $\eta$: Efficiency
*   **Typical AI Metric:** For a 1.2 MW GPU cluster, the secondary pumps may draw ~60-80 kW of electrical power to maintain the required flow rates (~1.5 to 2.0 GPM per GPU).

### 4.2 Redundancy & Branch Circuit Sizing
*   **Sizing:** Per NEC/CEA, size branch circuits at **125%** of the CDU's Maximum Continuous Rating (MCR).
*   **Example:** A 40A rated CDU requires a 50A circuit breaker and corresponding 10 sq.mm copper cable.

## 5. AI-Ready Design Requirements ({{ cookiecutter.ai_silicon_vendor }} Infrastructure)

| Feature | Requirement | Implementation |
| :--- | :--- | :--- |
| **Dual Power Feed** | Source A & Source B | Integrated ATS or Dual Inlets in the CDU cabinet. |
| **Control Power** | Redundant DC Supplies | Ensure the PLC/Controller stays live during source transfer. |
| **VFD Integration** | Modbus/BACnet Control | Dynamic flow adjustment based on GPU "Power Telemetry." |
| **Leak Detection** | Integrated Trip | Emergency Power Off (EPO) interface for the CDU if a leak is sensed. |

## 6. Construction & Layout (L&T Execution)
*   **Placement:** In-row CDUs are placed within the IT row. Electrical feeds must come from the **Overhead Busway** or **Floor PDUs** dedicated to critical cooling.
*   **Water-Electrical Separation:** Strictly maintain the "Drip-Zone" rule. Electrical conduits must never be located directly under mechanical pipe joints. 
*   **Shielding:** Use shielded VFD cables to prevent the pump's switching frequency from interfering with the GPU's high-speed interconnect signals.

## 7. Commissioning & Testing
1.  **ATS Transfer Test:** Verify the CDU pumps continue to run during a "Source A to Source B" UPS transfer.
2.  **Dry-Run Test:** Verify PLC logic and VFD ramp-up without fluid (if permitted by OEM).
3.  **Telemetry Check:** Ensure the CDU "Flow Rate" and "Inlet Temp" are visible in the BMS and the Cluster Management software.
4.  **Pressure-Trip Test:** Verify the electrical shutdown of the pump if the secondary loop pressure exceeds the burst rating of the GPU manifolds.

## 8. Failure Modes
*   **VFD Harmonic Resonance:** High-frequency noise from the CDU pump VFDs causing "ghost" alarms in the rack controllers. *Mitigation:* Install line reactors at the CDU input.
*   **Condensation on Cables:** If the facility water is too cold, condensation can form on cold pipes and drip onto electrical trays. *Mitigation:* Proper insulation and "Drip-Tray" monitoring.
*   **Communication Loss:** If the CDU loses the BMS signal, it must default to "100% Flow" to prevent GPU meltdown.

---

## 9. Design Checklist
- [ ] Are all CDUs connected to the UPS?
- [ ] Is there an ATS (internal or external) for dual-feed redundancy?
- [ ] Are the VFD cables shielded and separated from signal cables?
- [ ] Is the leak detection system integrated into the CDU electrical trip circuit?
- [ ] Has the UPS been sized to include the 15-20% additional load from the liquid cooling pumps?

---
## 📚 References
### Standards
* **ASHRAE TC 9.9 (2023):** Water-Cooled Servers and Related Heat Transfer Equipment.
* **IEC 62368-1:** Audio/video, information and communication technology equipment - Safety requirements.
* **UL 60950-1:** Information Technology Equipment - Safety.

### Manufacturer Documents
* **Vertiv / Liebert:** "XDU Coolant Distribution Unit Technical Manual."
* **Schneider Electric:** "In-Row Liquid Cooling Electrical Integration Guide."
* **Vendor Specs:** "{{ cookiecutter.ai_silicon_vendor }} Infrastructure Design Guide."

### Revision History
* 1.0: Initial Liquid Cooling Electrical Strategy for {{ cookiecutter.project_name }} {{ cookiecutter.city }}.

---
**Next File Recommendation:** `Detection_and_Suppression.md` (Focusing on the electrical and control aspects of VESDA and Gas Suppression systems).
