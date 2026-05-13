# USB-C PD Controversy and Risks

USB-C PD power mods for the PlayStation 2 are a controversial topic in the PS2 modding community.

Some people like the idea because USB-C PD is modern, compact, and convenient. Others are cautious because there have been concerns, failures, and reports of consoles being damaged by poor USB-C power implementations.

This document exists to address those concerns directly.

PowerOR is not being developed as a quick connector swap. It is being developed as an experimental power project that needs proper testing before it should be trusted in a console.

---

## Why USB-C PD for the PS2 Is Controversial

The PlayStation 2 was not designed around USB-C PD.

Adding USB-C power means changing how the console receives power, and that can create risk if the design is not handled carefully.

Common concerns include:

- Wrong voltage being supplied to the console
- Insufficient current available from the charger or trigger board
- Cheap or unreliable USB-C PD trigger boards
- Poor-quality USB-C cables
- Voltage sag under load
- Startup dips
- Ripple and noise
- Heat from DC-DC converters
- Underrated wiring
- Poor grounding
- Backfeeding between power sources
- Lack of proper protection circuitry
- Assuming a console is safe just because it powers on

A PS2 powering on does not prove the power system is safe.

---

## Powering On Is Not Enough

One of the biggest mistakes with power mods is assuming that if the console turns on, the design is good.

That is not enough.

A bad power design may still allow the console to boot, but cause problems later, such as:

- Random resets
- Controller issues
- Audio or video instability
- Storage corruption
- Excessive heat
- Unstable operation after long play sessions
- Damage to the console over time
- Failure when additional mods are installed

Power testing needs to include load testing, thermal testing, voltage stability testing, and long-term runtime testing.

---

## Risk: Incorrect Voltage

The PS2 Slim expects a specific DC input voltage range.

If the USB-C PD trigger board negotiates the wrong voltage, the console may be damaged.

Possible failure examples:

- Trigger board outputs 12V when 9V was expected
- Trigger board outputs 20V due to incorrect configuration
- Adjustable trigger board is accidentally set wrong
- Charger and trigger board negotiate an unexpected profile
- Output voltage is not checked before connecting to the console

Any USB-C PD setup should be tested with a meter before it is ever connected to a PS2.

---

## Risk: Insufficient Current

Voltage is only part of the power requirement.

The power source must also provide enough current.

If the charger, cable, trigger board, converter, or wiring cannot provide enough current, the voltage may sag under load.

This can cause:

- Console resets
- USB-C charger shutdown
- BlueRetro or controller instability
- Storage issues
- Audio/video issues
- Heat buildup
- Unreliable behavior that is hard to diagnose

A power source that works at idle may fail during gameplay or startup.

---

## Risk: Cheap Trigger Boards

USB-C PD trigger boards are not all equal.

Some are well designed. Others are very basic modules with limited protection and unknown quality control.

Possible issues with cheap trigger boards include:

- Poor soldering
- Underrated connectors
- Weak traces
- Incorrect voltage selection
- Inconsistent negotiation
- Limited current handling
- Poor documentation
- No meaningful protection circuitry

A trigger board should not be trusted just because it says “9V” or “PD” in the listing.

It needs to be tested.

---

## Risk: USB-C Cables

The USB-C cable is part of the power system.

A poor cable can cause voltage drop, heat, or unstable operation.

Cable issues may include:

- Thin internal conductors
- Long cable length
- Poor connector quality
- Unknown current rating
- No e-marker for higher-current operation
- Excessive voltage drop under load

For higher-power use, the cable should be selected intentionally, not randomly.

---

## Risk: Voltage Sag and Startup Dips

The PS2 may draw more current during startup or during certain load conditions.

If the power source cannot respond quickly enough, the voltage can dip.

Voltage dips can cause:

- Failed boot
- Reset loops
- Random crashes
- Storage problems
- Controller problems
- Unstable behavior when the console changes load

This is why startup behavior needs to be measured.

A multimeter may not show fast dips clearly. An oscilloscope is much better for checking startup dips, ripple, and transient behavior.

---

## Risk: Ripple and Noise

A noisy power source can cause problems even if the average voltage looks correct.

Ripple and switching noise may come from:

- USB-C chargers
- Trigger boards
- Buck converters
- Poor PCB layout
- Poor capacitor selection
- Long wires
- Poor grounding

Potential symptoms may include:

- Audio noise
- Video issues
- Controller instability
- Random crashes
- Unstable storage devices
- General unreliable behavior

PowerOR needs to be tested not only for voltage level, but also for power quality.

---

## Risk: Heat

