# Trigger Board: Purchase or Design?

This document covers the USB-C PD trigger board portion of the PowerOR project.

A USB-C PD trigger board is the part of the system that communicates with a USB-C PD charger and requests a specific voltage profile, such as 9V, 12V, 15V, or 20V.

For PowerOR, the trigger board is one of the most important parts of the design because it controls what voltage enters the rest of the power system.

---

## Why a Trigger Board Is Needed

A USB-C PD charger does not automatically output 9V, 12V, 15V, or 20V just because a USB-C cable is plugged in.

By default, USB-C starts at 5V.

To get a higher voltage, the connected device needs to communicate with the charger and request a supported PD profile.

A trigger board does this communication.

For example:

- A 9V trigger board requests 9V from the charger.
- A 12V trigger board requests 12V from the charger.
- A 15V trigger board requests 15V from the charger.
- A 20V trigger board requests 20V from the charger.

The charger must support the requested voltage and current profile.

If the charger does not support the requested profile, the trigger board may fail to negotiate, fall back to another voltage, or behave in a way that needs to be tested.

---

## Trigger Board Role in PowerOR

In the PowerOR project, the trigger board is not the entire power solution.

It is only one section of the power system.

The full power path may include:

- USB-C port
- USB-C PD trigger circuit
- Voltage conversion, if needed
- Input protection
- Power conditioning
- Power OR-ing
- OEM PSU priority circuit
- Output wiring to the console

A trigger board by itself does not solve every power concern.

PowerOR exists because the full power path needs to be designed and tested as a system.

---

## Purchase or Design?

There are two basic options:

1. Use an off-the-shelf USB-C PD trigger board.
2. Design a custom USB-C PD trigger circuit as part of PowerOR.

Both options have advantages and disadvantages.

---

## Option 1: Purchase a Trigger Board

A purchased trigger board is the simplest way to start testing.

Purchased boards are easy to find and usually inexpensive. They allow quick experiments with USB-C PD voltage negotiation without designing the USB-C PD section from scratch.

---

## Advantages of a Purchased Trigger Board

A purchased trigger board may be useful because:

- It is quick to test.
- It is inexpensive.
- It avoids designing the PD negotiation circuit at the beginning.
- It allows early testing with chargers and cables.
- It can help prove whether USB-C PD is practical for the project.
- It reduces the number of unknowns during early development.

For early PowerOR testing, using a purchased trigger board may make sense.

It lets the project focus first on:

- Voltage behavior
- Current draw
- Charger compatibility
- Power OR-ing
- Protection
- Fitment
- Console testing

---

## Disadvantages of a Purchased Trigger Board

A purchased trigger board also has risks.

Common problems may include:

- Unknown component quality
- Poor documentation
- Unknown current capacity
- Thin PCB traces
- Poor USB-C connector strength
- No meaningful protection
- Poor soldering
- Incorrect or misleading listings
- Inconsistent behavior between boards
- Limited mechanical mounting options
- Unknown long-term reliability

A cheap trigger board should not be trusted just because it says “9V” or “PD” in the listing.

It must be tested.

---

## Purchased Board Testing Requirements

Any purchased trigger board should be tested before it is connected to a PS2.

Minimum tests should include:

- Confirm selected output voltage with a multimeter.
- Confirm charger negotiation.
- Test with the intended USB-C charger.
- Test with the intended USB-C cable.
- Test with a dummy load.
- Check voltage under load.
- Check for heat.
- Check for voltage sag.
- Check startup behavior.
- Check if the board recovers properly after power is removed.
- Check behavior with multiple chargers.

If possible, the output should also be checked with an oscilloscope for ripple, dips, spikes, and startup behavior.

---

## Purchased Board Inspection

Before using a purchased board, inspect it visually.

Check for:

- Poor solder joints
- Loose USB-C connector
- Burn marks
- Damaged components
- Missing parts
- Thin power traces
- Poor strain relief
- Questionable wire pads
- Unclear voltage selection method

If the board has solder jumpers or switches for voltage selection, verify the setting before applying power.

Do not assume the board is set correctly from the seller.

---

## Option 2: Design a Custom Trigger Board

The second option is to design the USB-C PD trigger circuit directly into the PowerOR board.

This would make PowerOR more complete and cleaner as a final kit.

---

## Advantages of a Custom Trigger Design

A custom trigger section may provide:

- Better mechanical fitment
- Cleaner board layout
- Known component selection
- Known current path
- Better documentation
- Better protection integration
- Better test point placement
- Better connector support
- More control over layout
- More control over grounding
- More consistent kit assembly

