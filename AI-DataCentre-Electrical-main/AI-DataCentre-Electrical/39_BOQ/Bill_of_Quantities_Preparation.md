# Title: Bill of Quantities (BOQ) & Procurement Specifications
## Purpose: To define the methodology for quantifying, estimating, and specifying electrical components for a 40 MW AI-ready data centre.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #BOQ #Estimation #Procurement #CostEngineering #LTVyoma #QuantitySurvey
## Related Files: [[Standard_Drawing_Templates.md]], [[AI_Load_Estimation.md]], [[Transformer_Design.md]]
## Standards Covered: IS 1200 (Part 8), ISO 10845, RICS Black Book, CPWD Specifications

---

## 1. Overview
The Bill of Quantities (BOQ) is the commercial heart of the L&T Mahape project. It translates the 3D BIM model and 2D drawings into a line-item list of materials and labor. For an AI-ready facility, the BOQ must be exceptionally precise because specialized components (like 120kW-ready busway or Li-ion BESS) have long lead times and high capital costs. Mistakes in quantification here directly lead to project delays or budget overruns.

## 2. BOQ Structure: The "Work Breakdown"
A hyperscale electrical BOQ is typically divided into "Schedules" to align with procurement packages:

| Schedule | Description | Key Items |
| :--- | :--- | :--- |
| **Schedule A** | High Voltage (HT) System | 33kV GIS, Transformers, HT Cabling, Outdoor Gantry. |
| **Schedule B** | Low Voltage (LT) System | PCCs, MCCs, APFC Panels, Busducts. |
| **Schedule C** | UPS & Energy Storage | UPS Modules, Li-ion Battery Cabinets, DC Cabling. |
| **Schedule D** | Backup Power (DG) | DG Sets, Fuel System, Synchronization Panels, Acoustic Enclosures. |
| **Schedule E** | White Space Distribution | Track Busway, Tap-off Boxes, RPPs, rPDUs. |
| **Schedule F** | Containment & Cabling | Cable Trays, LT Power/Control Cables, Fire Sealing. |
| **Schedule G** | Earthing & Lightning | Earth Pits, Grounding Grid, Air Terminals, SPDs. |
| **Schedule H** | Automation & Monitoring | SCADA PLCs, EPMS Meters, BMS Integration. |

## 3. Estimation Methodology (IS 1200)
As an L&T PM, you must follow standard measurement codes to ensure the BOQ is "Audit-Proof."
*   **Cables:** Measured in Linear Meters (LM). Always add a **3% to 5% slack/wastage factor** for terminations and routing bends.
*   **Busducts:** Measured in Linear Meters. Include "Joint Kits" as part of the meterage or as separate items.
*   **Switchgear:** Measured in Numbers (Nos) or Sets. Ensure the "Incomer" and "Bus-Coupler" are distinct from "Outfeeders."
*   **Earthing:** Mesh is measured in LM (for flats) or Sqm (for mesh). Earth pits are measured in Nos.

## 4. AI-Ready BOQ Considerations
AI infrastructure introduces high-value items that are not present in standard DCs:

1.  **High-Density Track Busway:** Instead of standard 250A busway, the BOQ will reflect **800A to 1200A** track busway with a high density of **250A Tap-off units**.
2.  **Liquid Cooling Electricals:** Include items for CDU (Coolant Distribution Unit) power feeds and leak detection sensing cables (often overlooked in electrical BOQs).
3.  **K-Factor Transformers:** Ensure the transformer line item explicitly specifies "K-13" or "K-20" rating, as the cost premium is 15-25% over standard units.
4.  **BESS Safety:** Include specialized fire suppression (Aerosol or Novec) specifically for the battery cabinets as a line item if not in the Fire Schedule.

## 5. Worked Example: Quantifying Busway for an AI Row
**Scenario:** A row of 10 NVIDIA racks, each 120kW.
*   **Required Capacity:** 250A per rack at 415V.
*   **Busway Rating:** 1200A (to allow for diversity and future growth).
*   **BOQ Line Items:**
    1.  *Main Busway Run:* 1200A, 3P4W, 200% Neutral, Copper - **12 Meters**.
    2.  *End Feed Box:* 1200A with Protection - **1 No**.
    3.  *Tap-off Units:* 250A, 3P, with Energy Metering & LSI Breaker - **10 Nos**.
    4.  *Installation & Testing:* Per meter and per tap-off.

## 6. Technical Specifications for Procurement
Every line item in the BOQ must reference a **Technical Specification (TS)** document.
*   **"Make List":** L&T standardizes on top-tier vendors (Schneider, ABB, Siemens, Cummins, CAT).
*   **Compliance:** The vendor must provide "Point-by-Point" compliance to the TS before the Purchase Order (PO) is issued.
*   **Lead Times:** Explicitly state the required "On-Site Date." For transformers in Mahape, this may be **24-32 weeks**.

## 7. Common Mistakes in BOQ Preparation
*   **Forgetting Terminations:** Lugs and glands for 300 sq.mm cables are expensive; if they aren't in the BOQ, the contractor will claim an "extra."
*   **Missing Support Systems:** Cable trays need rods, channels, and anchors. Quantify the **Structural Support** separately.
*   **Inadequate Spares:** Not including the 5% mandatory operational spares in the initial procurement.
*   **VFD/Soft Starter Confusion:** Listing a "Chiller Feed" but forgetting the specialized motor starter or VFD required by the design.

## 8. Construction Sequence Integration
The BOQ should follow the construction logic of the Mahape site:
1.  *Long-Lead Items:* (Transformers, GIS, DGs) - Ordered in Month 1.
2.  *First Fix:* (Earthing, Embedded conduits, Trays) - Ordered in Month 3.
3.  *Second Fix:* (Panels, Cables, Busducts) - Ordered in Month 6.
4.  *Final Fix:* (Wiring, Lighting, rPDUs) - Ordered in Month 9.

---

## 9. Design Checklist
- [ ] Are all line items traceable to a GFC (Good for Construction) drawing?
- [ ] Has a 5% wastage factor been applied to cables?
- [ ] Is the "Neutral Sizing" (100% or 200%) clearly specified in busway/cable items?
- [ ] Are bimetallic lugs included for Aluminum-to-Copper connections?
- [ ] Has the "Installation, Testing & Commissioning" (ITC) component been included for every equipment item?

---
## 10. References
### Standards
* **IS 1200 (Part 8):** Method of Measurement of Building and Civil Engineering Works - Electrical Works.
* **ISO 10845:** Construction procurement.
* **CPWD Specifications:** For electrical works in the Indian context.

### Manufacturer Price Lists (Internal L&T Reference)
* **ABB/Schneider:** Latest LP (List Price) and Multiplier sheets.
* **Polycab/Havells:** Latest copper/aluminum index for cable pricing.

### Revision History
* 1.0: Initial BOQ Methodology for L&T Vyoma Mahape project.

---
**Next File Recommendation:** `40_Calculations/Master_Formula_Reference.md` (A centralized "Cheat Sheet" of every formula used in this repository for quick engineering checks).