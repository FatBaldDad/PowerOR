# Power Conditioning and Protection

This document covers power conditioning and protection for the PowerOR project.

PowerOR is not just about getting USB-C PD power into a PlayStation 2 Slim. The power also needs to be controlled, protected, filtered, and tested before it should be trusted in a console.

The goal is to reduce risk by treating the power path as a complete system.

---

## Why Power Conditioning Matters

A PS2 Slim needs stable DC power.

Even if a USB-C PD trigger board outputs the correct voltage, the power may still need conditioning before it is safe or reliable for console use.

Power conditioning helps with:

- Voltage stability
- Short load changes
- Startup behavior
- Ripple reduction
- Noise reduction
- Voltage dips
- Transient response
- General reliability

The goal is not only to reach the correct voltage.

The goal is to keep the voltage stable while the console is actually running.

---

## Why Protection Matters

Protection is important because a mistake or failure in the power path can damage the console.

Possible problems include:

- Wrong USB-C PD voltage
- Overvoltage
- Undervoltage
- Reverse current
- Backfeeding
- Short circuit
- Excessive current draw
- Heat
- Poor wiring
- Poor grounding
- Charger failure
- Trigger board failure
- Buck converter failure

PowerOR should be designed so that one bad condition is less likely to immediately damage the console.

---

## Power Path Overview

The PowerOR power path may include:

<pre>
USB-C PD Charger
        ↓
USB-C Cable
        ↓
USB-C Port
        ↓
PD Trigger Board / Trigger Circuit
        ↓
Protection
        ↓
Voltage Conversion, if needed
        ↓
Power Conditioning
        ↓
Power OR-ing
        ↓
PS2 Console Input
</pre>

The OEM PSU side also needs to be considered:

<pre>
OEM PS2 Power Supply
        ↓
OEM Power Input
        ↓
Protection / Priority Path
        ↓
Power OR-ing
        ↓
PS2 Console Input
</pre>

Both paths must be handled safely.

---

## Correct Voltage First

The first layer of protection is making sure the correct voltage is present before connecting the console.

For PowerOR, every power source should be checked before use.

Basic checks:

- Confirm USB-C PD trigger output voltage.
- Confirm OEM PSU output voltage.
- Confirm PowerOR output voltage.
- Confirm voltage at the console input.
- Confirm voltage under load.
- Confirm no unexpected voltage appears on the inactive power input.

Never assume a board is correct because of a label or seller description.

Measure it.

---

## Overvoltage Protection

Overvoltage happens when the voltage is higher than the console should receive.

This is one of the most serious risks in a USB-C PD project.

Possible causes:

- Trigger board set to the wrong voltage
- Adjustable trigger board accidentally changed
- Charger negotiation issue
- Buck converter failure
- Incorrect resistor values in a converter feedback network
- Wiring mistake
- Source switchover spike
- Load removal overshoot

Overvoltage can damage the PS2.

Protection options to consider may include:

- TVS diode
- Fuse or resettable fuse
- eFuse
- Overvoltage protection IC
- Crowbar-style protection
- Comparator-controlled shutdown
- Careful fixed-voltage trigger selection
- Locked or non-adjustable voltage configuration

The final protection method should be selected based on testing, board space, cost, and reliability.

---

## Undervoltage Behavior

Undervoltage happens when the console receives too little voltage.

Undervoltage may not immediately destroy the console, but it can cause unstable behavior.

Possible symptoms include:

- Failed boot
- Random resets
- Controller glitches
- Storage instability
- Audio or video problems
- USB-C charger cycling
- Internal mods behaving strangely

Possible causes include:

- Charger cannot supply enough current
- Cable voltage drop
- Trigger board current limit
- Buck converter current limit
- Thin wiring
- Poor solder joints
- Weak ground return
- Source switchover dip

PowerOR should be tested to make sure voltage does not sag too low during startup or gameplay.

---

## Reverse Current Protection

Reverse current protection prevents current from flowing backward into a power source or circuit section.

This is important because PowerOR is designed around more than one possible power source.

Without reverse current protection, one power source may feed into another.

Examples:

