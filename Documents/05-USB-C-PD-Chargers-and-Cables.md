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

```text
Output:
5V 3A
9V 3A
12V 3A
15V 3A
20V 3.25A
