# Title: Glossary of AI & Hyperscale Electrical Engineering
## Purpose: To provide a standardized terminology reference for L&T engineers working on AI-ready hyperscale infrastructure.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #Glossary #Terminology #AI-Ready #DataCentreJargon #LTVyoma
## Related Files: [[Project_Overview.md]], [[NVIDIA_Architecture.md]], [[Uptime.md]]
## Standards Covered: IEEE 100, IEC 60050 (IEV), TIA-942-B, ASHRAE TC 9.9

---

## 1. Overview
In the 40 MW Mahape project, clear communication is essential. Hyperscale data centers sit at the intersection of Electrical Engineering, Mechanical Engineering, and Silicon Architecture. This glossary defines the essential terms you will encounter in design meetings with NVIDIA, Microsoft, and L&T stakeholders.

## 2. Electrical Power Systems (General)

*   **ATS (Automatic Transfer Switch):** A mechanical switch that transfers power between two sources (Utility and Generator) with a transition time of 20–50ms.
*   **STS (Static Transfer Switch):** A high-speed solid-state switch using Thyristors to transfer power between two synchronized AC sources in <4ms.
*   **VFI (Voltage and Frequency Independent):** A UPS topology where the output is independent of input voltage/frequency fluctuations (Double Conversion).
*   **Selectivity (Coordination):** The ability of a protection system to trip only the breaker closest to a fault.
*   **GPR (Ground Potential Rise):** The increase in voltage of the earth grid during a fault, critical for safety analysis in the HT Yard.

## 3. AI & High-Density Infrastructure

*   **Blackwell:** NVIDIA’s latest GPU architecture (e.g., GB200) designed for 120kW+ rack densities.
*   **TDP (Thermal Design Power):** The maximum amount of heat a GPU or server is expected to generate, used for sizing power and cooling.
*   **di/dt:** The rate of change of current over time. In AI, high *di/dt* during training bursts causes voltage transients.
*   **Power Shelf:** A centralized rack-mounted enclosure that houses multiple rectifiers (AC-to-DC) to feed a common DC busbar.
*   **ORV3 (Open Rack V3):** The Open Compute Project (OCP) standard for high-density racks, featuring a 48V DC busbar.
*   **NVLink:** NVIDIA’s high-speed GPU-to-GPU interconnect fabric, sensitive to high-frequency electrical noise.

## 4. Cooling & Mechanical Integration

*   **CDU (Coolant Distribution Unit):** A specialized heat exchanger that separates the facility chilled water (FWS) from the liquid coolant loop (TCS) feeding the GPUs.
*   **D2C (Direct-to-Chip):** A cooling method where cold plates are mounted directly on the GPU/CPU to remove heat via liquid flow.
*   **Secondary Loop:** The closed fluid circuit between the CDU and the IT racks.
*   **Approach Temperature:** The temperature difference between the primary fluid and the secondary fluid in a heat exchanger.
*   **PUE (Power Usage Effectiveness):** The ratio of total facility power to IT power. Target for AI-ready DCs is < 1.3.

## 5. Indian Regulatory & L&T Specifics

*   **CEIG (Chief Electrical Inspector to the Government):** The statutory authority responsible for inspecting and approving HT/LT installations in Maharashtra.
*   **CEA (Central Electricity Authority):** The Indian body that defines safety and connectivity regulations.
*   **White Space:** The area in the data center dedicated to IT equipment (Racks).
*   **Gray Space:** The infrastructure area (Electrical rooms, UPS rooms, AHU rooms).
*   **Point of Common Coupling (PCC):** The physical point where the L&T facility connects to the MSEDCL/Tata Power utility grid.

---

## 6. Acronym Quick-Reference Table

| Acronym | Full Form | Context |
| :--- | :--- | :--- |
| **BESS** | Battery Energy Storage System | UPS Backup (Lithium-ion). |
| **iMCC** | Intelligent Motor Control Centre | Pump/Chiller Control. |
| **BCMS** | Branch Circuit Monitoring System | PDU-level energy tracking. |
| **LSZH** | Low Smoke Zero Halogen | Cable Sheath type. |
| **GFC** | Good For Construction | Final approved drawings. |
| **EPMS** | Electrical Power Monitoring System | PQ and Energy Analytics. |
| **VESDA** | Very Early Smoke Detection Apparatus | Aspirating smoke detection. |

---

## 7. Failure Analysis Terminology

*   **Cascading Failure:** A failure in one component (e.g., a fan) leading to the failure of another (e.g., a UPS) through interdependency.
*   **Root Cause:** The fundamental reason for a failure, which, if addressed, prevents recurrence.
*   **MTBF (Mean Time Between Failures):** A statistical measure of reliability.
*   **Concurrent Maintainability:** The ability to perform maintenance on any part of the power train without interrupting the IT load (Uptime Tier III).

---

## 8. References
### Standards
* **IEC 60050:** International Electrotechnical Vocabulary (IEV).
* **IEEE 100:** The Authoritative Dictionary of IEEE Standards Terms.
* **TIA-942-B:** Infrastructure Standard for Data Centers.

### Revision History
* 1.0: Initial Glossary for L&T Vyoma Mahape project.

---
**Next File Recommendation:** `44_Reference_Index/Final_Repository_Map.md` (The master index that links every folder and file in this 46+ document knowledge base).