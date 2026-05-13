# PS2 Power Requirements

This document covers the basic power requirements that matter for the PowerOR project.

PowerOR is being designed around selected PlayStation 2 Slim consoles, not every PS2 model. The goal is to understand what the console needs before deciding whether USB-C PD can be used as a safe optional power source.

This project should be driven by measured power behavior, not assumptions.

---

## Important Note

The PlayStation 2 Slim power system should not be treated casually.

A console may power on with a weak or unstable power source, but that does not mean the power system is safe or reliable.

For PowerOR, the important questions are:

- What voltage does the console expect?
- How much current does the console actually draw?
- How much current is needed during startup?
- How much margin should the power system have?
- What happens when the console has internal mods?
- What happens when the optical drive is removed?
- What happens when the power source changes from OEM PSU to USB-C PD?

---

## Target Console Range

PowerOR is currently focused on selected PS2 Slim consoles.

The main target range is:

- SCPH-750xx
- SCPH-770xx
- SCPH-790xx

These consoles are better candidates for this project than earlier PS2 models because they are Slim consoles, use an external DC power input, and are more realistic for compact custom builds.

The SCPH-790xx series is especially interesting because it is commonly used for Ultra Slim style builds and generally has lower power demand than earlier Slim models, especially when the optical drive is removed.

---

## Out-of-Scope Consoles

This project will not target:

- Any consoles prior to SCPH-750xx
- SCPH-900xx

Earlier consoles are outside the current scope of this project because they may have different power requirements, board layouts, current draw, and fitment concerns.

The SCPH-900xx series is also outside the current scope because it uses an internal power supply and is generally sufficient as-is for this type of project.

---

## Nominal Voltage

PS2 Slim consoles in the target range are designed around an external DC power input.

For this project, the original OEM power supply should be treated as the reference point.

The PowerOR design should aim to provide a console-safe voltage that behaves like the expected OEM power input.

Important points:

- The console does not only care about voltage.
- The voltage must remain stable under load.
- The voltage should not sag too low during startup.
- The voltage should not overshoot during plug-in or switchover.
- The voltage should not contain excessive ripple or noise.
- The voltage should be checked before connecting to a console.

A USB-C PD trigger board output should never be trusted without measuring it first.

---

## 8.5V vs 9V Discussion

The PS2 Slim OEM adapter is commonly associated with an 8.5V DC output.

USB-C PD commonly offers a 9V profile.

That makes 9V attractive because it is close to the PS2 Slim input voltage, but close does not automatically mean safe.

For PowerOR, 9V should be treated as a design and testing question, not an assumption.

Things to verify:

- Actual USB-C PD output voltage at no load
- Output voltage under console load
- Voltage drop through wiring and protection circuitry
- Voltage at the console input, not just at the trigger board
- Startup behavior
- Ripple and noise
- Heat
- Long-term stability

The goal is not just to get “about 9V.”  
The goal is to provide stable, console-safe power.

---

## Current Requirements

Current draw depends on the console model, board revision, optical drive state, and installed mods.

A stock console and a heavily modified console may have very different power needs.

Current draw may change during:

- Startup
- Disc drive activity
- Game loading
- USB device activity
- Controller activity
- Memory card activity
- Internal mod activity
- Wireless module activity
- Video output activity

Because of this, current testing must be done under real conditions.

---

## Why Current Headroom Matters

A power system should not be designed to run right at its limit.

If the console normally draws around a certain amount of current, the power system should have extra headroom for startup, load changes, heat, and aging parts.

Without enough current headroom, the console may experience:

- Random resets
- Failed boots
- Controller instability
- Storage instability
- Audio or video issues
- USB-C charger shutdown
- Voltage sag
- Heat buildup
- Long-term reliability problems

For PowerOR, the current rating of the charger, cable, trigger board, converter, wiring, connectors, and PCB traces all matter.

The lowest-rated part in the chain can become the weak point.

---

## Optical Drive Considerations

