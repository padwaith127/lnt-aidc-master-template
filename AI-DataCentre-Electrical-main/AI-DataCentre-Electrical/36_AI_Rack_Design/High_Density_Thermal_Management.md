# Title: AI Rack Design & High-Density Thermal-Electrical Management
## Purpose: To define the electrical and thermal interface requirements for 60kW to 120kW AI racks, focusing on NVIDIA GB200/Blackwell infrastructure.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #AIRack #NVIDIA #Blackwell #HighDensity #PowerShelf #ORV3 #Busbar #LTVyoma
## Related Files: [[Rack_Level_Distribution.md]], [[Liquid_Cooling.md]], [[NVIDIA_Architecture.md]], [[Short_Circuit.md]]
## Standards Covered: OCP Open Rack V3 (ORV3), ASHRAE TC 9.9, IEC 62368-1, IEEE 1584.1

---

## 1. Overview
In the L&T Mahape 40 MW facility, the "AI Rack" is no longer just a piece of furniture; it is a high-performance power conversion engine. At 120kW per rack (NVIDIA GB200 NVL72), the density is 10x to 20x higher than traditional enterprise racks. This requires a shift from AC-to-server distribution to a **Centralized DC Power Shelf** with a vertical **DC Busbar**.

## 2. The AI Power Shelf Architecture (ORV3 Standard)
Modern AI racks (NVIDIA/OCP) utilize a centralized power shelf to maximize efficiency and serviceability.
*   **Input:** Dual 415V 3-Phase AC feeds (Source A & B).
*   **Conversion:** 6 to 12 high-efficiency rectifiers (N+1 or N+N) converting AC to **48V DC** (or 54V DC).
*   **Backplane:** A massive vertical copper busbar delivering DC current to the GPU nodes.

### 2.1 Why 48V DC?
At 120kW, 12V DC distribution would require ~10,000 Amperes per rack, leading to massive $I^2R$ losses and unmanageable copper thickness. 48V DC reduces the current to ~2,500A, making distribution via a 3-inch busbar feasible.

## 3. Engineering Calculations: The Thermal-Electrical Nexus

### 3.1 Heat Dissipation Calculation
In an AI rack, 99.9% of electrical energy consumed is converted to heat.
*   **Total Heat ($Q_{total}$):** $120 \text{ kW} = 409,456 \text{ BTU/hr}$.
*   **Liquid vs. Air Split:** In a Direct-to-Chip (D2C) system:
    *   **Liquid (Cold Plate):** ~80% (96kW) is removed by the CDU.
    *   **Air (Fans):** ~20% (24kW) is rejected into the room.
*   **L&T Strategy:** The HVAC system in Mahape must still provide 24kW of air cooling *per AI rack* even if liquid cooling is primary.

### 3.2 DC Busbar Sizing (Rear of Rack)
*   **Current ($I$):** $120,000 \text{ W} / 48 \text{ V} = 2,500 \text{ Amperes}$.
*   **Busbar Cross-Section:** To limit voltage drop to $< 1\%$ and keep temperature rise $< 30^\circ \text{C}$:
    *   Required: ~1200 $mm^2$ of Copper.
    *   Standard ORV3 Busbar: Multi-layered copper with silver/tin plating.

## 4. Electrical Protection & Safety
1.  **DC Arc Flash:** 48V is below the 50V safety threshold in many standards, but the **available fault current** from the rectifier bank can be $> 20,000\text{A}$. An arc flash at this current can still cause significant equipment damage and molten metal splatter.
2.  **Circuit Breakers:** Every GPU node connects to the DC Busbar via a "Blind-mate" connector with an integrated high-speed electronic fuse or e-Fuse.
3.  **Selective Coordination:** The branch DC fuses must trip faster than the Main Rectifier Protection to prevent a single GPU short from taking down the entire 120kW rack.

## 5. Thermal-Electrical Integration (The NVIDIA "Cold Plate")
*   **Leak Detection Interlock:** The AI rack contains liquid manifolds. The electrical design must include **leak-sensing ropes** at the base of the rack, integrated with the CDU's pump-stop circuit and the rack's PDU trip.
*   **Condensation Management:** The secondary loop fluid must be kept above the **Room Dew Point** (calculated by the BMS) to prevent moisture from forming on the 48V DC busbars, which would cause an immediate short circuit.

## 6. AI-Ready Design Features (L&T Execution)

| Feature | Requirement | Reason |
| :--- | :--- | :--- |
| **Overhead Busway** | 250A or 400A Tap-offs | To feed the 120kW Power Shelf without floor clutter. |
| **Weight Loading** | 2,500 kg+ per rack | Fluid-filled racks + Copper busbars + GPUs are extremely heavy. |
| **EMC Shielding** | Class A / Class B | High-speed InfiniBand signals require isolation from VFD noise. |
| **Fiber Management** | Zero-U side channels | Massive amounts of networking fiber (NVLink) cannot block airflow. |

## 7. Commissioning & Testing
1.  **Rectifier Load Sharing:** Verify that all rectifiers in the power shelf share the DC load within $\pm 5\%$.
2.  **Thermal Soak Test:** Run the AI rack at 100% TDP for 12 hours. Use IR cameras to inspect the **AC input connectors** and **DC busbar joints**.
3.  **Flow-Power Interlock:** Simulate a CDU pump failure; verify the NVIDIA software/hardware initiates a "Graceful Shutdown" before the GPU temp reaches $85^\circ \text{C}$.

## 8. Failure Modes
*   **Busbar Contamination:** Dust/Humid air in Mahape causing tracking on the 48V DC backplane. *Mitigation:* Use IP2X rated busbar shrouds.
*   **Rectifier "Thermal Throttling":** Rectifiers overheating because they are located in the "hot" part of the power shelf. *Mitigation:* Dedicated fan modules for the power shelf.
*   **DC Over-voltage:** Faulty rectifier control causing $> 60\text{V}$ DC, which fries the GPU voltage regulators (VRMs).

---

## 9. Design Checklist
- [ ] Is the floor structural capacity $\geq$ 2500 kg/sqm?
- [ ] Are dual 3-phase feeds provided per AI Power Shelf?
- [ ] Is the leak detection system tied to the rack power trip?
- [ ] Is the DC busbar rated for the full 2500A+ continuous current?
- [ ] Are the AC input connectors (IEC 60309 63A/125A/250A) specified with locking mechanisms?

---
## 10. References
### Standards
* **OCP ORV3:** Open Rack V3 Specification (Power & Mechanical).
* **ASHRAE TC 9.9:** Thermal Guidelines for Data Processing Environments (2023 Update).
* **IEC 62368-1:** Safety for Communication Technology Equipment.

### Manufacturer Documents
* **NVIDIA:** "Blackwell GB200 NVL72 System Architecture White Paper."
* **Vertiv:** "High Density Power and Cooling Solutions for AI Infrastructure."
* **Advanced Energy:** "Power Shelf Solutions for OCP and AI Racks."

### Revision History
* 1.0: Initial AI Rack Electrical-Thermal Strategy for L&T Vyoma Mahape.

---
**Next File Recommendation:** `37_NVIDIA_Architecture/GPU_Infrastructure_Requirements.md` (Deep dive into the specific power profiles and infrastructure needs of H100, B200, and NVL72 clusters).