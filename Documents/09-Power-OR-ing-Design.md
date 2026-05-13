# Power OR-ing Design

This document covers the power OR-ing portion of the PowerOR project.

Power OR-ing is the main idea behind this project. The goal is to allow more than one possible power source while preventing those sources from directly fighting each other.

For PowerOR, the two main power sources are:

- The original PS2 Slim OEM power supply
- An optional USB-C PD power source

The intended behavior is that the OEM power supply remains the preferred/default source when connected, while USB-C PD acts as an optional alternate input.

---

## What Power OR-ing Means

Power OR-ing is a method of allowing multiple power sources to feed one load.

In this project, the load is the PS2 Slim console.

The basic idea is:

<pre>
OEM PSU Input
      \
       \
        +---- Power OR-ing ---- PS2 Console Input
       /
      /
USB-C PD Input
</pre>

The console should be able to receive power from either source, but the two sources should not be directly tied together.

Power OR-ing helps control which source powers the console and helps prevent unwanted current flow between sources.

---

## Why Power OR-ing Is Needed

PowerOR exists because simply connecting two power supplies together is not safe.

If the OEM PSU and USB-C PD output are tied together directly, one source may feed into the other.

That can cause:

- Backfeeding
- Heat
- Charger shutdown
- Damage to the USB-C PD trigger board
- Damage to the OEM PSU
- Damage to protection parts
- Unpredictable console behavior
- Voltage instability
- Unsafe source switching

Power OR-ing is used to isolate the sources while still allowing the console to receive power.

---

## PowerOR Design Goal

The design goal is:

- Keep the OEM PS2 Slim power input available.
- Add USB-C PD as an optional alternate input.
- Give the OEM PSU priority when connected.
- Prevent backfeeding between the OEM PSU and USB-C PD source.
- Keep the output voltage stable.
- Allow safe testing of both power paths.
- Avoid treating USB-C PD as a universal replacement for the OEM PSU.

The OEM power supply should remain the preferred power source.

USB-C PD should be treated as optional and experimental until testing proves otherwise.

---

## Basic Power Source Behavior

The intended behavior can be described like this:

| OEM PSU | USB-C PD | Desired Behavior |
|---|---|---|
| Connected | Not connected | Console runs from OEM PSU |
| Not connected | Connected | Console runs from USB-C PD |
| Connected | Connected | Console prefers OEM PSU |
| Removed | Connected | USB-C PD may continue powering the console if switchover is stable |
| Connected | Removed | OEM PSU powers the console normally |
| Not connected | Not connected | Console is off |

This behavior must be tested.

It should not be assumed safe just because the circuit works on paper.

---

## OEM PSU Priority

OEM PSU priority means the original PS2 power supply should be the preferred source when it is connected.

This matters because the OEM supply is already designed for the console.

Reasons to prefer the OEM PSU:

- It is the known original power source.
- It reduces dependence on USB-C PD behavior.
- It provides a fallback during testing.
- It reduces risk if the USB-C charger or trigger board behaves poorly.
- It keeps the console usable even if USB-C PD is not connected.

PowerOR should not force the console to depend only on USB-C PD.

---

## USB-C PD as Alternate Input

The USB-C PD side should be treated as an alternate input.

It may be useful for:

- Lighter PS2 Slim builds
- Ultra Slim style builds
- Builds without the optical drive
- Compact setups
- Testing modern power options
- Situations where the OEM PSU is not preferred or not available

However, USB-C PD should not be assumed suitable for every PS2.

PowerOR is not currently intended for heavily modified consoles with large power demands.

---

## Backfeeding

Backfeeding happens when current flows backward into a power source or circuit section where it should not go.

In PowerOR, backfeeding could happen in several ways:

- OEM PSU feeds into the USB-C PD trigger board.
- USB-C PD feeds into the OEM power input.
- One source charges capacitors on the other input side.
- One source powers a circuit that should be off.
- A disconnected input still has voltage present because the other source is feeding it.

Backfeeding can damage parts or cause confusing behavior.

Preventing backfeeding is one of the most important goals of PowerOR.

---

## Why Not Tie the Inputs Together?

The OEM PSU output and USB-C PD output should not be tied together directly.

Even if both sources are close in voltage, they are not identical.

Possible issues:

- One supply may be slightly higher than the other.
- The higher supply may force current into the lower supply.
- The USB-C charger may shut down.
- The OEM PSU may be stressed.
- The voltage may become unstable.
- Heat may build up in traces, wires, or protection parts.
- The console may behave unpredictably.