The optical drive can be a significant part of the console’s power demand.

A console with the optical drive removed may draw less current than a fully stock console with a working drive.

This is one reason PowerOR is especially interesting for Ultra Slim style builds.

Possible lower-power use cases include:

- Optical drive removed
- MMCE / memory-card-based storage
- Lightweight internal mods
- No internal hard drive
- No high-current video mod
- No large internal storage device

However, even with the optical drive removed, the console still needs proper power testing.

---

## Light Builds vs Heavy Builds

PowerOR is currently intended for lighter PS2 Slim builds.

This project is not currently intended for heavily modified consoles that require significantly more power.

PowerOR is not currently recommended for builds with:

- RetroGEM
- Internal IDE interfaces
- Internal hard drives
- Large internal SSD setups
- High-current HDMI mods
- Multiple internal wireless modules
- Multiple internal power converters
- Unknown or untested current draw
- Several active mods powered at the same time

Those builds may need a stronger power design with more current capacity, better thermal handling, and more complete protection.

---

## Internal Mods Increase Power Demand

Every internal mod adds some amount of power draw.

Some mods only draw a small amount. Others may add a meaningful load.

Examples of added loads may include:

- HDMI adapters
- Bluetooth controller modules
- Bluetooth audio modules
- Internal storage devices
- Router or network modules
- Displays or touchscreens
- LEDs
- Microcontrollers
- DC-DC converters
- Memory card emulators
- Fans or cooling mods

Even if each mod seems small, the total current can add up.

PowerOR should only be used when the total system current draw has been considered and tested.

---

## USB-C PD Power Limits

USB-C PD power depends on the charger, cable, and trigger board.

A charger may support 9V, but not necessarily at the current required for a console.

For example, a USB-C PD setup may advertise:

- 9V at 2A
- 9V at 3A
- 12V at 3A
- 15V at 3A
- 20V at 3A
- 20V at 5A

The profile matters.

A 9V 1.5A or 9V 2A profile may not be enough for some PS2 builds.

For this project, the power source should be selected with enough current headroom for the intended console and mod setup.

---

## 9V at 3A Target

One possible target for PowerOR is a USB-C PD trigger stage that can request 9V at up to 3A when the charger supports it.

This may be useful for lighter PS2 Slim builds.

However, 9V at 3A should not be treated as automatically enough for every console.

It must be tested with:

- The specific console model
- The specific board revision
- The intended internal mods
- The intended USB-C charger
- The intended USB-C cable
- The intended PowerOR board revision

If the console or build requires more current, a higher-power design may be needed.

---

## Higher-Power Option: Higher Voltage With Buck Conversion

For builds that need more power, another possible approach is to request a higher USB-C PD voltage and use a buck converter to step it down.

Examples:

- Request 12V and buck down
- Request 15V and buck down
- Request 20V and buck down

This can reduce current on the USB-C input side and may allow more power to be available from the charger.

However, this also adds complexity.

A buck converter design must consider:

- Output voltage accuracy
- Current capacity
- Heat
- Efficiency
- Ripple
- Layout
- Inductor selection
- Capacitor selection
- Protection
- Thermal limits
- Load transients

For PowerOR, higher-voltage input with buck conversion may be useful later, but it must be tested carefully.

---

## Voltage Drop

Voltage drop is a major concern in power wiring.

Voltage can drop across:

- USB-C cable
- USB-C connector
- Trigger board traces
- Protection circuitry
- OR-ing circuitry
- Wires
- Connectors
- PCB traces
- Solder joints

The voltage should be measured at the console input, not only at the USB-C trigger board.

A setup may look good at the trigger board but sag too low by the time it reaches the console.

---

## Wire Size and Current Path

The power path should use wire and PCB traces suitable for the expected current.

Thin wire may create:

- Voltage drop
- Heat
- Unstable console behavior
- Long-term reliability issues

The ground path matters just as much as the positive voltage path.

A weak ground return can cause instability even if the positive supply looks correct.

