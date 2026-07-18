# Title: Emergency Backup Generation - DG System Design
## Purpose: To define the engineering requirements for a 40 MW+ standby power plant using Diesel Generators (DG) for hyperscale AI workloads.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #DieselGenerator #BackupPower #DCC-Rating #Hyperscale #Mahape #LTVyoma
## Related Files: [[Transformer_Design.md]], [[UPS_System.md]], [[Fuel_System.md]], [[Generator_Sync.md]]
## Standards Covered: ISO 8528, CPCB IV+, IEEE 446, NFPA 110, Uptime Tier III/IV

---

## 1. Overview
In a 40 MW AI-ready facility, the Diesel Generator (DG) system is the ultimate guarantor of availability. For the Mahape project, the DG plant must be capable of supporting the full facility load (IT + Cooling + Ancillary) indefinitely during a utility failure. Given the AI focus, the system must handle massive load steps and maintain frequency stability to support UPS charging and CDU (Liquid Cooling) operations.

## 2. Engineering Philosophy: The "Data Centre Continuous" (DCC) Rating
Traditional "Standby" or "Prime" ratings are insufficient for hyperscale DCs.
*   **DCC Rating (ISO 8528):** Defined by the Uptime Institute and major OEMs (Cummins/CAT). It allows the generator to run at a constant or varying load for unlimited hours, specifically for data centre applications where the utility is the primary source.
*   **Performance Class G3:** Mandatory for Data Centres. It defines strict limits on frequency and voltage deviations during load steps.

## 3. Equipment Selection & Sizing

### 3.1 Sizing Logic
For a 40 MW IT load (~55 MVA Total Facility Load):
*   **Unit Sizing:** Typically use **3.25 MVA (3000 kWe) or 4 MVA** units at 11kV.
*   **Redundancy:** N+1 or N+2 at the "Block" or "System" level.
*   **Example Configuration:** 20 x 3.25 MVA units (distributed across blocks).

### 3.2 Derating Factors (Mumbai Context)
The nameplate rating must be derated for local conditions in Mahape:
1.  **Ambient Temperature:** 45°C - 50°C (requires oversized radiators).
2.  **Altitude:** Sea level (minimal impact).
3.  **Humidity:** High (requires anti-condensation heaters in the alternator).

## 4. Engineering Calculations

### 4.1 Step Load Calculation
AI clusters cause high "Step Loads" during recovery.
*   **Formula:** $P_{step} = \text{UPS Input} + \text{Chiller/CDU Inrush} + \text{Battery Charging}$.
*   **Requirement:** The DG must accept 60% of its rated load in the first step without the frequency dropping below 45 Hz (per ISO 8528-5).

### 4.2 Fuel Autonomy Calculation
*   **Assumption:** 40 MW IT load + 15 MW Cooling = 55 MW total.
*   **Fuel Consumption:** ~200 Liters/Hour per MW of load.
*   **Calculation for 48 Hours:** 
    $$V_{fuel} = 55 \text{ MW} \times 200 \text{ L/MW/hr} \times 48 \text{ hr} = 528,000 \text{ Liters}$$
*   **Tank Strategy:** Bulk Storage (Underground/Above ground) + Day Tanks (near each DG).

## 5. AI-Ready Design Features
1.  **Fast Start-Up:** "Black Start" to "Ready-to-Load" in **< 15 seconds**. This is critical as Lithium-ion UPS runtimes are often sized for only 5-10 minutes.
2.  **Isochronous Load Sharing:** Using digital governors (e.g., DeepSea or ComAp) to ensure all parallel units share the load precisely.
3.  **Permanent Magnet Generator (PMG):** For superior short-circuit sustainment and cleaner power to the voltage regulator (AVR).

## 6. Statutory Compliance (India Specific)
*   **CPCB IV+ Emission Norms:** Mandatory for all new DG sets in India from 2024. Requires sophisticated after-treatment (SCR/DPF).
*   **Acoustics:** Noise level < 75 dB(A) at 1 meter from the enclosure (as per MoEFCC guidelines).
*   **Stack Height:** Minimum height calculated as $H = h + 0.2 \times \sqrt{kVA}$, where $h$ is the building height.

## 7. Layout & Installation (L&T Standards)
*   **Location:** Typically on the ground floor or a dedicated DG building. Roof-top placement requires massive structural reinforcement and vibration isolation (Spring isolators).
*   **Airflow:** Massive CFM requirements. Avoid "Hot Air Recirculation" by using ducting/louvers oriented with prevailing Mumbai winds.
*   **Fuel Piping:** Double-walled piping with "Leak Detection" sensors.

## 8. Commissioning: The Integrated Systems Test (IST)
The DG system is not "ready" until it passes the **Black Start Test**:
1.  **Load Bank Testing:** Each DG tested at 25%, 50%, 75%, 100%, and 110% load.
2.  **Step Load Test:** Verify G3 performance using a reactive load bank.
3.  **Synchronization Test:** Verify that all 20+ units can sync to a common bus within the required time window.
4.  **Heat Run:** 8-24 hour continuous run at 100% load to check for radiator/cooling system adequacy.

## 9. Failure Modes & Common Mistakes
*   **Fuel Contamination:** Algae growth in diesel due to Mumbai humidity. *Mitigation:* Fuel polishing systems.
*   **Wet Stacking:** Running DGs at low load (<30%) during testing causes unburnt fuel in the exhaust. *Mitigation:* Regular load bank testing.
*   **Vibration Transfer:** DG vibration affecting sensitive IT racks/liquid cooling pumps. *Mitigation:* High-efficiency anti-vibration mounts (AVM).

---

## 10. Design Checklist
- [ ] Are the DGs CPCB IV+ compliant?
- [ ] Is the "Data Centre Continuous" (DCC) rating certificate provided by the OEM?
- [ ] Has the fuel system been sized for 48 hours of autonomous run?
- [ ] Is the radiator sized for 50°C ambient to prevent "High Temp" trips during Mumbai summers?
- [ ] Are the starter batteries redundant (Dual-starter motors)?

---
## 📚 References
### Standards
* **ISO 8528-1:** Reciprocating internal combustion engine driven alternating current generating sets.
* **Uptime Institute:** Tier Standard: Topology (Requirements for Engine-Generators).
* **NFPA 110:** Standard for Emergency and Standby Power Systems.

### Manufacturer Documents
* **Cummins:** "Data Center Continuous (DCC) Rating Technical Paper."
* **Caterpillar:** "Electric Power SpecSizer for Data Centers."

### Revision History
* 1.0: Initial backup power strategy for 40 MW Mahape DC.

---
**Next File Recommendation:** `08_UPS/UPS_System_Design.md` (Focusing on the 40 MW Power Conditioning and BESS).