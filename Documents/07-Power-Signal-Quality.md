# Power Signal Quality

This document covers power signal quality for the PowerOR project.

For a PlayStation 2 Slim, voltage level alone is not enough. The power must also be stable, clean, and able to handle changes in load without causing the console to reset, glitch, or become unreliable.

A power source that measures close to the correct voltage with a multimeter may still have problems that only show up during startup, gameplay, source switching, or oscilloscope testing.

---

## Why Power Signal Quality Matters

The PS2 needs stable DC power.

A USB-C PD power setup may look good at first because the voltage appears correct, but the console may still have problems if the power signal has:

- Voltage sag
- Startup dips
- Overshoot
- Ripple
- Switching noise
- Poor transient response
- Intermittent dropouts
- Ground instability
- Excessive voltage drop through wiring

PowerOR needs to be tested for power quality, not just basic voltage.

---

## Voltage Is Only Part of the Story

A common mistake is checking the output with a multimeter, seeing a number close to the expected voltage, and assuming the power system is safe.

That is not enough.

A multimeter is useful for checking average voltage, but it may not show fast problems such as:

- Short voltage dips
- Startup spikes
- Ripple
- Switching noise
- Fast load transient events
- Brief disconnects during source switching

For PowerOR, both multimeter testing and oscilloscope testing are useful.

---

## Important Power Quality Questions

PowerOR testing should answer questions such as:

- What does the USB-C PD output look like at startup?
- How long does PD negotiation take?
- Does the voltage ramp smoothly?
- Does the voltage overshoot?
- Does the voltage dip when the console turns on?
- Does the voltage sag during gameplay?
- Does the voltage stay stable during source switching?
- Is ripple within a reasonable range?
- Does the charger shut down or renegotiate?
- Does the board get hot under load?
- Does the console behave normally over time?

These questions are more important than simply asking whether the console powers on.

---

## No-Load Voltage

No-load voltage is the voltage measured when the power source is active but not powering the console or a dummy load.

This is the first basic check.

For example:

```text
USB-C PD trigger board connected to charger
No console connected
Measure output voltage
