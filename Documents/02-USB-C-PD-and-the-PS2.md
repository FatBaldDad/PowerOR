# USB-C PD and the PS2

This document explains the basic idea behind using USB-C Power Delivery with a PlayStation 2 Slim console and how it relates to the PowerOR project.

PowerOR is not simply a “USB-C power mod.” The goal is to study whether USB-C PD can be used as an optional alternate power source for specific PS2 Slim builds while keeping the original OEM power supply available.

---

## What Is USB-C PD?

USB-C PD stands for **USB-C Power Delivery**.

A normal USB connection usually starts at 5V. With USB-C PD, the charger and the connected device can communicate and agree on a higher voltage and current profile.

Common USB-C PD voltage profiles may include:

- 5V
- 9V
- 12V
- 15V
- 20V

Not every charger supports every voltage or current level. The charger, cable, and trigger board all matter.

---

## Why USB-C PD Is Interesting for the PS2

The PS2 Slim normally uses an external DC power supply.

For custom PS2 Slim builds, USB-C PD is interesting because it may allow:

- A more modern power connector
- Easier charger replacement
- Cleaner portable-style builds
- Smaller external power supply options
- A possible backup or alternate input source

However, USB-C PD is only useful if the voltage and current are correct and stable.

Just because a USB-C PD board can power on a PS2 does not mean the setup is safe.

---

## USB-C PD Is Not Automatically Safe

USB-C PD by itself does not protect the console from every possible problem.

A poor USB-C PD setup can still create issues such as:

- Wrong voltage output
- Poor voltage negotiation
- Voltage sag under load
- Startup dips
- Ripple and noise
- Excessive heat
- Poor grounding
- Underrated wiring
- Underrated trigger boards
- Underrated DC-DC converters
- Backfeeding between power sources

This is why PowerOR is being treated as an experimental hardware project and not a finished install solution.

---

## Why a Trigger Board Is Needed

A USB-C PD charger does not automatically output 9V, 12V, 15V, or 20V just because it is plugged in.

The connected device has to request a voltage profile.

A **USB-C PD trigger board** is a small circuit that communicates with the charger and requests a specific voltage.

For this project, a trigger board may be used to request a voltage such as:

- 9V directly
- 12V or 20V followed by a DC-DC converter

The exact approach depends on the power design, current requirements, heat, and testing results.

---

## Direct 9V vs Higher Voltage With Buck Conversion

There are two basic approaches being considered.

### Option 1: Request 9V From USB-C PD

The trigger board requests 9V directly from the charger.

Possible advantages:

- Simpler design
- Less voltage conversion required
- Less heat from conversion
- Smaller circuit

Possible concerns:

- Limited current depending on the charger
- Some chargers may only provide 9V at lower current
- Voltage still needs to be tested under load
- Output may still need filtering and protection

---

### Option 2: Request Higher Voltage and Buck Down

The trigger board requests a higher voltage such as 12V, 15V, or 20V, then a DC-DC buck converter steps it down to the target console voltage.

Possible advantages:

- More power may be available from the charger
- Lower current on the USB-C input side
- Better option for higher-power designs
- More control over final output voltage

Possible concerns:

- More complex design
- More heat from the buck converter
- Requires careful converter selection
- Requires proper layout, filtering, and testing
- More parts and more failure points

For PowerOR, the best approach should be decided by testing, not assumptions.

---

## Why Current Capability Matters

Voltage is only one part of the power system.

The console also needs enough current.

A power source that can provide the correct voltage but not enough current may cause:

- Console instability
- Random resets
- Audio or video issues
- Controller issues
- Storage issues
- USB-C charger shutdown
- Voltage sag
- Excessive heat

This is especially important if the console has internal mods.

---

## Light Builds vs Heavy Builds

PowerOR is currently intended for lighter PS2 Slim builds.

This project is not currently aimed at heavily modified consoles with high-current internal upgrades.

Not recommended at this stage for builds with:

- RetroGEM
- Internal IDE interfaces
- Internal hard drives
- Large internal SSD setups
- Multiple high-current accessories
- Multiple internal power converters
- Unknown or untested current draw

Heavy builds may need a more robust power supply design with more current capacity, more thermal headroom, and more protection.

---

## Why Keep the OEM Power Supply?

The OEM PS2 Slim power supply is already designed for the console.

PowerOR keeps the OEM power input because it provides a known-good power option.

The intended behavior is:

- OEM PSU connected: use OEM power as the preferred source.
- USB-C PD connected: use USB-C PD as an optional alternate source.
- Both connected: OEM PSU should have priority.
- One source removed: the other source may continue powering the system if the design supports safe switchover.

The goal is not to remove the original power option.

The goal is to add a controlled alternate power path.

---

## Why Not Wire a USB-C PD Trigger Board Directly to the PS2?

A simple trigger board connected directly to the console may work, but it does not answer all safety concerns.

A direct setup may not include:

- OEM PSU priority
- Backfeed prevention
- Input protection
- Output filtering
- Voltage monitoring
- Proper current handling
- Thermal design
- Safe source switching
- Proper testing points

PowerOR exists because the power system should be treated as a full design, not just a connector swap.

---

## USB-C Charger Requirements

Not all USB-C chargers are equal.

A charger used with this project should be tested for:

- Supported voltage profiles
- Supported current at the selected voltage
- Stability under load
- Behavior during startup
- Behavior during sudden load changes
- Heat
- Shutdown behavior
- Cable compatibility

A charger that works for a phone may not be a good choice for a game console.

---

## Cable Requirements

The USB-C cable matters too.

A poor or thin cable can create voltage drop, heat, or unstable operation.

Things to consider:

- Cable current rating
- Cable length
- Wire gauge
- Connector quality
- E-marker support for higher-current setups
- Voltage drop under load

The cable should be treated as part of the power system, not an afterthought.

---

## What Needs To Be Measured?

Before USB-C PD power can be considered usable for a PS2 Slim, the design needs real testing.

Important measurements include:

- No-load output voltage
- Voltage under load
- Startup voltage behavior
- Current draw
- Voltage ripple
- Voltage sag
- Heat at the trigger board
- Heat at the DC-DC converter
- Heat at wiring and connectors
- Behavior when the OEM PSU is connected
- Behavior when USB-C PD is connected
- Behavior when both are connected
- Behavior when one source is unplugged

A multimeter is useful, but an oscilloscope is better for seeing startup behavior, dips, ripple, and transient events.

---

## PowerOR Development Goal

The goal of PowerOR is to explore a safer and more controlled way to use USB-C PD with selected PS2 Slim builds.

The design should focus on:

- OEM PSU priority
- Optional USB-C PD input
- Backfeed prevention
- Stable output voltage
- Sufficient current capacity
- Proper wiring
- Proper protection
- Proper testing
- Clear documentation

This project should move forward based on measured results.

---

## Current Position

USB-C PD may be useful for PS2 Slim builds, but it should not be treated as automatically safe.

PowerOR is being developed to test the idea carefully and document the process.

Until testing proves otherwise, this project should be considered experimental.