Heat is a major concern in small internal console builds.

Heat may come from:

- Trigger boards
- DC-DC converters
- Diodes
- MOSFETs
- Thin traces
- Underrated wires
- Connectors
- Poor airflow
- Internal console heat

A board that works on the bench may not be safe inside a closed PS2 shell.

Thermal testing needs to be done during real operation, not only during a quick power-on test.

---

## Risk: Backfeeding

Backfeeding happens when one power source feeds voltage into another power source or circuit path where it should not.

This is one of the major reasons PowerOR exists.

If the OEM PSU and USB-C PD source are both connected, the design must prevent them from fighting each other.

Backfeeding may damage:

- The USB-C PD trigger board
- The OEM PSU
- The PS2 power input circuit
- Protection components
- Other internal mods

PowerOR is intended to explore a safer source-selection method instead of simply tying power sources together.

---

## Risk: Poor Grounding and Wiring

Wiring matters.

A bad power mod can fail because of wiring even if the circuit idea is good.

Possible wiring problems include:

- Wire gauge too small
- Long wire runs
- Poor solder joints
- Weak ground return
- Shared noisy ground paths
- Loose connectors
- No strain relief
- Poor routing near sensitive signals

The power path should be treated as a high-current path.

Thin wires and poor solder joints can create voltage drop, heat, and instability.

---

## Risk: Heavy Internal Mods

PowerOR is not currently aimed at heavily modified consoles.

A lightly modified PS2 Slim and a heavily modified PS2 Slim do not have the same power requirements.

This project is not currently recommended for consoles with:

- RetroGEM
- Internal IDE interfaces
- Internal hard drives
- Large internal SSD setups
- High-current HDMI mods
- Multiple internal wireless modules
- Multiple internal power converters
- Unknown current draw
- Several active mods powered at the same time

Those builds may require a more robust power system with higher current capacity, better thermal handling, and additional protection.

PowerOR should be tested first on lighter builds.

---

## Why PowerOR Keeps the OEM PSU

The original OEM PS2 Slim power supply is a known-good power source for the console.

PowerOR keeps the OEM power option because it gives the build a fallback and allows USB-C PD to remain optional.

The intended behavior is:

- OEM PSU connected: OEM power has priority.
- USB-C PD connected: USB-C PD can act as an alternate input.
- Both connected: the supplies should not fight each other.
- One source removed: the system should behave predictably and safely.

Keeping the OEM power input reduces the risk of depending completely on an experimental USB-C PD setup.

---

## Why This Project Is Experimental

PowerOR is experimental because the design still needs to be proven.

The following areas need testing before this should be trusted:

- USB-C PD negotiation
- No-load voltage
- Voltage under load
- Current capacity
- Ripple and noise
- Startup behavior
- Switchover behavior
- OEM priority behavior
- Backfeed prevention
- Thermal performance
- Long-term runtime
- Behavior with real PS2 Slim consoles

Until these areas are tested, the project should not be treated as a finished solution.

---

## Testing Should Drive the Design

The goal of this project is not to prove that USB-C PD is always safe.

The goal is to test whether a controlled USB-C PD power design can be made safe enough for specific PS2 Slim use cases.

The design should move forward based on measured results, not guesses.

Good testing should include:

- Bench testing
- Dummy-load testing
- Thermal testing
- Oscilloscope testing
- Console runtime testing
- Testing with OEM PSU only
- Testing with USB-C PD only
- Testing with both power sources connected
- Testing with source removal and switchover
- Testing with the intended internal mods installed

---

## Public Feedback

Community feedback is welcome.

This project is being documented publicly because USB-C PD PS2 power mods need careful discussion.

Useful feedback includes:

- Real test results
- Known failure cases
- Charger behavior
- Trigger board behavior
- PS2 Slim current measurements
- Oscilloscope captures
- Thermal testing
- Fitment concerns
- Safety concerns

The goal is to make better decisions before any kit is released.

---

## Project Position

PowerOR does not claim that USB-C PD is automatically safe for the PS2.

PowerOR also does not claim that USB-C PD is impossible to use safely.

The position of this project is simple:

USB-C PD may be useful for selected PS2 Slim builds, but it must be designed, tested, and documented properly.

Until testing proves the design reliable, PowerOR should be treated as experimental.

---

## Disclaimer

This project involves modifying the power system of a PlayStation 2 console.

Incorrect voltage, unstable power, insufficient current, excessive ripple, poor wiring, poor grounding, or unsafe power-source switching can damage the console.

Use this information at your own risk.

Do not install this in a valuable or heavily modified console without proper testing.
