# Title: BESS Peak Shaving & Demand Limiting Strategy
## Purpose: To optimize utility tariff structures and manage peak demand charges for a 40 MW load profile using Energy Storage.
## Revision: 1.0
## Date: 24-May-2024
## Tags: #BESS #PeakShaving #TariffOptimization #MSEDCL #LTVyoma
## Related Files: [[Battery_Energy_Storage.md]], [[AI_Load_Estimation.md]]

---

## 1. Overview
In Maharashtra (MSEDCL/Tata Power), industrial tariffs include heavy "Demand Charges" based on the highest 15-minute peak power draw in a billing cycle. For a 40 MW AI facility, unexpected training spikes can spike utility bills significantly. 

## 2. Peak Shaving Logic
*   **Threshold Setting:** The EPMS/SCADA monitors the incoming utility power in real-time against a predefined "Cap" (e.g., 38 MW).
*   **Discharge Trigger:** If AI cluster demand pushes total site load above 38 MW, the BESS (Battery Energy Storage System) automatically discharges to supply the delta (e.g., 2 MW), keeping the utility meter flat.
*   **Recharge Window:** The BESS recharges during low-tariff hours (typically off-peak night hours, 22:00 to 06:00).

---
## 📚 References
* **MERC (Maharashtra Electricity Regulatory Commission):** Commercial Tariff Guidelines.
