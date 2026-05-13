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

# Option 1: Purchase a Trigger Board

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

# Option 2: Design a Custom Trigger Board

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

```text
9V at up to 3A
