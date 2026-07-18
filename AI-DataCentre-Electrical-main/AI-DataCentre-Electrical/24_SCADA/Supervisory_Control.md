# Title: SCADA & Automation Logic for {{ cookiecutter.it_capacity_mw }} MW AI-Ready DC
## Purpose: To define the architecture, control logic, and integration requirements for the Supervisory Control and Data Acquisition (SCADA) system governing the electrical infrastructure.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #SCADA #Automation #PLC #IEC61850 #ControlLogic #Hyperscale #{{ cookiecutter.project_code }}
## Related Files: [[HT_Switchgear.md]], [[LV_Switchgear.md]], [[Electrical_Power_Monitoring.md]], [[Backup_Generation.md]]
## Standards Covered: IEC 61850, IEEE C37.1, ISA-101 (HMI), ISA-99 / IEC 62443 (Cybersecurity), NIST SP 800-82

---

## 1. Overview
In the {{ cookiecutter.project_name }} {{ cookiecutter.city }} {{ cookiecutter.it_capacity_mw }} MW facility, the SCADA system is the "Autonomous Pilot." While the EPMS (Module 25) focuses on data and power quality, the SCADA system is responsible for **execution and logic**. For AI-ready infrastructure, the SCADA must manage the extreme power swings of {{ cookiecutter.ai_silicon_vendor }} GPU clusters by coordinating the response of the {{ cookiecutter.utility_voltage_kv }}kV grid, the Diesel Generators, and the Mechanical Cooling interlocks.

## 2. Theoretical Architecture: Redundancy & Latency
To meet Tier III requirements, the SCADA architecture follows a **Zero-Single-Point-of-Failure (ZSPOF)** model:
1.  **Level 0 (Device Layer):** Protection Relays (IEDs) and Smart Breakers.
2.  **Level 1 (Control Layer):** Redundant PLCs (Programmable Logic Controllers) in a **Hot-Standby** configuration.
3.  **Level 2 (Supervisory Layer):** Redundant SCADA Servers, Historians, and HMI Workstations.
4.  **Network:** Industrial Ethernet Ring using **IEC 61850 GOOSE** messaging for sub-10ms peer-to-peer communication.

## 3. Engineering Logic: The AI "Step-Load" Sequencer
AI workloads (Training runs) can cause a {{ cookiecutter.it_capacity_mw }} MW facility to jump from 10% to 90% load almost instantaneously. The SCADA must prevent "Voltage Collapse."

### 3.1 Load Sequencer Logic
*   **Problem:** If all {{ cookiecutter.it_capacity_mw }} MW of IT load tries to pick up simultaneously during a Utility-to-Generator transfer, the DGs will stall.
*   **Logic:** The SCADA executes a **Priority-Based Sequential Loading** algorithm.
    *   Step 1: Critical Cooling (CDUs/Pumps).
    *   Step 2: Core Network Fabric.
    *   Step 3: AI Compute Block 1 (High Priority).
    *   Step 4: AI Compute Block 2.
*   **Calculation:** Delay between steps ($\Delta t$) is determined by the DG frequency recovery curve (typically 2–3 seconds per step).

## 4. Key Equipment Specifications

| Component | Specification | Manufacturer Consideration |
| :--- | :--- | :--- |
| **PLC System** | Dual Redundant (Hot Standby) | Schneider M580, Siemens S7-1500R, Rockwell ControlLogix. |
| **Protocol** | IEC 61850 (MMS & GOOSE) | Mandatory for hyperscale relay integration. |
| **Network Switch** | Layer 3 Managed (Industrial) | Cisco IE3400, Hirschmann, Moxa. |
| **HMI Software** | High-Performance HMI (Grayscale) | AVEVA (Wonderware), GE iFIX, Ignition. |
| **Time Sync** | GPS Master Clock (PTP/NTP) | Tekron, Meinberg. |

## 5. Automated Transfer Scheme (ATS) - The "Main-Tie-Main"
The {{ cookiecutter.city }} facility uses a "Main-Tie-Main" (MTM) configuration on the LV bus.
*   **Sensing:** SCADA monitors voltage on both Incomer 1 and Incomer 2.
*   **Fault Logic:** If Incomer 1 fails, the SCADA verifies no fault exists on the bus (86 lockout check) and closes the Bus Coupler.
*   **Interlock:** Mechanical and Electrical interlocks are hard-wired, but the SCADA provides the "Auto-Close" logic.

## 6. AI-Ready Design Specifics
1.  **Cooling-Power Interlock:** If the SCADA detects a loss of power to a specific CDU (Coolant Distribution Unit), it must immediately send a signal to the {{ cookiecutter.ai_silicon_vendor }} Cluster Management software to "Throttle" the GPUs before they overheat.
2.  **Peak Shaving (Optional):** Integration with BESS (Battery Energy Storage) to discharge during peak GPU bursts to reduce "Demand Charges" from {{ cookiecutter.utility_provider }}.
3.  **Cybersecurity (Zone & Conduit):** The SCADA network must be air-gapped from the corporate network using a **DMZ with Industrial Firewalls** (IEC 62443 compliance).

## 7. Commissioning & Logic Validation
1.  **Level 4 (Functional):** Individual breaker "Open/Close" from HMI and verification of status feedback.
2.  **Level 5 (Integrated):** Full "Black Start" test. We simulate a utility failure and witness the SCADA:
    *   Sending DG start signals.
    *   Closing DG incomers.
    *   Sequencing the {{ cookiecutter.it_capacity_mw }} MW load in 5 MW blocks.
3.  **GOOSE Test:** Using a protocol analyzer to verify that a "Trip" signal from a {{ cookiecutter.utility_voltage_kv }}kV relay reaches the downstream breaker in **<10ms**.

## 8. Failure Modes
*   **Stale Data:** HMI shows a breaker as "Closed" but it's physically "Open." *Mitigation:* Double-point status monitoring (NO+NC auxiliary contacts).
*   **Control Loop Oscillation:** Transformer On-Load Tap Changers (OLTC) "hunting" due to AI load swings. *Mitigation:* Implementing a "Dead-band" and "Time-Delay" in the tap control logic.
*   **PLC CPU Switchover Failure:** PLC-A fails but PLC-B doesn't take over. *Mitigation:* Monthly "Simulated Processor Failure" drills.

---

## 9. Design Checklist
- [ ] Is the PLC system redundant with "Hot Standby" capability?
- [ ] Are the Ethernet switches "Industrial Grade" (High Temp/EMC rated)?
- [ ] Does the ATS logic include a "Fault-Trip" inhibit to prevent closing onto a dead short?
- [ ] Is the HMI designed per ISA-101 (situational awareness)?
- [ ] Is the network architecture compliant with IEC 62443-3-3?

---
## 10. References
### Standards
* **IEC 61850:** Communication networks and systems for power utility automation.
* **ISA-101:** Human-Machine Interfaces for Process Automation Systems.
* **IEC 62443:** Industrial Communication Networks - Network and System Security.

### Research Papers
* **Schneider Electric:** "Designing Redundant SCADA Architectures for Mission Critical Facilities."
* **Siemens:** "GOOSE Messaging for High-Speed Busbar Protection."

### Revision History
* 1.0: Initial SCADA/Automation Logic for {{ cookiecutter.project_name }} {{ cookiecutter.city }}.

---
**Next File Recommendation:** `Electrical_Power_Monitoring.md` (Focusing on the high-speed data capture, PUE analytics, and power quality forensic engine).