- OEM PSU backfeeding into the USB-C PD trigger board
- USB-C PD backfeeding into the OEM power input
- One rail feeding a section that should be off
- A capacitor discharging into the wrong part of the circuit

Reverse current can damage parts or cause confusing behavior.

PowerOR should prevent unwanted reverse current paths.

---

## Backfeed Prevention

Backfeeding is one of the main reasons PowerOR exists.

The OEM PSU and USB-C PD source should not be directly tied together.

If both are connected, the design should prevent them from fighting each other.

Backfeeding risks include:

- Damage to the USB-C PD trigger board
- Damage to the OEM PSU
- Damage to protection parts
- Heat
- Charger shutdown
- Unexpected voltage on disconnected inputs
- Unreliable source switching

Power OR-ing should be designed so each source is isolated from the other while still allowing the console to receive power.

---

## Input Protection

Input protection helps protect the board from problems at the power entry point.

Possible input protection features include:

- Fuse
- Resettable fuse
- TVS diode
- Reverse-current blocking
- Overvoltage protection
- Input capacitors
- Proper connector rating
- Proper trace width
- Proper ground return

The USB-C input and OEM input may not need identical protection, but both should be considered.

---

## Fuse Protection

A fuse or resettable fuse can help protect against excessive current.

Possible fuse options:

- Traditional fuse
- Resettable polyfuse / PTC
- Electronic fuse / eFuse

A fuse does not fix every problem, but it can help prevent a fault from becoming worse.

Things to consider:

- Hold current
- Trip current
- Voltage rating
- Resistance
- Heat
- Reset behavior
- Trip time
- Whether it protects the console or only the board

A fuse should be selected based on the expected current draw and safe operating margin.

---

## eFuse Option

An eFuse is an electronic fuse IC that can provide more controlled protection than a simple fuse.

Depending on the part, an eFuse may provide features such as:

- Current limiting
- Overvoltage protection
- Undervoltage lockout
- Reverse-current blocking
- Thermal shutdown
- Soft start
- Fault reporting

An eFuse may be useful for PowerOR, but it adds cost, design complexity, and layout requirements.

If an eFuse is used, it should be tested under real conditions before being trusted in a console.

---

## TVS Diode Protection

A TVS diode can help clamp short voltage spikes.

This may be useful for protecting against transient events.

Possible transient sources:

- Plugging in a charger
- Unplugging a charger
- Source switching
- Cable connection bounce
- Load changes
- Charger behavior
- Buck converter behavior

A TVS diode is not a complete overvoltage protection system.

It is usually used as part of a larger protection approach.

The TVS diode must be selected for the expected voltage and fault behavior.

---

## Bulk Capacitance

Bulk capacitance can help support the power rail during short load changes.

It may help reduce short dips when the load changes suddenly.

Possible benefits:

- Helps absorb short current demands
- Helps reduce voltage dips
- Helps stabilize the input or output rail
- Helps during startup or source switching

Possible concerns:

- Too much capacitance can create high inrush current.
- Large capacitors take space.
- Capacitors have voltage and temperature ratings.
- Capacitor ESR matters.
- Capacitor placement matters.

Bulk capacitance should be added intentionally, not randomly.

---

## Ceramic Capacitors

Ceramic capacitors are useful for high-frequency noise and local decoupling.

They can help reduce switching noise and ripple when placed properly.

Important points:

- Place close to the parts they support.
- Use proper voltage rating.
- Understand that capacitance drops with DC bias.
- Use multiple values if needed.
- Keep loop areas small.
- Follow regulator datasheet layout recommendations.

Ceramic capacitors are especially important around buck converters and switching circuits.

---

## Ripple Reduction

Ripple reduction is important if the design uses a switching regulator or noisy USB-C source.

Ripple may be reduced with:

- Proper output capacitors
- Proper input capacitors
- Good PCB layout
- Short current loops
- Low-ESR capacitors where appropriate
- Inductor selection
- Ferrite beads, if appropriate
- Filtering stages
- Proper grounding

Ripple should be measured with an oscilloscope.

A multimeter will not show ripple clearly.

---

