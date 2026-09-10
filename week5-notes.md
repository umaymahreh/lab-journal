# Week 5 — Signal Integrity & Protocol Analysis

**Board:** Arduino Uno (ATmega328P)

## Day 1 — Logic-Analyser Fundamentals
Sample rate vs. signal rate, the Nyquist trap. Set fx2lafw sample rate
to 4–5× the fastest expected edge rate, not just 2×. Verified channel
thresholds against the Uno's 5V logic levels before probing a real bus.

## Day 2 — Capturing and Decoding UART
Probed TX/RX (pins 1/0) during boot. Stacked the UART decoder in
PulseView, swept baud rate in small steps to confirm true baud
(*115200 8N1 — placeholder, confirm against your own capture*).

## Day 3 — Decoding I²C and SPI
I²C on A4/A5 (Wire lib), SPI on pins 10–13. Stacked decoders to resolve
start/address/ACK/data. Address-scanned the bus and cross-checked
against the datasheet (*0x76 — placeholder address, confirm your sensor*).

## Day 4 — Signal Quality
Compared a clean I²C bus (correct pull-up) against one with a weakened
pull-up on the scope — slower rise time, lower effective high level.
Also looked at ringing on an unterminated SPI clock line.

## Day 5 — Fault Diagnosis Exercise
Blind test: one member introduced a fault (missing I²C pull-up) without
telling the others. Found it from the decode (repeated NACKs) + the
analog trace underneath (SDA not reaching a valid high). Traced back to
the schematic before fixing.

## Deliverable
Annotated capture + decode for one bus, signal-quality comparison, one
diagnosed fault — per planner, pick **one** bus to go deep on rather than
covering all three shallowly.
