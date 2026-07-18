# Title: Root Cause Analysis (RCA) & Forensic Engineering
## Purpose: To define the investigative framework and technical methodology for analyzing electrical failures and unplanned outages in a {{ cookiecutter.it_capacity_mw }} MW AI-ready facility.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #RCA #FailureAnalysis #ForensicEngineering #5Whys #Ishikawa #OutageInvestigation #{{ cookiecutter.project_code }}
## Related Files: [[Electrical_Power_Monitoring.md]], [[Supervisory_Control.md]], [[Relay_Coordination_and_Selectivity.md]], [[Standard_Operating_Procedures.md]]
## Standards Covered: IEEE 3007.3, NFPA 70B, ISO 9001:2015, IEEE 1159

---

## 1. Overview
In a {{ cookiecutter.it_capacity_mw }} MW hyperscale environment, an unplanned outage is a high-stakes event. For the {{ cookiecutter.project_name }} {{ cookiecutter.city }} project, "fixing it and moving on" is insufficient. A formal **Root Cause Analysis (RCA)** is required to identify the underlying cause and prevent recurrence. This module provides the forensic tools to investigate complex interactions between high-density AI loads and the electrical power train.

## 2. Theoretical Framework: The 3 Layers of Failure
When an {{ cookiecutter.ai_silicon_vendor }} GPU cluster drops, we investigate three distinct layers:
1.  **The Physical Root Cause:** What physically failed? (e.g., a busbar insulator tracked).
2.  **The Human Root Cause:** Did a technician follow the MOP? Was there a design error?
3.  **The Latent (Systemic) Root Cause:** Was the maintenance interval too long? Was the protection setting too aggressive for AI step-loads?

## 3. The Forensic Toolkit: Data Acquisition
To conduct an RCA at the {{ cookiecutter.city }} site, engineers must extract data from:
*   **Sequence of Events (SOE):** From the SCADA system, time-stamped to 1ms.
*   **Waveform Capture:** From Class A EPMS meters to see the exact voltage/current sine waves during the fault.
*   **Relay Disturbance Records:** COMTRADE files from protection relays.
*   **Thermal Historian:** Checking BMS logs for temperature spikes leading up to the event.

## 4. Investigative Methodologies

### 4.1 The "5 Whys" Method
Simple but effective for linear failures.
*   *Problem:* The Main ACB tripped.
    1.  *Why?* The overcurrent protection operated.
    2.  *Why?* The current surged to 120% of the rating.
    3.  *Why?* The AI cluster initiated a massive training restart simultaneously.
    4.  *Why?* The "Sequential Loading" logic in the SCADA failed to execute.
    5.  *Why?* A recent software patch corrupted the PLC code. (**Root Cause**)

### 4.2 Ishikawa (Fishbone) Diagram
Used for complex outages involving multiple systems (Electrical, Mechanical, Control).
*   **Categories:** Manpower, Method, Machine, Material, Measurement, Environment.

### 4.3 Fault Tree Analysis (FTA)
A top-down deductive logic approach (Boolean logic) to find the combination of events that caused the system-level failure.

## 5. AI-Specific Failure Scenarios

### 5.1 Sympathetic Tripping
*   **Scenario:** A fault in one {{ cookiecutter.rack_density_kw }}kW rack causes an adjacent, healthy rack to trip.
*   **Analysis:** High-frequency transients through shared grounding (SRG) or neutral-to-earth voltage spikes ($V_{N-E}$) triggering sensitive SMPS protection.

### 5.2 BESS Thermal Runaway
*   **Scenario:** A Lithium-ion battery cabinet catches fire.
*   **Analysis:** Failure of the BMS to detect a single-cell over-voltage or an internal dendrite short circuit.

### 5.3 Harmonic Resonance Outage
*   **Scenario:** UPS capacitor banks fail during a specific AI compute cycle.
*   **Analysis:** The AI server's switching frequency matched the system's resonant frequency, magnifying current by 5x-10x.

## 6. Engineering Calculations: Fault Magnitude Estimation
Forensic engineers must verify the data against theory.
*   **Formula:** $I_f = \frac{V_{LN}}{Z_{source} + Z_{cable} + Z_{arc}}$
*   **Application:** If the relay recorded 25kA but the calculation suggests 50kA, there was significant **Arc Resistance** or a high-impedance fault.

## 7. The Post-Mortem Workflow
1.  **Preservation:** Freeze all logs and prevent anyone from clearing alarms.
2.  **Timeline Construction:** Align all time-stamps (SCADA, EPMS, Relay) to a single Master Clock.
3.  **Hypothesis Testing:** "If it was a transformer fault, why didn't the Buchholz relay trip?"
4.  **Action Plan:** Identify CAPA (Corrective and Preventive Actions).
5.  **Reporting:** Issue a professional RCA report to Management and the Client.

## 8. Common Mistakes in Investigations
*   **Blaming the Operator:** Stopping at "Human Error" without asking *why* the system allowed the error.
*   **Data Erasure:** Resetting the breaker before downloading the trip unit logs.
*   **Confirmation Bias:** Deciding the cause was "Lightning" before checking the keraunic data for that day.

## 9. Failure Modes of the RCA Process
*   **Incomplete Data:** Meters weren't synchronized, making it impossible to see what happened first.
*   **Lack of Expertise:** Not involving the relay manufacturer to decode the COMTRADE file.

---

## 10. RCA Checklist (Post-Outage)
- [ ] Are all relay COMTRADE files downloaded?
- [ ] Is the EPMS waveform capture exported as a CSV/PQDIF?
- [ ] Have the operators been interviewed separately to avoid "Group Think"?
- [ ] Was the weather/grid condition at the time of the fault recorded?
- [ ] Has a "Fishbone" session been scheduled with the mechanical and electrical teams?

---
## 11. References
### Standards
* **IEEE 3007.3:** Recommended Practice for Electrical Power System Operations and Maintenance.
* **NFPA 70B:** Standard for Electrical Equipment Maintenance (Forensic section).
* **IEEE 1159:** Recommended Practice for Monitoring Electric Power Quality.

### Research Papers
* **IEEE Paper:** *"Forensic Analysis of Power System Blackouts,"* 2020.
* **Uptime Institute:** *"Post-Mortem: Why Data Centers Fail."*

### Revision History
* 1.0: Initial RCA Methodology for {{ cookiecutter.project_name }} {{ cookiecutter.city }} project.

---
**Next File Recommendation:** `Hyperscale_Outage_Lessons.md` (Analyzing real-world failures to avoid them at {{ cookiecutter.city }}).
