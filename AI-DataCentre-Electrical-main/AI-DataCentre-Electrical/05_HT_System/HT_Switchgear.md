# Title: HT Switchgear Design, Protection & Architecture
## Purpose: To define the engineering specifications of the {{cookiecutter.utility_voltage_kv}} kV Medium/High Voltage distribution system for the {{cookiecutter.project_name}}.
## Tags: #HTSwitchgear #VCB #RelayProtection #{{cookiecutter.utility_voltage_kv}}kV #Hyperscale
## Standards Covered: IEC 62271-200, IEC 62271-100, IEEE 242, Local Safety Codes

---

## 1. Overview
The HT (High Tension) Switchgear is the "Primary Distribution Hub." For a {{cookiecutter.it_capacity_mw}} MW load in {{cookiecutter.city}}, this system must facilitate **Concurrent Maintainability**, allowing any breaker or bus section to be serviced without dropping the AI training workload.

## 2. Engineering Philosophy: AI-Ready HT Architecture
In AI hyperscale design, we utilize a **Block Redundant** or **Distributed Redundant** architecture.
*   **Segmented Busbars:** The main HT bus is segmented using Bus Couplers to limit the "Blast Radius" of a fault.
*   **AI Transient Handling:** AI workloads cause sudden load shedding or pickup. The HT protection must be "Stable" enough to ignore transients but "Sensitive" enough to clear internal faults in <100ms.

## 3. Equipment Selection & Specifications

| Feature | Specification | Reasoning |
| :--- | :--- | :--- |
| **Enclosure Type** | Metal-Clad (LSC-2B-PM) | Ensures maximum operator safety and compartmentation. |
| **Interruption Medium** | Vacuum (VCB) or SF6 | Reliable, low maintenance. |
| **Insulation** | Air (AIS) or Gas (GIS) | GIS is preferred for hyperscale to minimize footprint and protect against {{cookiecutter.city}} environmental factors. |
| **Busbar Material** | Electrolytic Copper (99.9%) | Lower losses and better thermal performance than Al. |
| **Protection Relay** | Numerical (IEC 61850) | Enables high-speed GOOSE messaging for logic interlocks. |

## 4. Engineering Calculations: CT Ratio and Burden
Current Transformers (CT) must not saturate during a fault.
*   **Ratio Selection:** 120% to 150% of full load current.
*   **Protection Core:** 5P20 (5% error at 20 times rated current).
*   **Metering Core:** Class 0.2s (Revenue quality for EPMS integration).

## 5. Protection Philosophy (The "Protection SLD")
Every HT feeder in the {{cookiecutter.project_name}} must have:
1.  **Overcurrent & Earth Fault (50/51, 50N/51N):** Standard IDMT (Inverse Definite Minimum Time) curves.
2.  **Differential Protection (87T/87B):** For Transformers >10MVA and Main Busbars.
3.  **Under/Over Voltage (27/59):** To protect UPS/Cooling motors from {{cookiecutter.utility_provider}} grid instability.

## 6. Construction & Layout 
*   **Room Environment:** HT rooms must be pressurized and air-conditioned to prevent the ingress of dust or humidity, which causes "Tracking" on insulators.
*   **Clearance:** Maintain minimum clearances per Local AHJ / Electrical Inspectorate requirements.

## 7. Failure Modes & AI-Specific Risks
*   **Partial Discharge (PD):** Environmental degradation leads to PD in cable terminations. *Mitigation:* Install permanent Online PD Monitoring sensors.
*   **Resonance:** Large AI sites have massive amounts of capacitance (UPS filters). This can cause "Ferroresonance" during switching. *Mitigation:* Use damping resistors on PTs.

## 8. Design Checklist
- [ ] Is the switchgear de-rated for a maximum ambient of {{cookiecutter.max_ambient_temp}}°C?
- [ ] Are all relays communicating via **IEC 61850** to the SCADA?
- [ ] Does the "Arc Flash" study require the use of "Remote Racking" for operators?