Power sources should be isolated from each other.

---

## Simple Diode OR-ing

The simplest form of power OR-ing uses diodes.

Each power source feeds the output through a diode.

Basic idea:

<pre>
OEM PSU ----|>|----
                 \
                  +---- PS2 Console Input
                 /
USB-C PD ---|>|----
</pre>

This prevents one source from easily feeding backward into the other source.

---

## Advantages of Diode OR-ing

Simple diode OR-ing has some advantages:

- Easy to understand
- Simple circuit
- Low parts count
- Naturally blocks reverse current
- Good for basic testing
- Easy to prototype

For early concept testing, diode OR-ing may help prove the basic behavior.

---

## Disadvantages of Diode OR-ing

The major problem with normal diodes is voltage drop.

A standard diode may drop too much voltage for this project.

Possible problems:

- Lower voltage reaches the console.
- More heat is generated.
- Efficiency is reduced.
- Voltage sag becomes worse under load.
- The diode may need to handle significant current.
- Thermal performance may become a problem inside the console.

Because the PS2 Slim input voltage margin matters, wasting voltage in a diode may not be ideal.

---

## Schottky Diode OR-ing

A Schottky diode has a lower voltage drop than many standard diodes.

This can make it more attractive for power OR-ing.

Possible advantages:

- Lower voltage drop than standard diodes
- Simpler than MOSFET-based ideal diode circuits
- Blocks reverse current
- Easy to understand

Possible concerns:

- Still has voltage drop
- Still generates heat
- Current rating matters
- Thermal performance matters
- May still waste too much voltage for the PS2 power path

Schottky diode OR-ing may be useful for early prototypes, but it may not be the best final solution.

---

## Ideal Diode / MOSFET OR-ing

A more efficient approach is to use MOSFET-based ideal diode behavior.

An ideal diode circuit attempts to act like a diode, but with much lower voltage drop.

Possible advantages:

- Lower voltage loss
- Less heat
- Better efficiency
- Better for higher-current paths
- Better voltage delivered to the console
- More suitable for compact internal installs

Possible concerns:

- More complex
- Requires proper part selection
- Requires proper layout
- May need a controller IC
- Must be tested for reverse-current blocking
- Must be tested during source switching
- Failure behavior must be understood

A MOSFET-based OR-ing design may be better for a final PowerOR board, but it must be tested carefully.

---

## Source Priority Methods

PowerOR needs OEM PSU priority.

There are different ways to create priority behavior.

Possible approaches include:

- Voltage-based priority
- Ideal diode behavior where the higher source naturally supplies the load
- Controlled MOSFET switching
- Comparator-controlled enable/disable
- Power mux controller
- eFuse or load switch arrangement
- Manual selection switch for prototype testing

The final method should be chosen based on safety, reliability, space, cost, and testing.

---

## Voltage-Based Priority

One possible approach is to let the source with the slightly higher voltage supply the load.

For example, if the OEM PSU path is slightly higher than the USB-C PD path after losses, the OEM PSU may naturally take over.

Possible advantages:

- Simple behavior
- Fewer control signals
- Less logic required

Possible concerns:

- Depends on actual voltage differences
- May vary by charger
- May vary by OEM PSU
- May not provide reliable priority
- Could result in load sharing
- Could switch unpredictably under load

Voltage-based priority should not be assumed reliable without testing.

---

## Controlled Priority

A controlled priority design intentionally enables one source and disables another.

For PowerOR, that could mean:

- Detect OEM PSU input.
- When OEM PSU is present, enable the OEM path.
- Disable or block the USB-C PD path.
- When OEM PSU is absent, allow the USB-C PD path.

Possible advantages:

- More predictable priority behavior
- Less chance of load sharing
- Better control over backfeeding
- Easier to define expected behavior

Possible concerns:

- More complex
- Requires detection circuitry
- Requires more parts
- Requires careful failure-mode testing
- Requires stable control logic

Controlled priority may be better for a final kit if it can be kept reliable and compact.

---

## Power Mux Option

A power mux is an IC designed to select between power sources.

Depending on the part, a power mux may provide:

- Source selection
- Reverse-current blocking
- Current limiting
- Priority control
- Soft start
- Fault reporting
- Overvoltage or undervoltage protection
- Thermal protection

A power mux may be useful for PowerOR, but it must be selected carefully.

Important questions:

- Can it handle the required voltage?
- Can it handle the required current?
- Does it support the desired priority behavior?
- What is the voltage drop?
- How much heat does it generate?
- Does it block reverse current?
- What happens during switchover?
- What happens during a fault?
- Is the package practical to assemble?

