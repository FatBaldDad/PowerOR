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

<pre>
USB-C PD trigger board connected to charger
No console connected
Measure output voltage
</pre>

This confirms that the trigger board is requesting the expected voltage.

However, no-load voltage does not prove the setup can power a PS2.

A board can show the correct voltage with no load and still fail under real load.

---

## Loaded Voltage

Loaded voltage is the voltage measured while the power system is supplying current.

This is much more important than no-load voltage.

Loaded voltage should be checked during:

- Dummy-load testing
- Console startup
- Console idle
- Gameplay
- Internal mod operation
- Source switching
- Long runtime testing

The voltage should be measured as close to the console input as practical.

Measuring only at the trigger board output may hide voltage drop through the rest of the power path.

---

## Voltage Sag

Voltage sag happens when the voltage drops under load.

This can happen if the charger, cable, trigger board, converter, wiring, or PowerOR board cannot provide enough current or respond quickly enough to load changes.

Voltage sag can cause:

- Failed boot
- Random resets
- Controller instability
- Storage instability
- Audio or video issues
- USB-C charger shutdown
- Unreliable behavior
- Heat in weak parts of the power path

For PowerOR, voltage sag must be tested under realistic load.

---

## Startup Dips

Startup is one of the most important times to test.

When the console first powers on, the load can change quickly. Internal capacitors charge, regulators start up, and installed mods may begin drawing current.

If the power system dips too low during startup, the console may:

- Fail to boot
- Reset repeatedly
- Start inconsistently
- Cause internal mods to behave strangely
- Trigger charger protection
- Cause USB-C PD renegotiation

A startup dip may be too fast to see clearly with a multimeter.

An oscilloscope is the better tool for checking startup behavior.

---

## Overshoot

Overshoot happens when the voltage briefly rises above the intended level.

Overshoot may occur during:

- Charger startup
- PD negotiation
- Buck converter startup
- Source switching
- Load removal
- Plugging or unplugging power sources

Overshoot is dangerous because even a short high-voltage spike may stress or damage components.

PowerOR testing should check for overshoot at the output of the USB-C PD stage, the PowerOR board output, and the console input.

---

## Ripple

Ripple is the repeating AC variation that rides on top of the DC output voltage.

Some ripple is normal with switching power supplies and buck converters, but too much ripple can cause problems.

Ripple may come from:

- USB-C charger switching circuitry
- USB-C PD trigger board layout
- Buck converter output
- Poor capacitor selection
- Poor capacitor placement
- Long wires
- Poor grounding
- High load current
- Poor PCB layout

Possible symptoms of excessive ripple include:

- Audio noise
- Video instability
- Controller issues
- Storage issues
- Random crashes
- General unreliable behavior

Ripple should be checked with an oscilloscope.

---

## Switching Noise

Switching noise is high-frequency noise caused by switching regulators, chargers, buck converters, and fast current changes.

Switching noise can be harder to diagnose than simple voltage sag.

It may affect sensitive parts of the system, especially if wiring and grounding are poor.

Possible sources include:

- USB-C PD charger
- Buck converter
- Internal console regulators
- Long power wires
- Poor ground routing
- Poor capacitor layout
- Nearby digital circuits

PowerOR should be designed and tested with noise in mind.

---

## Load Transients

A load transient is a sudden change in current demand.

For example, the console may suddenly draw more current during startup, gameplay, storage access, wireless activity, or when internal mods become active.

The power system must respond without the voltage dipping too far or overshooting.

Load transient testing helps show whether the power system has enough margin and output capacitance.

---

## Ground Stability

The ground path is just as important as the positive voltage path.

A weak or noisy ground can create strange problems even if the positive voltage appears correct.

Ground problems may cause:

- Controller instability
- Audio noise
- Video noise
- Random resets
- Communication issues between internal mods
- Incorrect voltage readings
- Unstable behavior during load changes

PowerOR wiring should use a strong ground return and avoid long, thin, or poorly connected ground paths.

---

## Voltage Drop Through the Power Path

Voltage should be measured at multiple points.

Possible measurement points:

- USB-C PD trigger board output
- PowerOR USB-C input
- PowerOR output
- OEM PSU input
- Console power input
- Internal console voltage rails, if appropriate

Voltage drop can happen across:

- USB-C cable
- USB-C connector
- Trigger board
- Protection circuitry
- Power OR-ing components
- Wires
- PCB traces
- Connectors
- Solder joints

The most important voltage is the voltage that actually reaches the console.

---

## PD Negotiation Behavior

USB-C PD negotiation is not instant.

The charger and trigger board need time to communicate and agree on a voltage profile.

Important things to test:

- Does the trigger board start at 5V before requesting 9V?
- How long does it take to reach the requested voltage?
- Does the voltage briefly jump or dip?
- Does the charger ever renegotiate?
- Does the charger shut down under load?
- Does the trigger board recover properly after unplugging and reconnecting?
- Does behavior change with different chargers or cables?

The PD negotiation behavior needs to be understood before the output is trusted.

---

