# Week 3 — Visual & Incoming Inspection

**Board:** Raspberry Pi Pico (RP2040)

## Day 1 — Component Identification
Matched physical components against the BOM: resistor/cap colour codes,
3-digit EIA codes on SMD passives, package types (SOT-23, SOIC, LQFP)
cross-checked against KiCad's BOM at each reference designator.

## Day 2 — Solder-Joint Quality (IPC-A-610)
Reviewed what separates a good joint from a defective one — full wetting,
smooth concave fillet. Studied common failure modes to watch for:
cold joints, bridging, tombstoning, insufficient wetting.

## Day 3 — Built the Inspection Checklist
Reusable checklist across 5 categories: placement, orientation, solder,
cleanliness, mechanical fit. Built as a form so it can be reused on any
future board.

## Day 4 — Physical Inspection
Ran the checklist against the reference Pico under a phone macro lens,
section by section (USB connector, BOOTSEL, crystal, QSPI flash, RP2040
package, castellated pads, GPIO header).

**Result: passed every checklist item.**

## Day 5 — Counterfeit Awareness
Covered red flags for counterfeit/reclaimed parts: sanded/re-topped
markings, mismatched fonts/logos, re-tinned leads. Relevant given the
group sources spares from local grey-market channels.

## Defect Log
4 minor cosmetic notes only — dust near USB connector, handling residue
near GPIO header, slightly faded silkscreen near debug test points,
a cosmetic scratch on solder mask near the castellated pads. All
accepted, no rework required.

## Deliverable
Reusable incoming-inspection checklist + defect log for the reference Pico.