A power mux should not be selected only because it looks convenient on paper.

It must be tested.

---

## eFuse and Load Switch Options

An eFuse or load switch may also be useful in the power path.

Possible uses:

- Current limiting
- Controlled startup
- Reverse-current blocking
- Overvoltage protection
- Undervoltage lockout
- Thermal shutdown
- Enable/disable control
- Fault output

An eFuse may be useful on one or both inputs, but it adds complexity.

The design should avoid becoming overly complicated before the basic power behavior is understood.

---

## Manual Selection Option for Testing

For early prototypes, a manual switch may be useful.

A manual source selection switch could allow testing of:

- OEM PSU path only
- USB-C PD path only
- Both connected but only one enabled
- Different source behaviors without automatic switching

Possible advantages:

- Easier debugging
- More control during testing
- Less automatic behavior to troubleshoot
- Good for early prototypes

Possible concerns:

- Not ideal for a final kit
- User error risk
- Switch current rating matters
- Mechanical fitment matters

Manual selection can be useful during development, but the final design should reduce user error.

---

## Switchover Behavior

Switchover behavior is one of the most important parts of PowerOR testing.

Switchover means the console changes from one power source to another.

Examples:

- USB-C PD is powering the console, then OEM PSU is plugged in.
- OEM PSU is powering the console, then USB-C PD is plugged in.
- Both are connected, then OEM PSU is removed.
- Both are connected, then USB-C PD is removed.

During switchover, the design must avoid:

- Voltage spikes
- Voltage dips
- Backfeeding
- Charger shutdown
- Console resets
- Excessive heat
- Unstable behavior

Switchover should be measured with an oscilloscope when possible.

---

## Seamless vs Safe Switchover

A perfectly seamless switchover would allow one source to take over without the console noticing.

That may be difficult.

For PowerOR, safe behavior is more important than seamless behavior.

The project should first focus on:

- No backfeeding
- No overvoltage
- No dangerous spikes
- No overheating
- Predictable source behavior
- Stable operation under normal use

A console reset during a source change may be acceptable during early testing if the power path is safe.

A hidden backfeed or voltage spike is not acceptable.

---

## Load Sharing

Load sharing happens when both power sources supply part of the current at the same time.

This may happen unintentionally if both sources are close in voltage.

Load sharing can be difficult to control.

Possible concerns:

- One source may carry most of the load.
- Current may shift between sources.
- Heat may appear in unexpected places.
- The USB-C charger may react badly.
- The OEM PSU may not behave as expected.
- Testing becomes harder to interpret.

For PowerOR, the preferred behavior is source priority, not uncontrolled load sharing.

---

## Output Voltage During OR-ing

The OR-ing stage should not drop the voltage too much.

Voltage loss can happen through:

- Diodes
- MOSFETs
- eFuses
- Power mux ICs
- Connectors
- PCB traces
- Wires
- Solder joints

The voltage should be measured at:

- Each input
- After the OR-ing stage
- At the console input

The voltage at the console input is the most important measurement.

---

## Current Handling

The OR-ing components must handle the expected current.

Current handling depends on:

- Component current rating
- MOSFET RDS(on), if used
- Diode forward voltage, if used
- Thermal resistance
- PCB copper area
- Trace width
- Connector rating
- Wire gauge
- Airflow
- Console shell temperature

The OR-ing stage should not be the weak point in the power path.

---

## Heat in the OR-ing Stage

Any voltage drop at high current creates heat.

Heat can come from:

- Diodes
- MOSFETs
- eFuse ICs
- Power mux ICs
- Thin PCB traces
- Connectors
- Wires
- Poor solder joints

Thermal testing should be done during:

- Dummy-load testing
- Console startup
- Gameplay
- Long runtime
- Source switching
- Closed-shell testing, if safe

A board that works on the bench may run hotter inside a console.

---

## Failure Modes

PowerOR should consider possible failure modes.

Possible failures include:

- USB-C PD input fails off
- USB-C PD input fails high
- OEM PSU input fails or is disconnected
- OR-ing MOSFET fails open
- OR-ing MOSFET fails short
- Diode fails short
- Diode fails open
- Control circuit fails
- Power mux fails
- Charger shuts down
- Converter shuts down
- Output is shorted
- Backfeed protection fails

The goal is to reduce the chance that a single failure immediately damages the console.

---

## Test Points for OR-ing

PowerOR should include test points where possible.

Useful test points include:

- OEM input voltage
- USB-C PD input voltage
- OR-ing output voltage
- Console output voltage
- Ground
- Source-detect signal, if used
- Enable signal, if used
- Fault signal, if used

Test points make it easier to check the board before connecting it to a console.

---

## OR-ing Test Plan

Power OR-ing should be tested before console testing.

Suggested test sequence:

1. Inspect the board with no power applied.
2. Check for shorts.
3. Apply OEM PSU input only.
4. Measure OR-ing output.
5. Apply USB-C PD input only.
6. Measure OR-ing output.
7. Apply both inputs.
8. Confirm expected priority behavior.
9. Check for backfeed into the inactive or lower-priority input.
10. Add a dummy load.
11. Repeat input-only and both-input tests under load.
12. Check heat.
13. Check voltage drop.
14. Check source removal behavior.
15. Check source plug-in behavior.
16. Use an oscilloscope to check dips and spikes.
17. Only then test with a console.

The console should not be the first test load.

---

## Backfeed Test Ideas

Backfeed testing should check whether voltage appears where it should not.

Suggested checks:

| Test | Expected Result | Notes |
|---|---|---|
| OEM only, USB-C disconnected | No unsafe voltage backfed into USB-C input | Measure USB-C side |
| USB-C only, OEM disconnected | No unsafe voltage backfed into OEM input | Measure OEM side |
| Both connected | OEM priority behavior confirmed | Check current path |
| OEM removed while USB-C remains | No dangerous dip or spike | Scope preferred |
| USB-C removed while OEM remains | No dangerous dip or spike | Scope preferred |
| Dummy load connected | No excessive heat | Check OR-ing parts |

---

## Priority Test Ideas

Priority testing should verify that the OEM PSU behaves as the preferred source.

Suggested checks:

| Test | Desired Result | Notes |
|---|---|---|
| OEM connected first, then USB-C | OEM remains preferred | No reset if possible |
| USB-C connected first, then OEM | OEM takes priority | Check for dip/spike |
| Both connected at startup | OEM preferred | Confirm output behavior |
| OEM removed with USB-C connected | USB-C takes over if supported | Check stability |
| OEM reconnected | OEM returns as preferred source | Check transition |

---

## Oscilloscope Testing

An oscilloscope is strongly recommended for OR-ing testing.

Use it to check:

- Source plug-in behavior
- Source removal behavior
- Output dips
- Output spikes
- Switchover behavior
- Startup behavior
- Ripple during load
- Charger reaction
- Converter reaction

A multimeter may miss fast events that could still matter.

Oscilloscope captures should be saved in the project documentation.

Suggested folder:

<pre>
Testing/Oscilloscope-Captures/
</pre>

---

## Intended Use Case

PowerOR is intended for selected lower-power PS2 Slim builds.

This project is not currently intended for heavily modified consoles with high current draw.

Not currently recommended for:

- RetroGEM
- Internal IDE interfaces
- Internal hard drives
- Large internal SSD setups
- High-current HDMI mods
- Multiple internal wireless modules
- Multiple internal power converters
- Builds with unknown current draw

The OR-ing stage must be sized for the actual build.

---

## Public Documentation and Final Kit Files

This repository may document:

- The purpose of power OR-ing
- Design goals
- Testing process
- Risk discussion
- Fitment notes
- Public prototype notes
- Non-production diagrams

Final production files are not planned for public release at this time.

This may include:

- Final Gerbers
- Complete KiCad source
- Pick-and-place files
- Final production BOM
- Assembly files
- Manufacturing package

The goal is to document the project while protecting the final assembled kit design.

---

## Practical Design Rule

For PowerOR, the practical design rule is:

Do not let the two power sources fight each other.

That means:

- Do not tie OEM PSU and USB-C PD directly together.
- Prevent backfeeding.
- Verify OEM priority.
- Measure voltage drop.
- Check heat.
- Test under load.
- Test source switching.
- Use the console only after dummy-load testing.

Power OR-ing must be proven through testing.

---

## Project Position

Power OR-ing is the center of the PowerOR project.

The goal is not just to add a USB-C port.

The goal is to create a controlled dual-input power system for selected PS2 Slim builds, while keeping the OEM power supply as the preferred/default source.

Until the OR-ing behavior is measured and documented, the project should remain experimental.

---

## Disclaimer

This document is part of an experimental hardware project.

Unsafe power OR-ing can cause backfeeding, voltage spikes, voltage dips, heat, charger shutdown, unstable console behavior, or console damage.

Use this information at your own risk.