## Ferrite Beads

Ferrite beads may be useful for reducing high-frequency noise in some parts of the design.

However, they should not be used as a magic fix.

Things to consider:

- Current rating
- DC resistance
- Impedance at the noise frequency
- Heat
- Voltage drop
- Placement
- Whether the bead affects regulator stability

Ferrite beads can help with noise, but they do not replace proper layout, grounding, and capacitor placement.

---

## Buck Converter Considerations

If PowerOR uses a higher USB-C PD input voltage, a buck converter may be needed to step the voltage down.

A buck converter design must be handled carefully.

Important considerations:

- Input voltage range
- Output voltage target
- Output current rating
- Efficiency
- Heat
- Inductor selection
- Catch diode or synchronous rectification
- Input capacitors
- Output capacitors
- Feedback resistor values
- Layout
- Switching frequency
- Ripple
- Load transient response
- Thermal performance

A buck converter should not be selected only by its advertised current rating.

It must be tested.

---

## Converter Current Rating

Many DC-DC converter modules advertise optimistic current ratings.

A module that claims 5A may not safely provide 5A continuously inside a closed console shell.

Current rating depends on:

- Heat sinking
- Airflow
- Input voltage
- Output voltage
- Efficiency
- Inductor size
- IC thermal limits
- Diode or MOSFET heating
- PCB copper area
- Ambient temperature

For PowerOR, converter current capacity should be verified with dummy-load testing and thermal testing.

---

## Heat Management

Heat is a major part of power protection.

Power components can get hot during normal operation.

Parts to check:

- USB-C port
- Trigger board
- Buck converter IC
- Inductor
- Diode
- MOSFETs
- eFuse
- OR-ing parts
- Wires
- Connectors
- PCB traces
- Capacitors

Thermal testing should be done:

- At idle
- Under dummy load
- During gameplay
- During long runtime
- With the console shell closed, if safe
- With the intended internal mods installed

A board that runs cool on the bench may run hotter inside the console.

---

## Inrush Current

Inrush current is the current drawn when power is first applied and capacitors charge.

Too much inrush current may cause:

- Charger shutdown
- Trigger board reset
- Spark at connector
- Voltage dip
- Stress on components
- Source switchover problems

Possible ways to manage inrush include:

- Soft-start converter
- eFuse with controlled startup
- Current limiting
- Careful capacitor sizing
- Controlled load connection
- Proper source sequencing

Inrush behavior should be measured during startup.

---

## Soft Start

Soft start allows the output voltage to rise in a controlled way instead of snapping on instantly.

This can reduce stress on the charger, trigger board, converter, and console.

Soft start may help with:

- Inrush current
- Startup dips
- Charger compatibility
- Converter stability
- Source switching behavior

If a buck converter or eFuse supports soft start, it may be useful for PowerOR.

---

## Grounding

Grounding is part of power conditioning.

A poor ground path can cause instability even if the positive voltage looks correct.

Grounding concerns include:

- Thin ground wires
- Long ground paths
- Shared noisy current paths
- Poor solder joints
- Small PCB ground return
- Bad connector contact
- Ground bounce during load changes

The positive power path and ground return should both be sized for the expected current.

---

## PCB Trace Width

The PCB traces in the power path must be sized for the expected current.

Thin traces can cause:

- Voltage drop
- Heat
- Reliability problems
- Power instability

Trace width depends on:

- Current
- Copper thickness
- Temperature rise
- Trace length
- Board thickness
- Internal or external layer
- Available copper pour area

PowerOR should use wide traces or copper pours for high-current paths wherever possible.

---

## Wire Size

Wire size matters.

Undersized wire can create voltage drop and heat.

For PowerOR, the wiring should be selected based on the expected current and length.

Important wiring points:

- Keep high-current wires short.
- Use wire gauge appropriate for the load.
- Use strong ground wiring.
- Avoid thin wires for main power.
- Avoid weak solder joints.
- Add strain relief where needed.
- Route power wires away from sensitive signals when possible.

The wiring is part of the power system.

---

## Connectors

Connectors must be rated for the expected current.

Connector concerns include:

