# Title: Rack Level Distribution & AI Power Shelf Integration
## Purpose: To define the engineering requirements for power delivery within the IT rack, specifically focusing on {{cookiecutter.ai_silicon_vendor}} AI clusters.
## Tags: #RackPower #rPDU #PowerShelf #48VDC #{{cookiecutter.ai_silicon_vendor}}
## Standards Covered: IEC 60309, IEC 62368-1, OCP ORV3

---

## 1. Overview
In the {{cookiecutter.project_name}}, rack-level distribution has evolved from simple power strips (rPDUs) to complex **Power Shelves** and **DC Busbars**. "AI GPU Racks" (60kW - 120kW+) require fundamentally different electrical interfaces than standard 10kW racks.

## 2. The Shift to AI Architecture (OCP / Power Shelves)
Modern {{cookiecutter.ai_silicon_vendor}} infrastructure does not use individual power supplies for every server. Instead, it utilizes a **Centralized Power Shelf**.
*   **Input:** 415V/480V 3-Phase AC.
*   **Conversion:** Rectifiers convert AC to **48V DC** (or 54V DC).
*   **Distribution:** A massive vertical **Copper Busbar** at the rear of the rack delivers DC power to all GPUs via blind-mate connectors.

## 3. Engineering Calculations: Sizing the Rack Input
### 3.1 120kW AI Rack Feed
*   **Total Load:** 120,000 Watts.
*   **Redundancy:** Dual feeds (Source A and Source B).
*   **Formula:** $I = \frac{P}{\sqrt{3} \times V \times PF}$
*   **Requirement:** Since this is a continuous load, standard electrical codes require a 125% sizing factor for the breaker.
*   **Selection:** 250A to 400A 3-Phase Feed via Overhead Busway Plug-in Unit or Industrial Pin-and-Sleeve Connector (**e.g., IEC 60309**).

## 4. AI-Ready Design Requirements
1.  **Cord Management:** At 120kW+, the AC "Whip" cables are extremely heavy. Design for minimum bend radii to prevent terminal stress.
2.  **Phase Balancing:** Ensure that across the row, racks are phase-rotated (L1-L2-L3, L2-L3-L1, etc.) to keep the main UPS balanced.
3.  **48V DC Grounding:** Ensure the internal rack DC busbar is referenced correctly to the rack frame to prevent "Floating DC" potentials.

## 5. Construction & Layout
*   **Overhead Busway:** Mandatory for AI zones. It allows for the 250A+ plug-ins which cannot be easily managed under a raised floor.
*   **Rack Grounding:** Every rack must be bonded to the **Signal Reference Grid (SRG)** using a 16 sq.mm or 25 sq.mm flexible copper braid to protect the high-speed networking fabric.

## 6. Failure Modes
*   **Phase Loss:** One phase of the 3-phase feed drops. *Result:* Rectifiers may go into "Degraded Mode" or shutdown.
*   **Connector Overheating:** Loose pin-and-sleeve connection. *Mitigation:* Annual infrared (IR) scanning of all rack-level connectors.

## 7. Design Checklist
- [ ] Is the rack feed sized for 125% of the Peak TDP of the {{cookiecutter.ai_silicon_vendor}} cluster?
- [ ] Are the cables LSZH (Low Smoke Zero Halogen) to meet fire codes?
- [ ] Has the floor loading been verified for the massive weight of the liquid-filled power shelf + GPUs?
