# Title: Power Distribution Units (PDU) - Floor-Mounted Distribution
## Purpose: To define the technical specifications, sizing, and monitoring requirements for floor-mounted PDUs in high-density AI data halls.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #PDU #PowerDistribution #IsolationTransformer #BranchCircuitMonitoring #AI-Infrastructure #LTVyoma
## Related Files: [[UPS_System_Design.md]], [[Busbar_Distribution.md]], [[Rack_Power.md]], [[EPMS.md]]
## Standards Covered: IEC 61439-1, UL 60950, IEEE 1100, NFPA 75, IS 8623

---

## 1. Overview
The Power Distribution Unit (PDU) is the final large-scale distribution point in the data centre power chain. It typically takes high-ampacity input from the UPS (e.g., 400A - 800A) and distributes it to multiple branch circuits or busway runs that feed the IT racks. In the L&T Mahape project, PDUs serve as critical points for electrical isolation and granular energy metering.

## 2. Design Philosophy: The AI Shift
Traditional PDUs (150kVA - 300kVA) are often insufficient for AI clusters. 
*   **High Capacity:** For NVIDIA H100/B200 clusters, PDUs are now sized between **500kVA and 800kVA**.
*   **PDU-less Architecture:** In many hyperscale AI designs, the floor PDU is bypassed in favor of direct-feed **Overhead Busways** to reduce footprint and increase efficiency. However, PDUs remain essential for legacy zones and localized isolation.

## 3. Equipment Components & Selection

| Component | Specification | Purpose |
| :--- | :--- | :--- |
| **Main Incomer** | 4-Pole ACB or MCCB | Primary protection and isolation. |
| **Isolation Transformer** | K-13 or K-20 Rated | (Optional) To create a new Neutral-Ground bond and filter noise. |
| **Branch Breakers** | 63A - 125A MCCBs | Feeding individual AI racks or Busway segments. |
| **Monitoring (BCMS)** | Branch Circuit Monitoring System | Revenue-grade metering (Class 0.5) per circuit. |
| **SPD** | Type 2 Surge Protection | Protecting AI power shelves from switching transients. |

## 4. Engineering Calculations

### 4.1 PDU Capacity Sizing
*   **Formula:** $S_{pdu} = \frac{\sum P_{racks}}{PF \times \text{Diversity Factor}}$
*   **Worked Example (AI Cluster):**
    *   One row of 10 AI Racks at 40kW each = 400kW.
    *   Assume Output PF = 1.0.
    *   Diversity Factor = 1.0 (AI workloads are continuous).
    *   $S_{pdu} = \frac{400}{1.0 \times 1.0} = 400 \text{ kVA}$.
    *   **Selection:** 500 kVA PDU (to provide 20% expansion margin).

### 4.2 Neutral Sizing
AI servers generate significant harmonic current.
*   **Requirement:** The PDU internal busbars and neutral conductor must be rated for **200% of the phase current**.
*   **Reasoning:** 3rd harmonic currents (Triplens) from single-phase SMPS add up in the neutral rather than canceling out.

## 5. AI-Ready Technical Requirements
1.  **High-Frequency Noise Filtering:** AI GPU clusters are extremely sensitive to high-frequency transients. If using a transformer-based PDU, ensure it has an electrostatic shield.
2.  **Intelligent Monitoring (BCMS):** Must track $V, I, kW, kVA, PF,$ and $THD$ per circuit. This data is critical for the L&T EPMS to calculate real-time PUE at the row level.
3.  **Front-Only Access:** To save expensive white-space floor area in Mahape, specify PDUs that allow all maintenance and cabling from the front.

## 6. Construction & Layout (L&T Standards)
*   **Location:** Placed at the end of the row (EoR) or middle of the row (MoR).
*   **Cabling:** Usually bottom entry via a raised floor (600mm - 1000mm height) or top entry via overhead cable ladders.
*   **Seismic Bracing:** Must be bolted to the sub-floor (concrete slab) to meet Zone III requirements.

## 7. Commissioning & Testing
1.  **Transformer Insulation Test:** (If applicable) Megger primary to secondary and to earth.
2.  **BCMS Calibration:** Verify that the PDU display matches a calibrated handheld power analyzer.
3.  **Thermal Imaging:** Conduct an IR scan of all branch breaker terminations under 100% load (using load banks).
4.  **Grounding Verification:** Ensure the PDU cabinet is bonded to the Signal Reference Grid (SRG).

## 8. Failure Modes
*   **Sub-breaker Nuisance Tripping:** Caused by high inrush from AI power shelves. *Mitigation:* Use breakers with adjustable "Short-time" delay settings.
*   **Neutral Overheating:** Undersized neutral busbar handling harmonic loads. *Mitigation:* 200% Neutral sizing.
*   **Communication Loss:** BCMS gateway failure. *Mitigation:* Redundant Modbus/TCP links.

## 9. Design Checklist
- [ ] Is the PDU rated for the full 1.0 PF load of the AI racks?
- [ ] Does the BCMS support SNMP or Modbus for EPMS integration?
- [ ] If a transformer is used, is it K-13 rated or higher?
- [ ] Are the branch breakers "Hot-swappable" (if required by client)?
- [ ] Is there a local Emergency Power Off (EPO) button with a protective cover?

---
## 📚 References
### Standards
* **IEEE 1100:** Recommended Practice for Powering and Grounding Electronic Equipment (Emerald Book).
* **IEC 61439-1:** Low-voltage switchgear and controlgear assemblies.
* **NFPA 75:** Standard for the Fire Protection of Information Technology Equipment.

### Manufacturer Documents
* **Schneider Electric:** "APC InfraStruxure PDU Technical Data."
* **Vertiv:** "Liebert PPC (Precision Power Center) User Manual."
* **Eaton:** "Power Distribution Rack (PDR) Specifications."

### Revision History
* 1.0: Initial release for Mahape 40MW PDU Strategy.

---
**Next File Recommendation:** `14_RPP/Remote_Power_Panels.md` (Focusing on the secondary distribution layer for standard-density zones).