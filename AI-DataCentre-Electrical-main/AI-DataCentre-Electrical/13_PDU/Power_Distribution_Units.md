# Title: Power Distribution Units (PDU) - Floor-Mounted Distribution
## Purpose: To define the technical specifications, sizing, and monitoring requirements for floor-mounted PDUs in high-density AI data halls.
## Project: {{cookiecutter.project_name}}
## Tags: #PDU #PowerDistribution #IsolationTransformer #BranchCircuitMonitoring
## Standards Covered: IEC 61439-1, UL 60950, IEEE 1100, NFPA 75

---

## 1. Overview
The Power Distribution Unit (PDU) is the final large-scale distribution point in the data centre power chain. It typically takes high-ampacity input from the UPS and distributes it to branch circuits or track busways feeding the IT racks. 

## 2. Design Philosophy: The AI Shift
*   **High Capacity:** For {{cookiecutter.ai_silicon_vendor}} AI clusters, PDUs are sized massively, often between **500kVA and 1000kVA**.
*   **PDU-less Architecture vs. PDU:** In many hyperscale designs, floor PDUs are bypassed entirely in favor of direct-feed **Overhead Busways** to save white-space footprint. However, PDUs remain essential if galvanic isolation or local voltage step-down is required.

## 3. Engineering Calculations
### 3.1 PDU Capacity Sizing
*   **Formula:** $S_{pdu} = \frac{\sum P_{racks}}{PF \times \text{Diversity Factor}}$
*   **AI Diversity Factor:** Must be set to **1.0** (AI workloads run continuously at peak).
*   **Margin:** Always add a 20% expansion margin for future silicon generations.

### 3.2 Neutral Sizing
AI servers generate significant harmonic current.
*   **Requirement:** The PDU internal busbars and neutral conductor must be rated for **200% of the phase current**.

## 4. AI-Ready Technical Requirements
1.  **Isolation Transformer:** If used, it must be **K-13 or K-20 Rated** to handle harmonic heating and include an electrostatic shield to filter high-frequency noise.
2.  **Intelligent Monitoring (BCMS):** Must track $V, I, kW, kVA, PF,$ and $THD$ per circuit. This data is fed to the EPMS to calculate real-time PUE at the row level.
3.  **Front-Only Access:** To save expensive white-space floor area, specify PDUs that allow all maintenance and cabling from the front.

## 5. Failure Modes
*   **Sub-breaker Nuisance Tripping:** Caused by high inrush from {{cookiecutter.ai_silicon_vendor}} power shelves. *Mitigation:* Use MCCBs with adjustable "Short-time" and "Instantaneous" delay settings.
*   **Communication Loss:** BCMS gateway failure. *Mitigation:* Redundant Modbus/TCP or SNMP links.

## 6. Design Checklist
- [ ] Is the PDU rated for the full 1.0 PF load of the AI racks?
- [ ] Does the BCMS support EPMS integration?
- [ ] If a transformer is used, is it K-13 rated or higher?
- [ ] Is there a local Emergency Power Off (EPO) button with a protective cover (per local fire code)?
