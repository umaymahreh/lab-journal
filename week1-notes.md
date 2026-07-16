
# Week 1 - Foundations, Safety & Bench Setup

## Day 1 - ESD Safety Basics

- Human body can build up 1000s of volts of static charge, often 
  unfelt below ~3000V
- Chips can be permanently damaged by as little as 10-100V discharge
- Damage can be instant, or a hidden defect causing failure weeks later
- Defense: wrist strap + grounded mat - touch mat before handling any board
- Habits: ground yourself first, store components in anti-static bags, 
  handle boards by edges, avoid synthetic clothing/carpet near bench

## Day 2 - Tool Install Checklist
- KiCad: installed ✅
- PulseView: installed ✅
- Python + libraries: installed ✅
- Git: installed ✅

## Day 3 - Datasheet: ATmega328P

- Absolute max ratings: Voltage on any pin: -0.5V to VCC+0.5V; 
  Max VCC: 6.0V; Operating temp: -40C to 85C
- Recommended operating: 1.8V-5.5V depending on speed grade; 
  our board runs it at 5V
- Pinout: 28-pin DIP/TQFP; includes VCC/GND, 23 general I/O pins 
  (digital 0-13, analog A0-A5 dual-purpose), RESET, XTAL1/XTAL2, AREF

## Day 3 - Datasheet: LD1117S50TR (Voltage Regulator)

- Absolute max ratings: Input voltage max 15V; Junction temp max 150C
- Recommended operating: Input 6.5V-15V typical, fixed 5V output, 
  up to 800mA output current
- Pinout: 3-pin SOT-223 package - VIN, GND, VOUT

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
### 1. Power Rails
- Barrel jack or USB -> Voltage Management (auto-selects source) -> 
  Voltage Regulator U1 (LD1117S50TR) -> regulated 5V rail
- 5V rail -> second regulator U3 (LP2985-33DBVR) -> regulated 3.3V rail
- Both rails feed the ATMEGA328P

### 2. Decoupling Capacitors
- ATMEGA328P: C14, C15 (0.1uF each) on VCC/AVCC pins
- Voltage Regulator stage: C1 (input), C2 + C3 (output)
- 3.3V regulator stage: C5 (1uF), C6 (2.2uF)

### 3. Communication Buses (pin mapping to headers)
- UART: RXD/TXD -> ARD_DIG0/ARD_DIG1 (header P4)
- SPI: SCK/MISO/MOSI/SS -> ARD_DIG13/12/11/10 (header P3)
- I2C: SDA/SCL -> ARD_AN4/ARD_AN5 (header P3)

## BOM Cross-Check (Day 4)

Verified these components against the schematic:
- U1 = LD1117S50TR (voltage regulator) - confirmed on Voltage Regulator sheet
- U5 = ATMEGA328P (main MCU) - confirmed on ATMEGA328P sheet
- C5, C10 = 1uF capacitors 
- R13 = 0 ohm resistor - confirmed as DTR-to-RESET series resistor

## Day 5 - Physical Mapping
Pending - hardware (Arduino board, multimeter) not yet arrived



## Week 1 - End of Week Deliverable

### Schematic-to-Board Summary
Traced the Arduino Uno R3's power rails (barrel jack/USB -> voltage 
management -> 5V regulator -> 3.3V regulator), decoupling capacitors 
on the ATMEGA328P, and all three communication buses (UART, SPI, I2C) 
mapped to physical header pins. Cross-checked key components against 
the BOM.

### Tool Install Checklist
- KiCad: installed and verified
- PulseView (sigrok): installed, demo device confirmed
- Python + numpy/pandas/matplotlib/scipy/pyserial: installed, verified
- Git: installed and verified
- GitHub repo created and connected, commits pushed successfully

### Outstanding
Physical board verification pending hardware delivery (Arduino Uno, 
multimeter ordered).