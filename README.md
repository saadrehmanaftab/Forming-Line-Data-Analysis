# Forming line production data analysis

Self initiated study by Saad Ur Rehman, October 2026. **All inputs are assumed. No real production data is used.**
The script generates 4 weeks of shift records for 3 forming presses (180 shifts), then analyzes downtime, scrap,
OEE and a material balance, and writes an Excel report and two charts.

## Run

```
pip install numpy pandas matplotlib openpyxl
python forming_line_analysis.py
```

Outputs: `report.xlsx`, `downtime_pareto.png`, `weekly_oee.png`, `results.json`. The random seed is fixed (2026),
so a rerun reproduces the numbers on the CV.

## Result of the run (assumed data)

| Metric | Value |
|---|---|
| Shifts analyzed | 180 |
| Availability, performance, quality | 90.2%, 94.3%, 97.4% |
| OEE | 82.8% (weekly 83.1, 82.9, 82.7, 82.6) |
| Downtime | 140.7 hours, tool change 45.5%, material shortage 28.5%, maintenance 14.4%, quality hold 11.6% |
| Scrap rate | 2.62% of parts, flash 48.6%, short shot 31.2%, contamination 20.3% |
| Material balance | input 3289 kg, good 3091 kg, scrap 83 kg, runner and purge loss 115 kg, yield 94.0% |

## Assumptions (all placeholders)

- 480 planned minutes per shift, 3 shifts per day, 5 days per week, 4 weeks, 3 presses
- Ideal cycle 20 s with 16 cavities, actual cycle 6% slower on average (sd 3%)
- Downtime events per shift and duration: tool change 0.9 events, 22 min; material shortage 0.35, 35 min;
  maintenance 0.2, 45 min; quality hold 0.3, 18 min (normal durations, Poisson event counts)
- Mean scrap share of parts: flash 1.2%, short shot 0.8%, contamination 0.5%, lognormal shift to shift noise
- Part mass 0.9 g, runner and purge loss 3.5% of input material

## Limits

The data is synthetic, so the numbers show the method, not any real line. OEE is computed from shift totals
(availability times performance times quality). The study makes no claim about any employer or real process.
