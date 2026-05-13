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

## Protection Areas Being Considered

PowerOR may need to account for several protection areas:

- Overvoltage protection
- Undervoltage behavior
- Reverse-current protection
- Backfeed prevention
- Input protection
- Fuse or eFuse protection
- TVS diode protection
- Inrush current control
- Soft-start behavior
- Heat management
- Proper grounding
- Proper wire size
- Proper PCB trace width
- Proper connector current rating

Protection should be viewed as layered risk reduction.

No single protection part makes the design automatically safe.

---

## Overvoltage Risk

Overvoltage is one of the most serious risks in a USB-C PD power project.

Possible causes include:

- Trigger board set to the wrong voltage
- Adjustable trigger board accidentally changed
- Charger negotiation issue
- Buck converter failure
- Incorrect converter feedback values
- Wiring mistake
- Source switchover spike
- Load removal overshoot

Overvoltage can damage the PS2.

This is why voltage must be measured before connecting anything to a console.

---

## Undervoltage Risk

Undervoltage may not immediately destroy the console, but it can cause unstable behavior.

Possible symptoms include:

- Failed boot
- Random resets
- Controller glitches
- Storage instability
- Audio or video problems
- USB-C charger cycling
- Internal mods behaving strangely

PowerOR needs to be tested to make sure voltage does not sag too low during startup, gameplay, or source switching.

---

## Reverse Current and Backfeed Prevention

Reverse current protection prevents current from flowing backward into a power source or circuit section.

Backfeeding is one of the main reasons PowerOR exists.

The OEM PSU and USB-C PD source should not be directly tied together. If both are connected, the design should prevent them from fighting each other.

Backfeeding risks include:

- Damage to the USB-C PD trigger board
- Damage to the OEM PSU
- Damage to protection parts
- Heat
- Charger shutdown
- Unexpected voltage on disconnected inputs
- Unreliable source switching

Power OR-ing should isolate each source while still allowing the console to receive power.

---

## Power Conditioning

Power conditioning may include:

- Bulk capacitance
- Ceramic capacitors
- Ripple reduction
- Noise filtering
- Ferrite beads, if appropriate
- Proper buck converter design
- Proper grounding
- Short high-current paths
- Wide PCB traces or copper pours
- Correct wire gauge
- Strong connectors

Bulk capacitance can help with short load changes, but too much capacitance can also create inrush current problems.

Ceramic capacitors are useful for high-frequency noise and local decoupling, especially around switching regulators.

Ripple and noise should be checked with an oscilloscope when possible.

---

## Buck Converter Considerations

If PowerOR uses a higher USB-C PD input voltage, a buck converter may be needed to step the voltage down.

A buck converter design must consider:

- Input voltage range
- Output voltage target
- Output current rating
- Efficiency
- Heat
- Inductor selection
- Input capacitors
- Output capacitors
- Feedback resistor values
- PCB layout
- Switching frequency
- Ripple
- Load transient response
- Thermal performance

A buck converter should not be selected only by its advertised current rating.

It must be tested under real load.

---

## Heat Management

Heat is a major part of power protection.

Parts to check during testing include:

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

A board that runs cool on the bench may run hotter inside a closed console shell.

Thermal testing should be done during real operation.

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

---

## Suggested Testing Sequence

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

For the full detailed write-up, see:

[Power Conditioning and Protection](Documents/08-Power-Conditioning-and-Protection.md)
