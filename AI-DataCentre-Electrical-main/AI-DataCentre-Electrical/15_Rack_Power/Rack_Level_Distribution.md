# Title: Rack Level Distribution & AI Power Shelf Integration
## Purpose: To define the engineering requirements for power delivery within the IT rack, specifically focusing on high-density AI clusters and NVIDIA infrastructure.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #RackPower #rPDU #NVIDIA #PowerShelf #Blackwell #GB200 #48VDC #LTVyoma
## Related Files: [[AI_Load_Estimation.md]], [[Busbar_Distribution.md]], [[PDU_Design.md]], [[NVIDIA_Architecture.md]]
## Standards Covered: IEC 60309, IEC 62368-1, NFPA 70 Art 645, UL 60950-1

---

## 1. Overview
The IT rack is the final destination of the 40 MW power chain. In an AI-ready facility like Mahape, the rack-level distribution has evolved from simple power strips to complex **Power Shelves** and **DC Busbars**. As an L&T engineer, you must distinguish between "Standard IT Racks" (10-15kW) and "AI GPU Racks" (40kW - 120kW), which require fundamentally different electrical interfaces.

## 2. The Shift to NVIDIA AI Architecture
Modern NVIDIA infrastructure (e.g., GB200 NVL72) does not use individual power supplies for every server. Instead, it utilizes a **Centralized Power Shelf**.
*   **Input:** 415V 3-Phase AC.
*   **Conversion:** Rectifiers convert AC to **48V DC** (or 54V DC).
*   **Distribution:** A vertical **Copper Busbar** at the rear of the rack delivers DC power to all GPUs/Nodes via blind-mate connectors.

## 3. Equipment Selection: rPDUs vs. Power Shelves

| Feature | Intelligent Rack PDU (rPDU) | NVIDIA / OCP Power Shelf |
| :--- | :--- | :--- |
| **Typical Load** | 5kW - 30kW | 30kW - 120kW+ |
| **Voltage Out** | 240V AC (C13/C19 outlets) | 48V / 54V DC (Busbar) |
| **Form Factor** | Zero-U (Vertical) | 1U - 3U Rack Mount |
| **Application** | Standard Compute / Storage | NVIDIA Blackwell / Grace-Hopper |
| **Redundancy** | Dual rPDUs (A & B Feed) | N+1 or N+N Rectifier Redundancy |

## 4. Engineering Calculations: Sizing the Rack Input

### 4.1 120kW AI Rack Feed (NVIDIA Blackwell NVL72)
*   **Total Load:** 120,000 Watts.
*   **Voltage:** 415V, 3-Phase.
*   **Redundancy:** Dual feeds (Source A and Source B).
*   **Formula:**
    $$I = \frac{P}{\sqrt{3} \times V \times PF}$$
*   **Calculation:**
    $$I = \frac{120,000}{1.732 \times 415 \times 0.99} \approx 169 \text{ Amperes}$$
*   **Requirement:** Since this is a continuous load in a Data Centre, the NEC (NFPA 70) requires a 125% sizing factor.
    $$I_{breaker} = 169 \text{ A} \times 1.25 = 211 \text{ A}$$
*   **Selection:** 250A 3-Phase Feed via Overhead Busway Plug-in Unit or Industrial Pin-and-Sleeve Connector (**IEC 60309 250A**).

## 5. AI-Ready Design Requirements
1.  **Cord Management:** At 120kW, the "Whip" cables are extremely heavy and thick. Design for minimum bend radii to prevent terminal stress.
2.  **Phase Balancing:** AI racks draw massive current. Ensure that across the row, racks are rotated (Rack 1: L1-L2-L3, Rack 2: L2-L3-L1, etc.) to keep the main UPS balanced.
3.  **Harmonic Interaction:** High-density rectifiers in power shelves can interact with UPS output filters. Ensure the Power Shelf has **Active Power Factor Correction (PFC)** with THDi < 5%.
4.  **48V DC Grounding:** Ensure the internal rack DC busbar is referenced correctly to the rack frame to prevent "Floating DC" potentials.

## 6. Construction & Layout (L&T Execution)
*   **Overhead vs. Underfloor:** For Mahape, **Overhead Busway** is mandatory for AI zones. It allows for the 250A+ plug-ins required for NVIDIA racks which cannot be easily managed under a raised floor.
*   **Busbar Tapping:** Ensure the "Tap-off" box has a local breaker to allow for safe "Hot-swapping" of the rack power feed.
*   **Rack Grounding:** Every rack must be bonded to the **Signal Reference Grid (SRG)** using a 16 sq.mm or 25 sq.mm flexible copper braid.

## 7. Commissioning & Testing
1.  **Visual Inspection:** Verify that the IEC 60309 connectors are fully seated and locked.
2.  **Voltage Verification:** Measure L-L and L-N at the input to the NVIDIA Power Shelf.
3.  **BMS Communication:** Verify that the Rack PDU or Power Shelf IP address is reachable and reporting kW/Amps to the EPMS.
4.  **Load Test:** Use a "Heat Load" simulator to verify the rack feed handles 100% load without thermal hotspots at the connectors.

## 8. Failure Modes
*   **Phase Loss:** One phase of the 3-phase feed drops. *Result:* NVIDIA power shelf rectifiers may go into "Degraded Mode" or shutdown.
*   **Connector Overheating:** Loose pin-and-sleeve connection. *Mitigation:* Annual infrared (IR) scanning of all rack-level connectors.
*   **Rectifier Failure:** Internal to the power shelf. *Mitigation:* Specify N+1 rectifiers per shelf.

## 9. Design Checklist
- [ ] Is the rack feed sized for 125% of the Peak TDP of the GPU cluster?
- [ ] Are the cables LSZH (Low Smoke Zero Halogen) to meet Indian NBC/Fire codes?
- [ ] For 120kW racks, has the floor loading been verified for the weight of the power shelf + GPUs?
- [ ] Is there clear labeling on the A and B feed cables?
- [ ] Are the rPDUs/Power Shelves equipped with "Vertical" form factors to avoid blocking airflow?

---
## 📚 References
### Standards
* **IEC 60309:** Plugs, socket-outlets and couplers for industrial purposes.
* **NVIDIA Blackwell Infrastructure Gold Site Survey:** (Partner Access).
* **OCP (Open Compute Project):** Open Rack V3 (ORV3) Power Distribution Specifications.

### Manufacturer Documents
* **Server Technology / Raritan:** "High Power rPDU Application Guide."
* **Vertiv:** "Geist Intelligent PDU Manual."
* **NVIDIA:** "Data Center Deployment Guide for DGX Systems."

### Revision History
* 1.0: Initial release for Mahape 40MW Rack Distribution.

---
**Next File Recommendation:** `16_Cable_Design/Sizing_and_Routing.md` (Focusing on the 415V and 11kV cabling across the facility).