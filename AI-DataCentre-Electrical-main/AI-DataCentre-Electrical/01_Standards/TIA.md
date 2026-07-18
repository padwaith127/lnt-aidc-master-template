# Title: ANSI/TIA-942-C Infrastructure Standard for Data Centres
## Purpose: To define the infrastructure topology, pathways, and spaces required for a Tier-rated hyperscale facility.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #TIA942 #Topology #DataCentreDesign #Infrastructure #Pathways #LTVyoma
## Related Files: [[Uptime.md]], [[Standard_Layouts.md]], [[Rack_Level_Distribution.md]]
## Standards Covered: TIA-942-C (2024), TIA-568, TIA-569, TIA-606

---

## 1. Overview
The **TIA-942** (Telecommunications Industry Association) standard is the comprehensive architectural and electrical "blueprint" for data centres. While Uptime focuses on *outcomes* (Availability), TIA-942 focuses on *inputs* (How to build it). For the L&T Mahape project, the latest **TIA-942-C (2024)** edition governs the physical structure of the 40 MW plant.

## 2. Infrastructure Rating Levels (Rated 1-4)
TIA-942 uses "Rated" levels (similar to Uptime Tiers):
*   **Rated 3 (Concurrently Maintainable):** No shutdown required for any component maintenance. This is the L&T Mahape target.
*   **Rated 4 (Fault Tolerant):** Redundant systems that can handle a "Single Point of Failure" without impacting the load.

## 3. Key Electrical & Telecommunication Requirements

### 3.1 Pathways and Spaces
*   **Redundancy:** Dual cable entry rooms (EF - Entrance Facilities) on opposite sides of the building.
*   **Separation:** Mandatory physical separation between Power and Data pathways (minimum 600mm) to avoid EMI on InfiniBand AI links.

### 3.2 Racks and Cabinets
*   **Clearance:** Minimum 1.2m (4 ft) in front of cabinets and 0.9m (3 ft) at the rear. 
*   **Weight:** Floor must support the weight of fully populated high-density AI racks (Module 36).

### 3.3 Power Distribution
*   **Two Paths:** Every critical IT load must be "Dual-Corded," fed by two independent PDUs/Busways originating from two independent UPS systems.

## 4. AI-Ready Design Adjustments (TIA-942-C Updates)
The 2024 edition of TIA-942 specifically addresses high-density needs:
1.  **Liquid Cooling Infrastructure:** Now includes requirements for CDU placement and secondary loop piping pathways within the white space.
2.  **Enhanced Grounding:** Specific requirements for the **Signal Reference Grid (SRG)** to support high-frequency AI networking.

## 5. TIA-942 vs. Uptime Institute
| Feature | TIA-942 | Uptime Institute |
| :--- | :--- | :--- |
| **Scope** | Complete (Arch, Elec, Mech, Telecom) | Functional (Elec & Mech only) |
| **Certification** | Audit-based by TIA-certified auditors | Certification by Uptime Staff |
| **Focus** | Physical layout and specifications | Operational Availability and Topology |

## 6. Design Checklist (TIA-942 Compliance)
- [ ] Are there dual Entrance Facilities (Fiber entry) for the building?
- [ ] Are the pathways for Power and Data physically separated?
- [ ] Is the floor load rating documented for AI GPU racks?
- [ ] Does the "Rated 3" design allow for concurrent maintenance on all HT/LT gear?
- [ ] Are all cables labeled according to TIA-606 (Standard for Administration)?

---

## 7. References
### Standards
* **ANSI/TIA-942-C (2024):** Telecommunications Infrastructure Standard for Data Centers.
* **TIA-569:** Pathways and Spaces.
* **TIA-606:** Administration Standard for Infrastructure.

### Revision History
* 1.0: Mapped TIA-942 requirements for L&T Vyoma Mahape project.