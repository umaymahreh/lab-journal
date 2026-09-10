# Week 7 — Data Analysis, SPC & Reliability

**Boards used across the program:** Arduino Uno R3 (Wk 1–2) →
Raspberry Pi Pico (Wk 3–4) → Arduino Uno (Wk 5–6)


## Day 1 — Aggregating the Dataset
Pulled every log from Weeks 1–6 into one dataset. Tagged which rows are
real hardware data vs. documented simulation (Week 2's log was partly
simulated — limited multimeter access that week) and which physical
board each row belongs to, since the reference board changed mid-program.

## Day 2 — Pass Rate & Pareto of Flagged Items
**Important reframe:** this is one board's history, not a batch of many
units — so "yield" here means % of test items passed, not % of boards
shipped clean.

- Week 1: no pass/fail testing (setup week)
- Week 2: 3 clean checks, 1 rail dip (auto-check missed it, graph caught it)
- Week 3: 12/12 checklist items clean, 4 cosmetic notes (accepted)
- Week 4: 4/4 functional steps passed

**Flagged-item Pareto (n=7):** cosmetic notes (4) > rail/monitoring
anomalies (2) > diagnosed fault (1).

## Day 3 — Process Stability
A real p-chart needs multiple units in batches — with one board, used a
simple run chart of flagged-items-per-session instead. No session had
more than 1 flagged item. Noted explicitly: real SPC needs multi-unit
data (input for Week 8).

## Day 4 — Weibull / Reliability
Worked a synthetic multi-unit example (β ≈ 0.7, decreasing hazard) since
the group's own board doesn't have enough real failure events yet to fit
its own curve.

## Day 5 — Synthesis
Two-part recommendation: (1) get more than one physical unit through the
protocol before SPC/Weibull are statistically meaningful, (2) both real
anomalies found so far only showed up via continuous monitoring, not
discrete testing — keep monitoring in whatever protocol comes out of
Week 8.

## Results Summary
- Total logged items (Wk 2–6): 27
- Clean pass rate: 25/27 (93%)
- Outright failures: 0
