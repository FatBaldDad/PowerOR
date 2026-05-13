# USB-C PD Chargers and Cables

This document covers USB-C PD chargers and cables as they relate to the PowerOR project.

The charger and cable should be treated as part of the power system, not as random accessories. A good PowerOR board cannot make up for a poor charger, poor cable, or unstable USB-C PD source.

PowerOR is being developed around the idea of using USB-C PD as an optional alternate power source for selected PS2 Slim builds while keeping the OEM PS2 power supply available.

---

## Why Chargers and Cables Matter

A USB-C PD power setup is not just the board inside the console.

The full power chain includes:

- USB-C PD charger
- USB-C cable
- USB-C PD trigger board
- Voltage conversion stage, if used
- Protection circuitry
- Power OR-ing circuitry
- Wiring
- PCB traces
- Console power input
- Internal mods powered by the console

A weak part anywhere in this chain can cause problems.

Possible problems include:

- Voltage drop
- Voltage sag under load
- Charger shutdown
- Failed PD negotiation
- Excessive heat
- Random console resets
- Controller instability
- Storage issues
- Audio or video issues

A console powering on does not prove the charger and cable are suitable.

---

## USB-C PD vs Normal USB Power

A normal USB connection usually starts at 5V.

The PS2 Slim target power range is much higher than normal 5V USB, so a basic USB charger is not enough.

USB-C PD allows the charger and connected device to negotiate higher voltage profiles, such as:

- 5V
- 9V
- 12V
- 15V
- 20V

For PowerOR, the charger must support the voltage profile required by the design.

If the design expects 9V, the charger must support 9V.

If the design uses 12V, 15V, or 20V with a buck converter, the charger must support that selected profile.

---

## USB-C PD Trigger Board Requirement

The charger does not automatically output 9V, 12V, 15V, or 20V just because a USB-C cable is plugged in.

A USB-C PD trigger board is needed to request the desired voltage from the charger.

For example:

- A 9V trigger board requests 9V from the charger.
- A 12V trigger board requests 12V from the charger.
- A 20V trigger board requests 20V from the charger.

The charger must support the requested profile, or the trigger board may fall back to another voltage, fail to negotiate, or not behave as expected.

The trigger board output should always be measured before connecting it to the console.

---

## Charger Voltage Profiles

When selecting a charger, do not only look at the total watt rating.

Look at the actual supported voltage and current profiles printed on the charger.

Example charger label:

<pre>
Output:
5V 3A
9V 3A
12V 3A
15V 3A
20V 3.25A
</pre>

This means the charger can provide different voltage/current combinations depending on what the connected device requests.

For PowerOR, the important part is whether the charger supports the voltage and current needed by the design.

---

## 9V Charger Target

One possible PowerOR target is 9V at up to 3A.

A charger that supports:

<pre>
9V 3A
</pre>

can theoretically provide up to:

<pre>
27W
</pre>

This may be useful for lighter PS2 Slim builds, but it should not be assumed safe or sufficient without testing.

A charger that only supports:

<pre>
9V 2A
</pre>

can only provide up to:

<pre>
18W
</pre>

That may not provide enough headroom for some builds.

For PowerOR, the charger should be selected based on the measured current draw of the console and installed mods.

---

## Higher Voltage Charger Option

Another possible approach is to request a higher USB-C PD voltage, then use a buck converter to step the voltage down.

Examples:

- 12V input stepped down to the console voltage
- 15V input stepped down to the console voltage
- 20V input stepped down to the console voltage

This can be useful because higher voltage means lower current on the USB-C input side for the same amount of power.

However, this adds more design complexity.

A higher-voltage design requires careful attention to:

- Buck converter current rating
- Converter efficiency
- Heat
- Ripple
- Load transients
- PCB layout
- Inductor selection
- Capacitor selection
- Protection circuitry
- Output voltage accuracy

This approach may be better for higher-power designs, but it should not be used casually.

---

## Charger Wattage Can Be Misleading

A charger advertised as “65W” or “100W” does not mean it can provide any voltage/current combination you want.

For example, a charger may be rated 65W because it can provide:

<pre>
20V 3.25A
</pre>

But that same charger may only provide:

