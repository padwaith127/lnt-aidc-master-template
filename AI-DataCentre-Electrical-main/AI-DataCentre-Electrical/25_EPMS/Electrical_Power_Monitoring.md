# Title: Electrical Power Monitoring System (EPMS) - Data & Forensics
## Purpose: To define the architecture, metering requirements, and analytical capabilities of the EPMS for high-speed power quality capture and real-time efficiency tracking.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #EPMS #PowerQuality #PUE #EnergyAnalytics #Forensics #Metering #{{ cookiecutter.project_code }}
## Related Files: [[Supervisory_Control.md]], [[Transient_and_Sag_Analysis.md]], [[Mitigation_Strategies.md]], [[Building_Management_Integration.md]]
## Standards Covered: IEC 61000-4-30 Class A, IEC 62053-22 (Class 0.2S), IEEE 1159, ISO 50001, ASHRAE 90.4

---

## 1. Overview
In a {{ cookiecutter.it_capacity_mw }} MW AI facility, the **Electrical Power Monitoring System (EPMS)** is the "Digital Forensic Lab." While SCADA (Module 24) is built for speed and control, the EPMS is built for **depth and accuracy**. It captures millisecond-level disturbances (Sags, Swells, Transients) and provides the revenue-grade metering data required to calculate Power Usage Effectiveness (PUE) and bill internal or external tenants.

## 2. Design Philosophy: The AI Forensic Engine
AI workloads ({{ cookiecutter.ai_silicon_vendor }}) operate with extreme thermal and electrical dynamics.
1.  **High-Resolution Sampling:** Standard 1-second polling is blind to AI transients. EPMS must support **Waveform Capture** at 1024 samples/cycle.
2.  **Event Chronology:** All meters must be synchronized to a GPS Master Clock via **PTP (Precision Time Protocol)** to ensure that a fault at the {{ cookiecutter.utility_voltage_kv }}kV incoming can be time-aligned with a trip at the Rack PDU.
3.  **Efficiency Granularity:** PUE must be measured at the Facility, Hall, and Row levels.

## 3. Metering Hierarchy & Selection

| Location | Meter Class | Key Capability |
| :--- | :--- | :--- |
| **Utility Incomer ({{ cookiecutter.utility_voltage_kv }}kV)** | Class 0.2S (Revenue) | IEC 61000-4-30 Class A (PQ Compliance). |
| **Main LT PCC Panels** | Class 0.5S | Harmonics to 63rd, Disturbance Direction Detection. |
| **UPS Input/Output** | Class 0.5S | Efficiency monitoring, Phase Imbalance. |
| **PDU / Busway Tap-offs** | Class 1.0 | kWh, kVA, Demand Current (Peak/Average). |
| **Rack PDU (rPDU)** | Class 1.0 | Real-time Power (W) per {{ cookiecutter.ai_silicon_vendor }} Power Shelf. |

## 4. Engineering Calculations: Real-Time PUE

The EPMS is the primary tool for validating the facility's **Power Usage Effectiveness (PUE)**.

### 4.1 PUE Formula
$$PUE = \frac{\text{Total Facility Energy (kWh)}}{\text{IT Equipment Energy (kWh)}}$$

*   **Total Facility Energy:** Measured at the {{ cookiecutter.utility_voltage_kv }}kV Utility Incomer.
*   **IT Equipment Energy:** Measured at the output of the UPS or PDU feeds to the racks.

### 4.2 AI-Ready Calculation Adjustment
AI clusters draw significant power during "Idle" vs. "Compute." The EPMS must track **pPUE (Partial PUE)** specifically for AI zones to identify if the liquid cooling pumps are operating efficiently relative to the GPU load.

## 5. System Architecture
*   **Layer 1 (Field):** Intelligent Electronic Devices (IEDs) with on-board memory for data logging (prevents data loss during network outages).
*   **Layer 2 (Network):** Dedicated High-speed Ethernet (Fiber backbone) using Modbus TCP/IP or BACnet/IP.
*   **Layer 3 (Software):** Database server with a "Sequence of Events" (SOE) recorder and automated reporting engine.

## 6. AI-Ready Technical Requirements
1.  **Disturbance Direction Detection:** The EPMS must automatically determine if a voltage sag originated from the **{{ cookiecutter.utility_provider }} Grid** or from an **Internal AI Load Step**.
2.  **Harmonic Trend Analysis:** AI power supplies generate high 3rd and 5th harmonics. The EPMS must alert operators if the **THDi** exceeds the transformer derating limit.
3.  **Virtual Metering:** Creating "Logic-based" meters that sum up different blocks of the {{ cookiecutter.it_capacity_mw }} MW facility for departmental billing (e.g., "AI Training Block A" vs "Cloud Compute Block B").

## 7. Commissioning & Validation
1.  **Meter Calibration Check:** Compare EPMS readings against a calibrated handheld Power Quality Analyzer (e.g., Fluke 435-II).
2.  **Time-Sync Audit:** Verify all meters are synchronized within **1 millisecond** of the GPS clock.
3.  **Waveform Trigger Test:** Manually trigger a waveform capture to ensure the data reaches the server and is stored in the correct COMTRADE format.

## 8. Maintenance & Operations
*   **Database Health:** Regular pruning of high-resolution waveform data to prevent storage bloat.
*   **Firmware Updates:** Ensuring meters are patched against cybersecurity vulnerabilities (IEC 62443).
*   **Report Automation:** Weekly automated emails to Management showing PUE trends and Peak Demand utilization.

## 9. Failure Modes
*   **Data Gaps:** Occur when meters lack internal memory during a network switch failure. *Mitigation:* Specify meters with "Backfill" capability.
*   **CT Polarity Errors:** Lead to incorrect Power Factor and Energy readings. *Mitigation:* Mandatory secondary injection testing during installation.
*   **Nuisance Alarms:** Too many minor alerts during AI step-loads. *Mitigation:* Implement "Dead-bands" and "Alarm Masking."

---

## 10. Design Checklist
- [ ] Are all meters at the Utility/Main Bus Class A (IEC 61000-4-30)?
- [ ] Is there a GPS Master Clock for time synchronization?
- [ ] Are all CTs/PTs selected for the correct accuracy class (0.2S or 0.5S)?
- [ ] Does the software support ITIC (CBEMA) curve plotting for voltage sags?
- [ ] Is the EPMS network air-gapped from the public internet?

---
## 11. References
### Standards
* **IEC 61000-4-30:** Testing and measurement techniques - Power quality measurement methods.
* **IEC 62053-22:** Electricity metering equipment - Static meters for active energy (classes 0,1 S, 0,2 S and 0,5 S).
* **ISO 50001:** Energy Management Systems.

### Research Papers / White Papers
* **Schneider Electric:** "Forensic Analysis in Data Center Power Systems."
* **Eaton:** "The Importance of Sequence of Events Recording in Mission Critical Facilities."

### Revision History
* 1.0: Initial EPMS Strategy for {{ cookiecutter.project_name }} {{ cookiecutter.city }} project.

---
**Next File Recommendation:** `Level_1_to_Level_5_Testing.md` (Defining the rigorous testing phases required to prove the {{ cookiecutter.it_capacity_mw }} MW plant is ready for AI hardware).