Power wiring should be kept short, clean, and mechanically secure.

---

## Ripple and Noise

The console needs stable DC power.

A power source can have the correct average voltage but still have excessive ripple or noise.

Ripple and noise may come from:

- USB-C chargers
- Trigger boards
- Buck converters
- Long wiring
- Poor grounding
- Poor capacitor placement
- Poor PCB layout
- Switching regulators

Ripple and noise should be checked with an oscilloscope where possible.

A multimeter is useful for average voltage, but it will not show fast dips, spikes, or switching noise clearly.

---

## Startup Behavior

Startup is one of the most important conditions to test.

During startup, the console may draw current quickly, and the power source must respond without dipping too low or overshooting.

Startup testing should check:

- Initial voltage ramp
- USB-C PD negotiation delay
- Voltage at the console input
- Any voltage dip during power-on
- Any overshoot
- Whether the console boots consistently
- Whether internal mods behave correctly

A console that boots once is not enough. Startup behavior should be tested repeatedly.

---

## Switchover Behavior

Because PowerOR is a power OR-ing project, switchover behavior matters.

Testing should include:

- OEM PSU only
- USB-C PD only
- Both sources connected
- OEM PSU plugged in while USB-C PD is active
- OEM PSU removed while USB-C PD is active
- USB-C PD plugged in while OEM PSU is active
- USB-C PD removed while OEM PSU is active

The design should avoid unsafe backfeeding and should behave predictably when sources are connected or removed.

---

## Suggested Testing Conditions

PowerOR should be tested under several conditions.

Suggested tests include:

| Test Condition | Purpose |
|---|---|
| No-load voltage | Verify output before connecting to a console |
| Dummy-load test | Test current capacity without risking a console |
| Startup test | Check voltage behavior during console power-on |
| Idle test | Measure current after boot |
| Gameplay test | Measure current during normal use |
| Long runtime test | Check heat and stability |
| Switchover test | Verify OEM and USB-C PD behavior |
| Thermal test | Check trigger board, converter, wiring, and OR-ing parts |
| Ripple test | Check power quality with an oscilloscope |
| Modded-console test | Verify behavior with the intended internal mods |

---

## Current Budget Planning

A current budget should be created for each build.

Example format:

| Device / Section | Estimated Current | Measured Current | Notes |
|---|---:|---:|---|
| PS2 Slim motherboard | TBD | TBD | Measure by board revision |
| Optical drive | TBD | TBD | Removed in some builds |
| HDMI adapter | TBD | TBD | Depends on device |
| BlueRetro / Bluetooth module | TBD | TBD | Depends on board |
| Audio module | TBD | TBD | If installed |
| Storage device | TBD | TBD | If installed |
| LEDs / display | TBD | TBD | If installed |
| Safety margin | TBD | TBD | Add headroom |
| Total | TBD | TBD | Must be below safe supply limit |

The measured current is more important than the estimate.

---

## Practical Rule for PowerOR

For this project, the practical rule should be:

Do not use PowerOR on a build unless the total current draw has been measured or reasonably tested.

The power source should have enough margin for:

- Startup load
- Normal gameplay
- Internal mods
- Heat
- Cable voltage drop
- Converter losses
- Long-term reliability

---

## Project Position

PowerOR is not being designed as a universal high-current PS2 power solution.

It is being developed for selected PS2 Slim builds where the power demand is understood and controlled.

The current focus is:

- Lower-power Slim builds
- OEM PSU priority
- Optional USB-C PD power
- Careful testing
- Avoiding heavy modded consoles until a stronger design is proven

The design should only move forward based on real test results.

---

## Disclaimer

This document is part of an experimental hardware project.

Do not assume a USB-C PD power setup is safe for a PS2 just because the voltage looks close or the console powers on.

Incorrect voltage, insufficient current, poor wiring, voltage sag, ripple, heat, or unsafe switchover behavior can damage a console.

Use this information at your own risk.
