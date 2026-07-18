# Title: Relay Coordination & Protection Selectivity
## Purpose: To define the logic and methodology for ensuring that electrical faults are cleared at the point of origin without interrupting the wider {{cookiecutter.it_capacity_mw}} MW facility.
## Project: {{cookiecutter.project_name}}
## Tags: #ProtectionRelay #Selectivity #Coordination #IEEE242 #TCC #ShortCircuit
## Standards Covered: IEEE 242 (Buff Book), IEC 60255, Local AHJ Codes

---

## 1. Overview
In a {{cookiecutter.it_capacity_mw}} MW AI data centre, "Selectivity" is the difference between a minor rack-level incident and a catastrophic site-wide outage. Protective devices must be coordinated such that only the device closest to the fault trips. This is complicated by high-density {{cookiecutter.ai_silicon_vendor}} clusters that generate massive "Step-load" currents which can mimic fault conditions.

## 2. Protection Philosophy: Total Selectivity
*   **Definition:** For any value of short-circuit up to the maximum available fault current ({{cookiecutter.fault_level_ka}} kA), only the downstream protective device operates.
*   **Strategy:** We utilize a combination of **Current Grading**, **Time Grading**, and **Logic Discrimination** (GOOSE messaging via IEC 61850).

## 3. Engineering Workflow: The Coordination Study
Using ETAP or SKM PowerTools:
1.  **Short Circuit Analysis:** Determine max and min fault currents at every bus based on the {{cookiecutter.utility_voltage_kv}}kV source.
2.  **Define Device Envelopes:** Plot the Time-Current Characteristic (TCC) curves.
3.  **Adjust Settings:** Manipulate Pickup ($I_p$) and Time Dial ($T_d$) to ensure no curve overlap.
4.  **Verify Stability:** Ensure the Transformer Inrush and Cooling Pump Starting currents sit to the left of the trip curves.

## 4. Engineering Calculations: Setting the Relay
Standard "Normal Inverse" (NI) curve calculation (IEC 60255):
$$t = TMS \times \frac{0.14}{(I/I_s)^{0.02} - 1}$$
*   **Coordination Margin:** Maintain 0.2s to 0.3s gap between relays to allow for mechanical breaker opening time.

## 5. AI-Specific Coordination Challenges
1.  **GPU Step-Loads:** AI clusters can ramp from 10% to 100% load in milliseconds. This rate of change ($di/dt$) can confuse instantaneous elements.
    *   *Solution:* Use **"Definite Time"** delays for high-set instantaneous elements to ignore 20ms AI transients.
2.  **Transformer Inrush:** AI DC transformers (K-13 rated) are often oversized. Magnetization inrush can be 10-12x full-load current.
3.  **UPS Fault Current:** UPS systems have limited fault-clearing capacity (2-3x rated current). If the UPS cannot clear a downstream rack fault, it will drop to Bypass.
    *   *Solution:* Coordinate rack-level MCCBs to trip faster than the UPS static switch transfer time.

## 6. Equipment & Technology
*   **Numerical Relays:** Must support **IEC 61850 GOOSE** messaging to achieve **Bus-Zone Interlocking**. If a feeder relay sees a fault, it sends a "Block" signal to the Incomer, preventing the entire site from tripping.
*   **Trip Units:** Electronic trip units in ACBs must be set for **LSIG**.

## 7. Failure Modes
*   **Sympathetic Tripping:** A fault on Feeder A causes Feeder B to trip due to shared neutral transients.
*   **Protection Blindness:** Fault current is lower than the relay pickup (common in high-impedance grounding).

## 8. Design Checklist
- [ ] Is there a minimum 200ms-300ms gap between all TCC curves?
- [ ] Does the transformer primary relay ignore the Magnetizing Inrush?
- [ ] Is GOOSE messaging enabled for high-speed Bus-Zone protection?
