# Title: Remote Power Panels (RPP) - Secondary White Space Distribution
## Purpose: To define the technical specifications, circuit management, and monitoring requirements for RPPs in hyperscale management and network zones.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #RPP #CircuitBreaker #PowerDistribution #NetworkPower #Hyperscale #LTVyoma
## Related Files: [[Power_Distribution_Units.md]], [[Rack_Power.md]], [[Cable_Design.md]]
## Standards Covered: IEC 61439-1 & 2, IS 8623, UL 67, NFPA 70

---

## 1. Overview
A Remote Power Panel (RPP) is a high-density power distribution sub-panel without an internal isolation transformer. It serves as the transition point between the main UPS distribution and the individual IT racks. In the L&T Mahape 40 MW facility, RPPs are primarily utilized for the "Standard Density" zones, Management Clusters, and Network Core rooms where a high volume of small-ampacity (16A/32A) circuits is required.

## 2. Theory: Circuit Density vs. Footprint
The primary value of an RPP is providing the maximum number of branch circuits in the minimum "White Space" footprint.
*   **Pole Capacity:** Standard RPPs support 42, 84, or 168 poles (breaker slots).
*   **Form Factor:** Typically matches the dimensions of a standard IT rack (600mm width) to maintain cold/hot aisle symmetry.

## 3. Equipment Components & Selection

| Component | Specification | Purpose |
| :--- | :--- | :--- |
| **Main Lug / Breaker** | 100A to 400A (4-Pole) | Main input from PDU or UPS Panel. |
| **Panelboards** | 42-way or 84-way | Housing for branch circuit breakers. |
| **Branch Breakers** | 16A, 32A, or 63A (1P/3P) | Direct power to Rack PDUs (rPDUs). |
| **Monitoring** | Branch Circuit Monitoring (BCM) | Tracking kWh per breaker for billing/capacity. |
| **Chassis** | Finger-safe (IP20) | Safety for technicians during live additions. |

## 4. Engineering Calculations

### 4.1 Load Balancing
To prevent neutral current buildup and transformer saturation upstream, RPP loads must be balanced across the three phases (L1, L2, L3).
*   **Formula:** Deviation % = $\frac{(I_{max} - I_{avg})}{I_{avg}} \times 100$
*   **Target:** Deviation should be **< 10%**.
*   **Mentoring Tip:** As an L&T PM, always review the "Schedule of Work" to ensure the electrician hasn't loaded all single-phase servers onto the 'R' phase.

### 4.2 Sizing the Feeders
*   **Scenario:** An 84-pole RPP feeding 40 racks, each with dual 32A feeds (N+1).
*   **Calculation:** 
    *   Estimated running load per rack: 4 kW.
    *   Total running load: $40 \text{ racks} \times 4 \text{ kW} = 160 \text{ kW}$.
    *   **Main Breaker Sizing:** 
        $$I = \frac{160,000}{\sqrt{3} \times 415 \times 0.95} \approx 234 \text{ A}$$
    *   **Selection:** 400A Main Breaker (to allow for 80% loading rule and future growth).

## 5. AI-Ready Design Considerations: The "Management Plane"
While NVIDIA GPUs are fed by heavy Busways, the **Management Plane** (the servers that control the GPUs) still relies on RPPs.
1.  **High-Speed Management Switches:** AI clusters require massive InfiniBand or Ethernet switching fabrics. These switches have high port density and require redundant 32A feeds from RPPs.
2.  **Harmonic Tolerance:** Ensure RPP busbars are rated for the high-frequency switching noise typical of modern management servers.
3.  **Intelligent Metering:** Integration with **EPMS** is mandatory to ensure the "Non-GPU" power consumption is accurately tracked for PUE calculations.

## 6. Construction & Layout (L&T Standards)
*   **Front/Rear Access:** Most RPPs are "Front-Access Only" to allow placement against walls or at the end of rows.
*   **Cable Management:** Use high-density wire ways. For 168 poles, the volume of outgoing cables (e.g., 3C x 6 sq.mm) is significant; ensure the RPP top/bottom gland plates are oversized.
*   **Safety:** Use "Shrouded" busbars to allow for the safe installation of new breakers while the panel is energized.

## 7. Commissioning & Testing
1.  **Phase Rotation Test:** Verify R-Y-B sequence matches the source.
2.  **Continuity & Polarity:** Verify every branch circuit reaches the correct rack.
3.  **Labeling:** **Critical Step.** Every breaker must be labeled with the Rack ID and PDU ID (e.g., Rack A01-PDU-1).
4.  **BMS Integration:** Verify that the "Main Breaker Trip" and "Surge Arrestor Fail" alarms are appearing on the SCADA.

## 8. Failure Modes
*   **Phase Overload:** Adding too many single-phase loads to one bus, causing the main breaker to trip.
*   **Loose Neutral:** Leads to voltage fluctuations and destroyed server power supplies. *Mitigation:* Use "Double-bolt" neutral connections and regular torque audits.
*   **Label Mismatch:** Technician turns off the wrong breaker, dropping a live AI management server.

## 9. Design Checklist
- [ ] Is the RPP footprint compatible with the floor tile grid?
- [ ] Are the branch breakers rated for the required fault current ($I_{cn}$)?
- [ ] Does the BCM monitor neutral current?
- [ ] Are the breaker positions clearly numbered and mirrored in the software?
- [ ] Is there 25% "Spare Capacity" (physical space and ampacity) for expansion?

---
## 📚 References
### Standards
* **IEC 61439-2:** Low-voltage switchgear and controlgear assemblies – Part 2: Power switchgear and controlgear assemblies.
* **IS 8623:** Specification for Low-Voltage Switchgear and Controlgear Assemblies.
* **UL 67:** Standard for Panelboards.

### Manufacturer Documents
* **Schneider Electric:** "Square D Remote Power Panel (RPP) Catalog."
* **Vertiv:** "Liebert RPP Specifications and Installation Guide."
* **Eaton:** "Power Distribution Rack and RPP Application Guide."

### Revision History
* 1.0: Initial release for Mahape 40MW RPP Strategy.

---
**Next File Recommendation:** `15_Rack_Power/Rack_Level_Distribution.md` (Focusing on Rack PDUs (rPDUs) and the NVIDIA-specific power shelf interface).