- Current rating
- Contact resistance
- Mechanical strength
- Insertion/removal stress
- Solder joint strength
- Heat
- Fitment inside the console
- Strain relief

A weak connector can become a failure point even if the circuit design is good.

---

## Test Points

PowerOR should include useful test points where possible.

Helpful test points may include:

- USB-C input voltage
- OEM input voltage
- PowerOR output voltage
- Ground
- Trigger board output
- Buck converter output
- Fault signal, if used
- Enable signal, if used

Test points make it easier to verify the board before connecting it to a console.

They also make troubleshooting safer and cleaner.

---

## Protection Against User Error

A final kit should try to reduce user error.

Possible user-error risks include:

- Wrong charger
- Wrong cable
- Wrong voltage trigger setting
- Reversed wiring
- Poor soldering
- Use in a heavy build
- Use with unsupported console models
- Installing without testing
- Assuming any USB-C charger is safe

Documentation and design should work together to reduce these risks.

Possible design choices:

- Fixed-voltage trigger configuration
- Clear labels
- Test pads
- Keyed connectors where possible
- Strong warnings
- Compatibility notes
- Pre-assembled board
- Pre-tested kit

---

## Protection Is Not a Guarantee

Protection circuitry reduces risk, but it does not make the project impossible to damage.

A bad enough fault can still cause damage.

Protection should be viewed as layered risk reduction.

PowerOR should still require:

- Correct charger
- Correct cable
- Correct wiring
- Correct installation
- Proper testing
- Appropriate console selection
- Reasonable current load

No single protection component makes the design automatically safe.

---

## Suggested Protection Checklist

| Protection Area | Status | Notes |
|---|---|---|
| Correct USB-C PD voltage verified | Not started |  |
| OEM PSU voltage verified | Not started |  |
| Reverse-current protection considered | Not started |  |
| Backfeed prevention tested | Not started |  |
| Overvoltage protection considered | Not started |  |
| Undervoltage behavior tested | Not started |  |
| Fuse or eFuse considered | Not started |  |
| Input capacitance reviewed | Not started |  |
| Output capacitance reviewed | Not started |  |
| Ripple tested | Not started |  |
| Startup inrush tested | Not started |  |
| Thermal testing completed | Not started |  |
| Wire size reviewed | Not started |  |
| PCB trace width reviewed | Not started |  |
| Connector current rating reviewed | Not started |  |
| Console runtime tested | Not started |  |

---

## Suggested Test Sequence

A safe testing sequence should move from low-risk tests to higher-risk tests.

Suggested order:

1. Inspect the board with no power applied.
2. Check for shorts with a multimeter.
3. Power the USB-C PD trigger board alone.
4. Verify trigger board output voltage.
5. Power the PowerOR board with no console connected.
6. Verify PowerOR output voltage.
7. Test with a dummy load.
8. Check voltage under load.
9. Check heat under load.
10. Check ripple with an oscilloscope if available.
11. Test OEM PSU input.
12. Test USB-C PD input.
13. Test both inputs connected.
14. Test source switching.
15. Only then test with a console.
16. Monitor heat and voltage during console testing.

The console should not be the first test load.

---

## Practical Design Rule

For PowerOR, the practical design rule is:

The power system should be designed to fail safely whenever possible.

That means:

- Avoid exposing the console to the wrong voltage.
- Avoid tying power sources directly together.
- Avoid underrated parts.
- Avoid thin wires in the main power path.
- Avoid unknown trigger board behavior.
- Avoid relying on one protection part to solve everything.
- Test before connecting to the console.

---

## Project Position

Power conditioning and protection are central to PowerOR.

This project is not about simply adding a USB-C port to a PS2.

The goal is to create a controlled power system that can be tested, documented, and possibly developed into a kit for selected lower-power PS2 Slim builds.

Until the power conditioning and protection have been tested, the project should remain experimental.

---

## Disclaimer

This document is part of an experimental hardware project.

Incorrect voltage, insufficient current, excessive ripple, unsafe source switching, poor protection, poor wiring, or excessive heat can damage a PlayStation 2 console.

Use this information at your own risk.
