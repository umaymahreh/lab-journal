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
## Day 3 - Oscilloscope Basics

Today's focus was the oscilloscope. Our team doesn't have physical access to one this week, so we covered it through theory, and used a Python script (numpy + matplotlib) to simulate what a clean vs noisy signal looks like on a scope screen.

We went over the three main scope concepts:
- **Timebase** - how much time each horizontal division on screen represents
- **Triggering** - how the scope decides when to start drawing the waveform so it looks stable instead of jumping around
- **Probing** - how the scope actually connects to a circuit, and how a bad probe connection can distort what you're seeing

To make this more concrete, we generated a simulated 1kHz square wave (0-5V) and compared it to the same wave with small random noise added on top (about ±0.2V). Seeing the two side by side made it much easier to understand what "noise on a line" actually looks like versus just hearing the term.

Looking at the two plots, the clean signal had sharp, even edges, while the noisy one had a slightly fuzzy, jagged look around the same edges - even though both were technically the "same" signal underneath.

We found triggering the hardest part to picture without an actual scope to try it on, but the concept made sense in theory - the scope needs a stable reference point (like a rising edge) to draw a steady picture instead of a flickering mess.

## Day 4 - Logging Data Automatically

Today's task was learning to log data automatically instead of manually taking readings one at a time. Since our team's hardware access was limited this week, we used a Python script to generate a simulated voltage log, representing what a real 5-minute logging session on a 5V rail would look like.

The script created 300 readings (one per second, so 5 minutes total), each with a small random wobble added to simulate natural ripple, plus a small dip near the end to simulate a minor real-world fault.

We opened the resulting CSV file in Excel just to sanity-check it - confirmed it had a timestamp column, a voltage column, and 300 rows that looked reasonable (values clustering around 5V).

This gave us a working example of what a logging tool's output actually looks like, which we'll replace with real SmuView-logged data once hardware access allows.

## Day 5 - Analyzing the Logged Data

Today we analyzed the CSV file from Day 4 using Python (pandas for the numbers, matplotlib for the chart).

**Results:**
- Expected (nominal) voltage: 5.0 V
- Measured average: 4.97 V
- Min / Max: 4.82 V / 5.03 V
- Ripple (max - min): 0.21 V

The average was very close to the expected 5V, which is a good sign overall. The ripple was a little higher than a perfectly clean rail would show, mainly because of a dip we noticed near the end of the log.

Interestingly, the script's automatic anomaly check (anything more than 5% off nominal) didn't flag this dip as a problem, but looking at the actual graph, there's a clear visible sag near the end. This taught us something useful: automated checks are helpful, but they can miss things that are obvious just by looking at the data visually - so both matter.

We saved the graph as `rail_plot.png`, showing voltage over the full 5-minute window with the dip clearly visible near the end.
