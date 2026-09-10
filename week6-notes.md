# Week 6 — Environmental Stress Screening (ESS) & Burn-In

**Board:** Arduino Uno (ATmega328P)

## Day 1 — Why Screening Works: The Bathtub Curve
High-but-falling failure rate early in life (infant mortality) → flat
useful-life period → rising failure rate at wear-out. Screening only
helps where infant mortality actually exists — stressing a defect-free
batch just burns useful life for nothing.

## Day 2 — Comparing Screening Methods
Static burn-in vs. temperature cycling vs. HASS/HALT. Cycling generally
finds solder-joint/interconnect defects faster than static burn-in for
the same total stress time (repeated expansion/contraction stresses
joints directly).

## Day 3 — Designing a Modest ESS Profile
25°C ↔ 55°C, ~1 hr ramp, 1 hr dwell each end, 3 cycles (~12 hrs total).
Kept comfortably inside rated limits. Monitored: 3V3 rail, 5V rail,
functional-test checkpoint each dwell. Ran off a UPS so load-shedding
couldn't interrupt the run.

## Day 4 — Running the Monitored Burn-In
Python script polled rails via SmuView + ran the Week 4 functional test
at each dwell, logging incrementally (append + flush, same pattern as
Week 4's script).

**Flag:** 3V3 rail dipped noticeably during the hot dwell of cycle 2,
self-recovered, no functional-test failure at that checkpoint.

## Day 5 — Reviewing the Log
No outright failure. One flagged rail transient — logged as "passed but
flagged for follow-up," not collapsed into a plain PASS. Scheduled for
a repeat burn-in cycle.

## Deliverable
One-page ESS profile doc + burn-in log (3 cycles, 6 functional-test
checkpoints, 1 flagged rail transient).
