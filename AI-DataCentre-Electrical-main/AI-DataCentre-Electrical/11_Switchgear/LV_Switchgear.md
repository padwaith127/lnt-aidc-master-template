# Title: Low Voltage (LV) Switchgear Design & PCC Architecture
## Purpose: To define the technical specifications for Main Low Voltage Panels (PCCs) and the logic for power distribution in the {{cookiecutter.project_name}}.
## Tags: #LVSwitchgear #PCC #ACB #ATS #IEC61439 #Selectivity #Form4b

---

## 1. Overview
In the {{cookiecutter.project_name}} facility, the LV Switchgear acts as the primary clearinghouse for electricity stepped down from the transformers. It houses the Air Circuit Breakers (ACBs) that manage the Main-Tie-Main (MTM) configurations and the Automatic Transfer Schemes (ATS) that switch between Utility and Generator power.

## 2. Engineering Philosophy: Concurrent Maintainability
To meet Uptime Tier III/IV standards, the LV Switchgear must support "Concurrent Maintainability."
*   **Form of Separation:** **Form 4b (Type 7)** is mandatory. This ensures that the busbars, functional units, and cable terminations are in separate compartments, allowing an engineer to work on one feeder while the rest of the panel is live.
*   **Withdrawable Design:** All ACBs and critical MCCBs must be "Fully Withdrawable" for rapid replacement.

## 3. Equipment Selection & Typical Ratings

| Component | Specification for AI DC | Reasoning |
| :--- | :--- | :--- |
| **Main Breakers** | Air Circuit Breakers (ACB) | High ampacity (3200A-6300A) and high Icu/Ics. |
| **Breaking Capacity** | {{cookiecutter.fault_level_ka}} kA | Must exceed the calculated fault level from transformers. |
| **Service Breaking ($I_{cs}$)** | 100% of $I_{cu}$ | Critical for DC; breaker must be reusable after a fault. |
| **Busbar Material** | Electrolytic Copper | Silver/Tin plated to resist {{cookiecutter.city}} environment. |

## 4. Automatic Transfer Scheme (ATS) Logic
The PCC manages the transition between {{cookiecutter.utility_provider}} and DG power.
1.  **Condition:** Utility voltage drops below 80% for >2 seconds.
2.  **Action:** Incomer 1 (Utility) trips.
3.  **Action:** "Start Signal" sent to DG Plant.
4.  **Condition:** DG reaches 95% voltage and frequency.
5.  **Action:** Incomer 2 (DG) closes.
6.  **Safety:** Electrical and Mechanical interlocks must prevent Utility and DG from ever being paralleled (unless designed for Closed Transition).

## 5. AI-Ready Design Considerations
1.  **Harmonic Derating:** The Neutral busbar must be **200%** of the Phase busbar capacity to handle 3rd harmonic currents from {{cookiecutter.ai_silicon_vendor}} servers.
2.  **Thermal Management:** {{cookiecutter.it_capacity_mw}} MW of power creates massive heat. Use **Internal Temperature Sensors** on busbar joints (connected to SCADA).
3.  **Electronic Trip Units:** Specify **LSIG** (Long time, Short time, Instantaneous, Ground fault) micro-processor based releases with integrated power metering.

## 6. Failure Modes
*   **Nuisance Tripping:** Inrush current from thousands of AI power supplies trips the "Instantaneous" (I) setting. *Mitigation:* Fine-tune coordination based on actual AI server inrush data.
*   **Busbar Flashover:** Dust and humidity lead to tracking. *Mitigation:* Use insulated busbars (Heat-shrink sleeves) and maintain room IP rating.

## 7. Design Checklist
- [ ] Is the form of separation Form 4b?
- [ ] Is the $I_{cs}$ rated at 100% of $I_{cu}$ ({{cookiecutter.fault_level_ka}} kA)?
- [ ] Has the panel been de-rated for {{cookiecutter.max_ambient_temp}}°C ambient temperature?
- [ ] Are the protection relays IEC 61850 compliant for EPMS integration?