## Charger Behavior Under Load

Different USB-C PD chargers may behave differently.

A charger may work fine with one load but fail with another.

Possible charger behaviors include:

- Stable output
- Voltage sag
- Shutdown under load
- Renegotiation
- Cycling on and off
- Heat buildup
- Current limiting
- Different behavior on different ports

This is why testing should be done with the actual charger and cable intended for use.

---

## Source Switching Behavior

PowerOR is a power OR-ing project, so source switching is a major part of the design.

Testing should include:

- OEM PSU only
- USB-C PD only
- Both connected
- Plugging in OEM PSU while USB-C PD is active
- Removing OEM PSU while USB-C PD is active
- Plugging in USB-C PD while OEM PSU is active
- Removing USB-C PD while OEM PSU is active

During these tests, check for:

- Voltage dips
- Voltage spikes
- Backfeeding
- Console resets
- Charger shutdown
- Heat
- Strange behavior from internal mods

The power transition should be predictable and safe.

---

## Multimeter Testing

A multimeter is useful for basic checks.

Use a multimeter to check:

- No-load voltage
- Loaded voltage
- Voltage at the console input
- Voltage drop across wiring
- Current draw, if your meter setup supports it safely
- Continuity
- Shorts before powering on

A multimeter is the first tool to use, but it does not show everything.

Fast dips, ripple, and noise need an oscilloscope.

---

## Oscilloscope Testing

An oscilloscope is the best tool for checking power quality.

Use an oscilloscope to check:

- Startup ramp
- Voltage dips
- Overshoot
- Ripple
- Switching noise
- Load transient response
- Source switching behavior
- USB-C PD negotiation behavior

Oscilloscope captures should be saved and documented in the project.

Suggested folder:

<pre>
Testing/Oscilloscope-Captures/
</pre>

---

## Dummy Load Testing

Before connecting PowerOR to a console, the board should be tested with a dummy load.

Dummy-load testing helps reduce the risk of damaging a console during early testing.

Suggested dummy-load tests:

- Light load
- 1A load
- 2A load
- 3A load
- Extended runtime load
- Thermal testing under load
- Voltage drop measurement
- Ripple measurement

The dummy load should be appropriate for the expected voltage and current.

---

## Console Runtime Testing

After dummy-load testing, console runtime testing can begin.

Runtime testing should include:

- Cold startup
- Repeated startup cycles
- Idle at main menu
- Gameplay
- Memory card access
- Controller use
- Internal mod activity
- Long play session
- Power source switching, if safe to test
- Heat checks after extended use

A short successful boot is not enough.

The console should be tested over time.

---

## Heat and Power Quality

Heat can make power problems worse.

As parts heat up, voltage regulation and current capacity may change.

Parts to check for heat:

- USB-C charger
- USB-C cable ends
- USB-C port
- Trigger board
- Buck converter
- OR-ing components
- Wires
- PCB traces
- Connectors
- Console power input area

Thermal testing should be done during real load, not only at idle.

---

## Suggested Power Quality Test Table

| Test | Status | Notes |
|---|---|---|
| No-load voltage measured | Not started |  |
| Loaded voltage measured | Not started |  |
| Voltage measured at console input | Not started |  |
| Startup dip checked | Not started |  |
| Overshoot checked | Not started |  |
| Ripple checked | Not started |  |
| Switching noise checked | Not started |  |
| Dummy-load test completed | Not started |  |
| Console startup test completed | Not started |  |
| Long runtime test completed | Not started |  |
| OEM PSU only tested | Not started |  |
| USB-C PD only tested | Not started |  |
| Both sources connected tested | Not started |  |
| Switchover behavior tested | Not started |  |
| Heat checked under load | Not started |  |

---

## Suggested Measurement Notes Table

| Measurement Point | No Load | Loaded | Notes |
|---|---:|---:|---|
| USB-C trigger output | TBD | TBD |  |
| PowerOR USB-C input | TBD | TBD |  |
| PowerOR output | TBD | TBD |  |
| Console input | TBD | TBD |  |
| Internal rail, if measured | TBD | TBD |  |

---

## Practical Testing Rule

For PowerOR, the practical rule is:

Do not trust the power system until it has been tested under load.

The design should be checked for:

- Correct voltage
- Stable voltage
- Enough current
- Low enough ripple
- Acceptable heat
- Safe switching behavior
- No backfeeding
- Reliable console operation

A power system that only passes a no-load voltage test is not proven.

---

## Project Position

Power signal quality is one of the main reasons PowerOR is being developed carefully.

The goal is not just to power on a PS2 with USB-C PD.

The goal is to understand whether USB-C PD can provide stable, safe, and reliable power for selected PS2 Slim builds when used with proper protection, wiring, testing, and source selection.

Until power quality has been measured and documented, the project should remain experimental.

---

## Disclaimer

This document is part of an experimental hardware project.

Incorrect voltage, voltage sag, ripple, overshoot, poor grounding, poor wiring, or unsafe source switching can damage a PlayStation 2 console.

Use this information at your own risk.