A custom design would also allow the trigger section to be planned around the rest of the PowerOR circuit instead of adapting to a random module.

---

## Disadvantages of a Custom Trigger Design

A custom trigger design is more involved.

Possible disadvantages include:

- More design work
- More research required
- More layout risk
- More prototype revisions
- More testing required
- More possible failure points
- More difficult troubleshooting
- Higher cost for early prototypes

A custom trigger circuit should not be added casually.

If the USB-C PD section is designed incorrectly, the whole power system can become unreliable or unsafe.

---

## Design Direction for PowerOR

For early development, it makes sense to test with purchased trigger boards first.

This allows the project to answer important questions:

- Can USB-C PD provide stable power for the intended PS2 Slim builds?
- Is 9V at 3A enough for the intended use case?
- Which chargers behave reliably?
- Which cables behave reliably?
- How much voltage drop occurs?
- How much heat is generated?
- What protection is needed?
- What OR-ing behavior is required?

Once the rest of the design is better understood, a custom trigger section can be considered for a later revision.

---

## 9V Direct Trigger Approach

One possible PowerOR direction is to use a trigger board that requests 9V directly from the USB-C PD charger.

This is attractive because the PS2 Slim OEM power input is commonly associated with 8.5V DC, and 9V is a common USB-C PD profile.

Possible advantages:

- Simpler power path
- Less conversion required
- Less heat compared to bucking down from a much higher voltage
- Smaller design
- Easier early testing

Possible concerns:

- 9V current may be limited depending on the charger
- Some chargers may not provide enough current at 9V
- Voltage still needs protection and conditioning
- Voltage drop through wiring and OR-ing circuitry must be measured
- 9V should not be assumed safe without testing

A 9V trigger approach may be suitable for lighter PS2 Slim builds, but it is not automatically suitable for every console.

---

## 9V at 3A Target

A practical early target for PowerOR is:

<pre>
9V at up to 3A
</pre>

This equals:

<pre>
27W
</pre>

This may be enough for selected lower-power PS2 Slim builds, especially builds without the optical drive and without high-current internal mods.

However, this must be confirmed by testing.

The full system must be tested with:

- The actual PS2 board revision
- The actual installed mods
- The actual charger
- The actual cable
- The actual trigger board
- The actual PowerOR board revision

Do not assume that 9V at 3A is enough for every PS2 Slim build.

---

## Higher Voltage Trigger With Buck Conversion

Another possible design direction is to request a higher USB-C PD voltage and then step it down with a buck converter.

Example input profiles:

- 12V
- 15V
- 20V

The buck converter would then regulate the output down to the console-safe voltage.

Possible advantages:

- More power may be available from the charger.
- Lower current flows through the USB-C input side for the same power.
- It may provide more headroom for higher-current designs.
- The final output voltage can be controlled by the buck stage.

Possible disadvantages:

- More heat
- More complexity
- More parts
- More layout sensitivity
- More ripple/noise concerns
- More testing required
- More thermal design required

This approach may be useful later, but it should be treated as a separate design path.

Never connect 12V, 15V, or 20V directly to the console input.

---

## Adjustable Trigger Boards

Some trigger boards allow the output voltage to be selected using buttons, jumpers, switches, or solder pads.

These can be useful for testing, but they also add risk.

Possible problems include:

- Accidentally selecting the wrong voltage
- The board resetting to a different voltage
- Unclear voltage display
- Poor documentation
- Button settings changing unintentionally
- No lockout against dangerous voltage selection

For a PS2 install, an adjustable trigger board should be treated carefully.

If used, the selected output voltage must be confirmed before connecting it to the console.

For a final kit, a fixed-voltage or locked configuration may be safer than a user-adjustable setup.

---

## Fixed-Voltage Trigger Boards

A fixed-voltage trigger board requests one specific PD profile.

For example:

<pre>
Fixed 9V trigger
</pre>

This may be safer for a kit because there is less chance of the end user selecting the wrong voltage.

Possible advantages:

- Simpler operation
- Less user error
- Easier documentation
- Easier testing
- More predictable behavior

Possible concerns:

- Less flexible
- Still depends on charger support
- Still needs testing
- Still may vary by board quality

For PowerOR kits, a fixed or locked voltage approach may be preferred.

---

## Current Handling

The trigger board must be able to handle the current required by the system.

Current handling depends on:

- USB-C connector
- PCB trace width
- Solder joints
- Copper thickness
- Components in the power path
- Output pads
- Wires
- Thermal design

