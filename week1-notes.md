# Week 1 - Foundations, Safety & Bench Setup

## Day 2 - Tool Install Checklist
- KiCad: installed ✅
- PulseView: installed ✅
- Python + libraries: installed ✅
- Git: installed ✅
- LibreOffice: installed ✅

## Day 4 - Schematic Reading (Attempt 1 - Shield template)
## File used
Arduino_Uno.kicad_pro (from KiCad/kicad-templates repo)
Note: this turned out to be a "shield" template - header-level 
pinout only, not full internal schematic.

## Power rails found
- P1 pin 1 = Vin (unregulated input)
- P1 pin 2 = +5V (regulated)
- (couldn't find which pin = 3.3V, need to check again)

## Reset
- P1 pin 5 = Reset

## Ground
- P2 and P4 both connect to GND at bottom of schematic

## Communication buses
- I2C: P3 pins 1,2 = A5(SCL), A4(SDA)
- SPI: P3 pins 5,6,7 = 13(SCK), 12(MISO), 11(MOSI)
- UART: P4 pins 7,8 = 1(Tx), 0(Rx)

## Limitation noted
This schematic didn't include the voltage regulator or 
decoupling capacitors - switching to rheingoldheavy's repo 
next to find those.
## Day 4 - Schematic Reading (Attempt 2 - Full board, rheingoldheavy repo)
[we'll fill this in later today]

## Day 5 - Physical Mapping
Pending - hardware (Arduino board, multimeter) not yet arrived# Day 4 - Schematic Reading