<pre>
9V 2A
</pre>

or:

<pre>
9V 3A
</pre>

The total wattage is not enough information.

Always check the supported PD profiles.

---

## Multi-Port Chargers

Multi-port USB-C chargers can be convenient, but they can also complicate testing.

Some chargers reduce available power when more than one port is used.

For example, a charger may provide full power on one port when used alone, but reduce output when another USB-C or USB-A device is plugged in.

Possible issues with multi-port chargers:

- Power is shared between ports.
- PD negotiation may restart when another device is plugged in.
- Output voltage may drop or renegotiate.
- The console may reset if the charger changes modes.
- The labeled maximum output may only apply when one port is used.

For PowerOR testing, use one charger port at a time unless multi-port behavior is specifically being tested.

---

## Power Banks

Some USB-C PD power banks may support the required voltage profile, but they should be tested carefully.

Possible issues with power banks:

- Auto-shutoff at low load
- Limited current at 9V
- Voltage drop as the battery discharges
- Heat during high load
- PD renegotiation
- Shorter runtime than expected
- Output behavior changing between ports

A power bank should not be assumed safe just because it supports USB-C PD.

It should be tested the same way as a wall charger.

---

## Avoid USB-A to USB-C Power Paths

A USB-A to USB-C cable is not the same as a USB-C to USB-C PD setup.

USB-A does not provide normal USB-C PD negotiation in the same way.

For PowerOR, the intended setup should use:

<pre>
USB-C PD charger -> USB-C to USB-C cable -> USB-C PD trigger/input board
</pre>

Avoid trying to power the project from random USB-A chargers, USB-A ports, or USB-A to USB-C cables unless that behavior is being intentionally tested for a separate reason.

---

## Cable Requirements

The USB-C cable matters.

A poor cable can cause voltage drop, heat, or unstable behavior.

Cable concerns include:

- Current rating
- Wire gauge
- Cable length
- Connector quality
- E-marker support
- Heat under load
- Voltage drop under load
- Mechanical strain

A cable should be selected intentionally for the expected current.

---

## 3A vs 5A Cables

Many USB-C cables are rated for up to 3A.

For current above 3A, a proper 5A cable is normally required.

A 5A cable should be electronically marked, often called an e-marked cable.

For a basic 9V 3A target, a good 3A-rated USB-C to USB-C cable may be enough for testing.

For higher-power designs, especially anything involving 20V at higher current, cable rating becomes more important.

Do not assume all USB-C cables are equal.

---

## Cable Length

Shorter cables are usually better for power delivery.

Long cables can create more voltage drop, especially at higher current.

For testing, use a short, good-quality USB-C to USB-C cable.

Avoid:

- Very long cables
- Unknown cheap cables
- Damaged cables
- Thin flexible charging-only cables with unknown ratings
- Loose connectors

If a setup works with one cable but not another, the cable may be part of the problem.

---

## Connector Quality

The USB-C connector is also part of the power path.

Poor connector contact can cause:

- Intermittent power
- Heat
- Voltage drop
- Failed negotiation
- Charger reset
- Console reset

For an internal kit, the USB-C port needs to be mechanically supported so the solder joints are not taking all the stress.

A strong mechanical mount is just as important as the electrical design.

---

## Recommended Charger Direction

For early PowerOR testing, a good starting point would be a known-quality USB-C PD charger that supports at least:

<pre>
9V 3A
</pre>

This gives a useful test target for lighter PS2 Slim builds.

For future higher-power testing, a charger that supports stronger profiles may be useful, such as:

<pre>
15V 3A
20V 3A
20V 5A
</pre>

However, higher voltage should only be used if the PowerOR board includes the proper voltage conversion and protection design.

Never connect a higher-voltage PD output directly to the console.

---

## Recommended Cable Direction

For early PowerOR testing, use:

- USB-C to USB-C cable
- Short length
- Known brand or known rating
- Rated for at least 3A
- Firm connector fit
- No visible damage
- No unknown adapters in the path

For higher-power testing, use:

- Proper 5A-rated USB-C cable
- E-marked cable
- Short length where possible
- Tested under load

---

## Charger Testing Checklist