A listing may claim a high current rating, but the board still needs to be tested.

If the board gets hot during load testing, it may not be suitable.

The trigger board should not be the weak point in the power path.

---

## Voltage Output Must Be Verified

Before connecting a trigger board to PowerOR or a console, verify the output voltage.

Recommended process:

1. Connect the trigger board to the USB-C PD charger.
2. Measure the output voltage with a multimeter.
3. Confirm the voltage matches the expected setting.
4. Apply a dummy load.
5. Measure the voltage again under load.
6. Check for heat.
7. Repeat with the intended cable.
8. Repeat with more than one charger if possible.

Do not trust the label.

Measure it.

---

## Trigger Board Test Table

Suggested trigger board documentation table:

| Item | Result | Notes |
|---|---|---|
| Trigger board name/model | TBD |  |
| Purchased or custom | TBD |  |
| Requested voltage | TBD |  |
| Charger used | TBD |  |
| Cable used | TBD |  |
| No-load voltage | TBD |  |
| Loaded voltage | TBD |  |
| Maximum tested current | TBD |  |
| Heat under load | TBD |  |
| Startup behavior checked | TBD |  |
| Ripple checked | TBD |  |
| Connector strength checked | TBD |  |
| Suitable for prototype testing | TBD |  |

---

## Trigger Board Failure Concerns

A trigger board failure can create serious problems.

Possible failure modes include:

- No output
- Wrong output voltage
- Intermittent output
- Voltage drop under load
- Excessive heat
- Failed negotiation
- Charger shutdown
- Shorted output
- Damaged USB-C connector
- Poor recovery after unplugging and reconnecting

The PowerOR design should assume that not every trigger board is trustworthy.

Protection and testing are required.

---

## Mechanical Fitment

The trigger board must fit inside the intended console build.

Mechanical concerns include:

- Board size
- USB-C port location
- Cable routing
- Mounting strength
- Clearance from the shell
- Clearance from RF shields
- Heat clearance
- Access to solder pads
- Stress on the USB-C connector

A board that works electrically may still be unsuitable if it cannot be mounted safely.

For a kit, the USB-C port should be mechanically supported so the solder joints are not carrying all insertion and removal force.

---

## Purchased Board as Prototype Tool

Purchased trigger boards should be viewed as prototype tools.

They are useful for learning and early testing, but they should not automatically become the final kit design.

They can help answer:

- Does the charger negotiate correctly?
- Is 9V stable enough?
- How much current can be drawn?
- How much heat is produced?
- How does the PS2 behave?
- Is a custom trigger section worth designing?

Once these questions are answered, the final PowerOR design can be improved.

---

## Custom Design as Future Kit Direction

A custom trigger section may make sense for a future PowerOR kit if testing shows that USB-C PD is practical.

A custom design could allow:

- Cleaner assembly
- Better mounting
- Better test points
- Better protection
- Known parts
- Better documentation
- More consistent behavior
- Better integration with PowerOR

However, the custom design should only happen after enough testing has been done to justify it.

---

## Public Documentation and Final Kit Files

This repository may document trigger board testing, design decisions, and public development notes.

However, final production files are not planned for public release at this time.

This may include:

- Final Gerbers
- Complete KiCad source
- Pick-and-place files
- Assembly files
- Final production BOM
- Manufacturing package

The public goal is to document the project, the risks, the testing, and the design direction while protecting the final assembled kit.

---

## Practical Starting Plan

The practical starting plan for PowerOR is:

1. Test purchased USB-C PD trigger boards.
2. Focus on 9V output first.
3. Confirm 9V at up to 3A where supported.
4. Test with known-good chargers and cables.
5. Use dummy loads before connecting a console.
6. Measure voltage at the trigger board output.
7. Measure voltage at the PowerOR output.
8. Measure voltage at the console input.
9. Check heat during extended use.
10. Document all results.
11. Decide later whether to design a custom trigger section.

This keeps the project moving without pretending the final trigger design is already solved.

---

## Project Position

For now, purchased trigger boards are useful for testing and learning.

A custom trigger design may be better for a final kit, but only after enough testing has been completed.

PowerOR should not depend on assumptions, seller claims, or the fact that a console powers on.

The trigger board must be tested as part of the complete power system.

---

## Disclaimer

This document is part of an experimental hardware project.

A USB-C PD trigger board can output the wrong voltage, fail under load, overheat, or behave unpredictably with certain chargers and cables.

Incorrect voltage or unstable power can damage a PlayStation 2 console.

Use this information at your own risk.
