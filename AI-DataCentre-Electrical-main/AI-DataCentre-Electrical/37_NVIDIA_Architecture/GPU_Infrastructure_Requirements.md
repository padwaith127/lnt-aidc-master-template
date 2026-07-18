# Title: {{cookiecutter.ai_silicon_vendor}} GPU Infrastructure - Electrical Power Requirements
## Purpose: To define the specific electrical infrastructure, power profiles, and deployment requirements for {{cookiecutter.ai_silicon_vendor}} AI clusters.
## Project: {{cookiecutter.project_name}}
## Tags: #{{cookiecutter.ai_silicon_vendor}} #StepLoad #GPUInfrastructure #AI-Ready #HighDensity
## Standards Covered: OCP ORV3, IEEE 1100, IEC 62368-1

---

## 1. Overview
In the {{cookiecutter.project_name}}, the electrical design is purpose-built to host high-density {{cookiecutter.ai_silicon_vendor}} GPU infrastructure. Unlike standard CPU-based servers, AI clusters exhibit extreme power density and highly dynamic load profiles. This module provides the technical specs for the electrical engineer to ensure the infrastructure handles the thermal and electrical stress.

## 2. Power Step-Load & Transient Profiles
AI training is characterized by "Bursty" compute cycles.
1.  **Training Initialization:** Power jumps from 10% to 100% in < 50ms.
2.  **Checkpointing:** Sudden drop in power as data is written to disk.
3.  **Communication Phase:** Fluctuating power draw as GPUs exchange data via high-speed interconnects.

**Engineering Mandate:** 
The UPS and Generator systems for the {{cookiecutter.it_capacity_mw}} MW facility must handle a **di/dt of >100A per millisecond** at the rack level without the voltage dropping below the ITIC/CBEMA lower bound.

## 3. Engineering Calculations: TDP vs. Peak Power
### 3.1 Thermal Design Power (TDP)
TDP represents the continuous power draw. For modern {{cookiecutter.ai_silicon_vendor}} racks, this ranges from **60kW to 120kW+ per rack**.

### 3.2 Peak Power Requirement
Facility electrical circuits must be sized for the **Maximum Peak Power**, which includes the GPU, CPU, Networking, Fans, and internal Power Shelf losses.
*   **Design Overhead:** Add a strict 10% to 15% overhead to the total Rack TDP to size the branch circuit breaker. 
*   **Selection:** A 120kW rack requires a minimum 250A, 415V/480V 3-Phase feed via overhead busway.

## 4. The 48V DC Ecosystem (OCP Standard)
Next-generation {{cookiecutter.ai_silicon_vendor}} systems utilize the **Open Rack V3 (ORV3)** or similar power architectures.
*   **Input:** 3-Phase AC into centralized rack-mounted Power Shelves.
*   **Output:** 48V DC (to 54V DC) to the server backplane.
*   **Why?** To handle the 2,500+ Amperes required for 120kW compute without melting internal cables. It utilizes a massive vertical copper busbar.
*   **Grounding:** The DC return is referenced to the rack frame at a single point to prevent ground loops.

## 5. AI-Ready Networking Power (The "Third Network")
AI clusters require distinct networks, each with its own power impact:
1.  **Compute Fabric:** High-speed interconnects between GPUs. High power draw at the switch level.
2.  **Storage Fabric:** High-speed data feed.
3.  **Management Network:** Low speed operations.

**Strategy:** Ensure that "Networking Switch Racks" are not under-sized. A core fabric switch rack for a large cluster can draw **20kW to 30kW** on its own.

## 6. Construction & Deployment Execution
*   **Busway Tap-offs:** Use "Heavy Duty" tap-off boxes (250A/400A) with integrated energy metering.
*   **Fiber Protection:** AI clusters involve thousands of fibers. Ensure electrical power cable trays do NOT overlap or crush high-density fiber troughs. Maintain 600mm separation.
*   **Weight Management:** Ensure the structural concrete slab is reinforced for the **1.5 to 2.5 metric ton** weight of a fully populated liquid-cooled AI rack.

## 7. Commissioning & Readiness (IST)
1.  **Load Step Simulation:** Use specialized Load Banks that can trigger 0-100% steps to test the UPS and DG transient response.
2.  **Harmonic Audit:** Confirm that the {{cookiecutter.ai_silicon_vendor}} rectifiers are not creating resonance with the facility's power factor correction banks.
3.  **Redundancy Test:** Pull "Source A" and verify the power shelf handles the load on "Source B" without any GPU performance throttling.

## 8. Failure Modes
*   **Current Overloading:** During "Maximum Compute," a poorly balanced rack can trip one phase of a 3-phase input.
*   **Transient Voltage Swell:** When an AI job finishes, the sudden 100kW load drop can cause a voltage swell that damages sensitive management hardware.
*   **Thermal Trip:** Failure of the CDU liquid pump (electrical failure) leads to GPU shutdown in < 15 seconds.

## 9. Design Checklist
- [ ] Is the busway design capable of >120kW per rack?
- [ ] Does the UPS handle a 100% load step within 1 cycle?
- [ ] Is the Signal Reference Grid (SRG) connected to every {{cookiecutter.ai_silicon_vendor}} rack to protect high-speed networking?
- [ ] Are the AC input connectors (e.g., IEC 60309) specified with locking mechanisms?
