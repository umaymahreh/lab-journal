# Week 4 — Electrical & Functional Testing

**Board:** Raspberry Pi Pico (RP2040)

## Day 1 — Pre-Power Checks
Continuity checks across supply rails (3V3–GND, VBUS–GND, 3V3–VBUS) on
the unpowered board, plus a reverse-polarity sanity check. Power-on done
through a current-limited bench supply; current settled to quiescent
draw within ~1–2 seconds — clean.

## Day 2 — In-Circuit Test Concepts
Compared how commercial ICT (bed-of-nails) and flying-probe testers work,
and how to approximate the same checks by hand with a DMM + test jig.

## Day 3 — Boundary Scan / Debug with OpenOCD
Connected to the RP2040 over SWD with a low-cost debug probe. Read back
MCU ID registers — matched expected RP2040 device ID.

```
openocd -f interface/cmsis-dap.cfg -f target/rp2040.cfg \
  -c "init; targets; rp2040.dap dpreg 0x0 0; exit"
```

## Day 4 — Building a Test Jig
Built a jig from a second (spare) Pico: drives known input patterns into
the board-under-test's GPIO pins and reads back outputs, removing manual
probing from the loop.

## Day 5 — Automated Functional Test Script
Wrote `functional_test.py` — runs a fixed test sequence, logs a
timestamped PASS/FAIL row per step, flushes after every write (survives
a mid-run power cut / load-shedding).

## Results
All 4 steps passed: GPIO2_HIGH, GPIO2_LOW, GPIO3_HIGH, ADC0_RANGE
(3.2996 V, within 3.28–3.32 range). MCU ID confirmed on Day 3.

## Deliverable
`functional_test.py` — reusable, unattended, restart-safe pass/fail logger.
