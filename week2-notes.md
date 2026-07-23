# Week 2

## Day 1 - Multimeter Basics

Today we started working with a multimeter. Since our internship is remote, one of our team members had a DMM on hand, so they took the actual readings while the rest of us joined on a call to watch and understand what was happening.

### What we measured

**Voltage**
We measured the voltage on the 5V rail of an Arduino Uno.
- Reading we got: 4.98 V
- Expected value: 5.00 V
- Difference: 0.02 V

We talked about why there's a small difference — things like tolerance in the onboard voltage regulator, or the meter itself not being 100% perfect.

**Current**
We also measured the current draw of the Arduino board while idle (no extra components connected).
- Reading we got: 45 mA

**Continuity**
We used the continuity mode to check a jumper wire. The meter beeped, which told us the connection was good.
- Result: Pass

### Understanding accuracy

We looked at the multimeter's datasheet to check its accuracy rating. It said something like ±(0.5% + 2 digits). We understood this to mean that even a "correct" reading can be slightly off, and that's normal — it's not a mistake on our part, it's just a limit of the tool. For a 5V reading, that works out to roughly ±0.045 V of expected error, so our 0.02 V difference is well within that range.

### What we found tricky

At first we weren't fully sure which mode to use for continuity versus resistance, since both use the same probes and look similar on the dial. We figured out that continuity mode is the one with the sound-wave/diode-like symbol, and it's meant for quick checks rather than getting an exact resistance value.

### Takeaway

Overall, we got a better sense of how to use a multimeter properly, what its limits are, and how to read its results without over-trusting the exact number.
## Day 2 - Power Supply Basics

Today we moved on to using a bench power supply. The idea was to learn how to power up a board safely, especially using a current limit so nothing gets damaged if there's a short or a wiring mistake.

### Setting up the supply

We set the bench power supply to output 5V, since that's what our board (Arduino Uno) needs.

Before connecting anything, we set a current limit on the supply. We picked 200 mA as a safe limit, since the board normally draws around 45-70 mA, so this gives enough headroom for normal operation but still protects against a short circuit.

### Powering up

- Voltage set: 5.00 V
- Current limit set: 200 mA
- Actual current drawn once powered on: 47 mA
- Board powered on normally: Yes (power LED lit up, board responded as expected)

We also talked about what would happen if there was a short somewhere on the board. In that case, the supply would "trip" - meaning it would stop supplying more current once it hit the 200 mA limit, and the voltage would drop instead of the current spiking. This is what protects the board from getting damaged.

### Why current limiting matters

We understood that this step is really important the first time you power up any new or unfamiliar board. Without a current limit, a wiring mistake or short could pull way more current than the board can handle, and it could burn out a component or trace before anyone even notices.

### What we found tricky

It took us a moment to understand the difference between the voltage the supply is "set to" versus what it actually "outputs" once current limiting kicks in. We realized that in constant current mode, the supply will drop the voltage to keep current at the limit, instead of keeping voltage fixed.

### Takeaway

We learned that powering up a new board isn't just about setting the right voltage - setting a safe current limit first is just as important, since it's what actually protects the hardware.
