# Title: BESS Peak Shaving & Demand Limiting Strategy
## Purpose: To optimize {{cookiecutter.utility_provider}} tariff structures and manage peak demand charges for a {{cookiecutter.it_capacity_mw}} MW load profile using Energy Storage.
## Tags: #BESS #PeakShaving #TariffOptimization #{{cookiecutter.utility_provider}} #EnergyArbitrage

---

## 1. Overview
In {{cookiecutter.state}}, industrial tariffs from {{cookiecutter.utility_provider}} include heavy "Demand Charges" based on the highest 15-minute peak power draw in a billing cycle. For a {{cookiecutter.it_capacity_mw}} MW facility supporting {{cookiecutter.ai_silicon_vendor}} workloads, unexpected training bursts can push the facility past its contracted MVA limit, resulting in massive financial penalties. 

By integrating a Lithium-ion Battery Energy Storage System (BESS) with the facility's SCADA, we can utilize **Peak Shaving** and **Energy Arbitrage**.

## 2. Peak Shaving Logic & Control
The strategy relies on a rapid-response feedback loop between the Main Incoming Meters and the BESS Inverters.

*   **Threshold Setting (The Cap):** The EPMS/SCADA is programmed with a hard utility limit (e.g., setting a cap at 95% of the sanctioned MVA).
*   **Discharge Trigger:** If an AI cluster initiates a massive training run and the total site load approaches the Cap, the BESS automatically switches from "Standby" to "Discharge" mode. It supplies the delta power (e.g., injecting 2 MW into the internal grid), ensuring the {{cookiecutter.utility_provider}} meter never sees the spike.
*   **Recharge Window (Arbitrage):** The BESS recharges exclusively during low-tariff (off-peak) hours in {{cookiecutter.state}}—typically late night. This allows the facility to buy power when it is cheapest and "spend" it internally when demand charges are highest.

## 3. Engineering Calculations & Impact

### 3.1 C-Rate and Thermal Management
Peak shaving requires the BESS to discharge at varying rates, which generates significant heat.
*   Unlike UPS backup (which discharges at 4C to 6C for 5 minutes), Peak Shaving may require a **0.5C to 1C discharge over 1 to 2 hours**.
*   **HVAC Impact:** The HVAC system in the BESS room must be sized to handle the continuous heat rejection of prolonged discharging, not just emergency standby.

### 3.2 Battery Degradation Factor
*   Using UPS batteries for daily peak shaving will rapidly consume the cycle life of the cells (e.g., utilizing 300 cycles per year).
*   **Solution:** Specify **LFP (Lithium Iron Phosphate)** chemistry, which offers 3000 to 5000 cycles, and oversize the Ah capacity by 20% to account for depth-of-discharge (DoD) degradation over a 10-year lifespan.

## 4. Integration with Emergency Operations
**Rule of Supremacy:** Emergency Backup *always* overrides Peak Shaving.
*   If the SCADA detects a utility failure from {{cookiecutter.utility_provider}} while the BESS is peak-shaving, the control logic immediately aborts the shaving routine, reserves the remaining battery State of Charge (SOC), and shifts to supporting the critical IT load while the Diesel Generators synchronize.
*   **SOC Minimum:** The system is hard-coded to never discharge below a specific SOC (e.g., 40%) during peak shaving, ensuring there is always enough runtime to bridge a utility blackout.

## 5. Design Checklist
- [ ] Has the local {{cookiecutter.utility_provider}} tariff structure been analyzed for Time-of-Use (TOU) rates?
- [ ] Is the BESS inverter capable of bidirectional, grid-interactive operation?
- [ ] Is the LFP battery cycle-life warranty rated for daily cycling?
- [ ] Has the SCADA "Emergency Override" logic been verified?
