# Title: Power Quality - Transient, Sag (Dip), and Swell Analysis
## Purpose: To define the engineering parameters for maintaining voltage stability and immunity against power quality disturbances in the {{cookiecutter.project_name}}.
## Project: {{cookiecutter.project_name}}
## Tags: #PowerQuality #VoltageSag #Transients #ITIC #CBEMA
## Standards Covered: IEEE 1159, ITIC (CBEMA) Curve, SEMI F47, IEC 61000-4-30 Class A

---

## 1. Overview
In a {{cookiecutter.it_capacity_mw}} MW AI data centre, AI GPU clusters are highly sensitive to **Voltage Sags (Dips)** and **Transients**. A voltage sag lasting only 50 milliseconds can trip the high-speed under-voltage protection in an {{cookiecutter.ai_silicon_vendor}} power shelf, causing a multi-million dollar training job to fail. 

## 2. The ITIC (CBEMA) Curve
The **ITIC Curve** is the design benchmark for Data Centres.
*   **Design Goal:** Ensure that the power delivered to the AI rack stays within the "No Interruption" zone of the curve.
*   **Ride-Through:** Modern AI power shelves typically have a **10ms to 20ms** hold-up time to survive very short sags without restarting.

## 3. Engineering Calculations: Sag Magnitude & Duration
### 3.1 Voltage Sag Magnitude at Bus ($V_{sag}$)
When a large liquid cooling pump or chiller starts:
$$V_{sag} = V_{pre-fault} \times \frac{Z_{fault}}{Z_{source} + Z_{transformer} + Z_{fault}}$$
*   **Strategy:** Ensure the sag at the UPS input never drops below 80% of nominal to prevent the UPS from "hunting" between Utility and Battery.

### 3.2 Transient Recovery Time
Following an AI load step-up (0 to 100%):
*   **Requirement:** The voltage must recover to $\pm 1\%$ of nominal within **20ms** (1 cycle). The UPS inverter's dynamic response is the primary defense here.

## 4. Mitigation Strategies for AI-Ready Sites
1.  **Surge Protective Devices (SPD):**
    *   Type 1 (Service Entrance): High energy handling at the {{cookiecutter.utility_voltage_kv}}kV yard.
    *   Type 2 (Distribution): Main LV/UPS Rooms.
    *   Type 3 (Point of Use): Inside AI Racks.
2.  **SEMI F47 Compliance:** Ensure all critical liquid cooling CDUs and VFDs are tested to **SEMI F47** standards (Voltage Sag Immunity) so cooling doesn't stop during a grid dip from {{cookiecutter.utility_provider}}.

## 5. Monitoring & Measurement
*   **Class A Meters:** Install IEC 61000-4-30 Class A meters at the Incoming and Main LT Incomers.
*   **Event Capture:** Meters must support **Waveform Capture** (1024 samples/cycle) to perform Root Cause Analysis (RCA) after a trip.

## 6. Design Checklist
- [ ] Are Class A PQ meters installed at all primary entry points?
- [ ] Do all SPDs have local and remote monitoring (dry contacts)?
- [ ] Has the UPS transient response been verified for a 100% load step?
- [ ] Are all mechanical/cooling controls compliant with SEMI F47 sag immunity?
