# Title: Annotated Bibliography - AI Data Centre Engineering Research
## Purpose: To curate and summarize the essential set of research papers, white papers, and technical brochures required to master AI-ready hyperscale electrical design.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #Research #WhitePapers #IEEE #CIGRE #NVIDIA #SchneiderElectric #LTVyoma
## Related Files: [[Design_Basis_Report.md]], [[NVIDIA_Architecture.md]], [[Power_Quality.md]]
## Standards Covered: IEEE 3000 Series, CIGRE TB 787, ASHRAE White Papers

---

## 1. Overview
As a Principal Consultant, I know that staying ahead in the 40 MW AI race requires moving beyond standard codes (IS/IEC). You must understand the "First Principles" found in cutting-edge research. This bibliography ranks the most influential documents currently shaping the design of NVIDIA-ready hyperscale facilities.

---

## 2. Top-Ranked Technical Papers (The "Must-Reads")

### Rank 1: NVIDIA White Paper
**Title:** *The Next Era of AI Infrastructure: Powering Blackwell and Beyond*  
**Authors:** NVIDIA Infrastructure Engineering Group  
**Year:** 2024  
**Why it Matters:** This is the definitive guide for the L&T Mahape project. It details the transition to the 120kW ORV3 rack, the 48V DC backplane logic, and the specific transient power characteristics of GPU clusters.  
**Key Insight:** AI loads are not static; they are highly dynamic, requiring specialized UPS response times.

### Rank 2: Schneider Electric White Paper #513
**Title:** *AI Impact on Data Center Design: Challenges and Opportunities*  
**Authors:** Victor Avelar, et al.  
**Year:** 2023  
**Publisher:** Schneider Electric Data Center Science Center  
**Why it Matters:** Provides the mathematical framework for how AI shifts the PUE and power density. It is the best resource for justifying the shift to liquid cooling electrical distribution to L&T management.  
**Key Insight:** AI requires a shift from "centralized cooling power" to "distributed cooling power" (CDUs).

### Rank 3: Uptime Institute Intelligence Report
**Title:** *The Impact of AI on Data Center Power Management*  
**Authors:** Uptime Institute Research  
**Year:** 2023  
**Why it Matters:** Focuses on the "Stability" of the grid. It analyzes how AI step-loads can trigger harmonic resonance in the facility's power train.  
**Key Insight:** Traditional N+1 redundancy might be insufficient for AI; "Block Redundant" architectures are becoming the preferred hyperscale standard.

### Rank 4: CIGRE Technical Brochure 787
**Title:** *Power Quality in Data Centres*  
**Publisher:** CIGRE (International Council on Large Electric Systems)  
**Year:** 2019  
**Why it Matters:** The most comprehensive global study on harmonics, voltage sags, and earthing in mission-critical facilities. Essential for the Mahape 33kV/11kV interface design.  
**Key Insight:** Harmonic interactions between parallel UPS systems can lead to "Silent Outages."

### Rank 5: IEEE 3000 Series (Modernized Color Books)
**Title:** *IEEE 3001.2: Recommended Practice for Load Analysis of Industrial and Commercial Power Systems*  
**Publisher:** IEEE Standards Association  
**Year:** 2022 (Active)  
**Why it Matters:** Replaces the old "Brown Book." It provides the standard calculations used in the ETAP/SKM models for the 40 MW facility.  
**Key Insight:** Modernizes the "Diversity Factor" for digital-first loads.

---

## 3. Specialized Domain Papers

### 3.1 On Thermal-Electrical Interdependency
**Title:** *ASHRAE TC 9.9 White Paper: Liquid Cooling Across the Industry*  
**Year:** 2023  
**Significance:** Defines the W1-W5 water classes. For Mahape, it dictates whether we can use free-cooling (economizers) or must rely on mechanical chillers, directly impacting the electrical BOQ.

### 3.2 On High-Density Protection
**Title:** *Selectivity in High-Availability Low Voltage Systems*  
**Publisher:** ABB Technical Paper  
**Year:** 2021  
**Significance:** Deep dive into "Zone Selective Interlocking" (ZSI) and how to coordinate 4000A ACBs with ultra-fast AI rack breakers.

### 3.3 On Grounding & Noise
**Title:** *IEEE Paper: Grounding Systems for High-Frequency Digital Facilities*  
**Authors:** Various  
**Year:** 2022  
**Significance:** Explains why the Signal Reference Grid (SRG) is mandatory for GPU-to-GPU InfiniBand communication to prevent packet loss.

---

## 4. How to Use this Bibliography for L&T Vyoma
1.  **Design Validation:** Use the CIGRE 787 findings to defend your "Active Harmonic Filter" sizing during client reviews.
2.  **Transients:** Use the NVIDIA Blackwell guide to set the "Short-time Delay" on your main breakers.
3.  **Efficiency:** Use Schneider WP #513 to calculate the PUE impact of liquid cooling pumps on the UPS bus.

---

## 5. Summary Table

| Importance | Source | Topic | Recommended Reader |
| :--- | :--- | :--- | :--- |
| **Critical** | NVIDIA | GPU Load Profiles | Design Engineer |
| **Critical** | Schneider | AI Infrastructure | Project Manager |
| **High** | IEEE | Protection/Stability | System Analyst |
| **High** | ASHRAE | Liquid Cooling | MEP Coordinator |
| **Medium** | CIGRE | Power Quality | O&M Team |

---

## 6. References
* **IEEE Xplore Digital Library:** [ieeexplore.ieee.org](https://ieeexplore.ieee.org)
* **CIGRE E-Cigre:** [e-cigre.org](https://e-cigre.org)
* **NVIDIA Partner Force:** [nvidia.com/en-us/about-nvidia/partners/](https://www.nvidia.com/en-us/about-nvidia/partners/)
* **Uptime Institute Portal:** [uptimeinstitute.com](https://uptimeinstitute.com)

---
**Next File Recommendation:** `43_Glossary/Terminology_Index.md` (Defining the high-level jargon used across the hyperscale and AI industry).