Before using a charger with PowerOR, test and document it.

Suggested charger test table:

| Test | Result | Notes |
|---|---|---|
| Charger brand/model | TBD |  |
| Rated wattage | TBD |  |
| Supports 9V | TBD |  |
| 9V current rating | TBD |  |
| Supports 12V | TBD |  |
| Supports 15V | TBD |  |
| Supports 20V | TBD |  |
| Single-port behavior tested | TBD |  |
| Multi-port behavior tested | TBD |  |
| No-load output measured | TBD |  |
| Loaded output measured | TBD |  |
| Heat checked | TBD |  |
| Stable during startup | TBD |  |
| Stable during long runtime | TBD |  |

---

## Cable Testing Checklist

Before using a cable with PowerOR, test and document it.

Suggested cable test table:

| Test | Result | Notes |
|---|---|---|
| Cable brand/model | TBD |  |
| Cable length | TBD |  |
| Rated current | TBD |  |
| E-marked | TBD |  |
| Connector fit | TBD |  |
| Voltage drop under load | TBD |  |
| Heat under load | TBD |  |
| Stable during startup | TBD |  |
| Stable during long runtime | TBD |  |

---

## Measuring Voltage Drop

Voltage should be measured at more than one point.

Useful measurement points include:

- Charger output, if accessible
- Trigger board output
- PowerOR input
- PowerOR output
- Console power input
- Console internal voltage rails, if appropriate

The most important measurement is the voltage that actually reaches the console input.

A setup may look good at the trigger board but still lose voltage through the cable, wiring, protection circuitry, or OR-ing stage.

---

## Testing Under Real Load

A charger and cable should be tested under load.

No-load voltage does not tell the whole story.

Testing should include:

- No-load voltage
- Dummy-load voltage
- Console startup
- Console idle
- Gameplay
- Long runtime
- Source switching
- Heat after extended operation

The goal is to confirm that the charger and cable remain stable when the system is actually being used.

---

## Warning About Cheap Chargers

Cheap chargers may not behave consistently.

Possible issues include:

- Poor voltage regulation
- Excessive ripple
- Overstated ratings
- Heat
- Poor protection
- Bad USB-C PD negotiation
- Shutdown under load
- Inconsistent behavior between units

For PowerOR, use a charger that is worth trusting with a console.

A cheap charger can make a good board look bad, or worse, damage the console.

---

## Warning About Adapters

Avoid stacking adapters in the power path.

Examples to avoid:

- USB-A to USB-C adapters
- Barrel jack adapters
- Magnetic USB-C adapters
- Unknown extension cables
- Loose right-angle adapters
- Unrated USB-C couplers

Every adapter adds another possible point of voltage drop, heat, or intermittent contact.

For testing, keep the power path simple and repeatable.

---

## Documentation Goal

Each charger and cable used for testing should be documented.

This helps separate board problems from power-source problems.

For example, if a console resets during testing, the issue could be:

- The charger
- The cable
- The trigger board
- The PowerOR board
- The wiring
- The console
- An internal mod
- A combination of several things

Good documentation makes troubleshooting easier.

---

## Practical Starting Recommendation

For early PowerOR testing:

- Use a known-quality USB-C PD wall charger.
- Confirm it supports 9V at 3A.
- Use a short USB-C to USB-C cable rated for at least 3A.
- Measure the trigger board output before connecting anything to the console.
- Test with a dummy load before testing with a PS2.
- Test voltage at the console input, not only at the USB-C board.
- Check for heat during extended testing.
- Avoid heavily modified consoles during early testing.

---

## Project Position

The charger and cable are not afterthoughts.

They are part of the PowerOR power system.

A safe design requires:

- A suitable charger
- A suitable cable
- A tested trigger board
- Proper voltage conversion, if needed
- Proper protection
- Proper wiring
- Proper power OR-ing
- Real load testing

Until the charger and cable are tested with the full system, the setup should be treated as experimental.

---

## Disclaimer

This document is part of an experimental hardware project.

Incorrect charger selection, poor cable quality, voltage drop, unstable USB-C PD negotiation, insufficient current, or excessive ripple can cause console instability or damage.

Use this information at your own risk.
