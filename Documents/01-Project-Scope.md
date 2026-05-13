# Project Scope

PowerOR is an experimental PlayStation 2 Slim power OR-ing project.

The goal of this project is to explore a controlled way to add optional USB-C PD power support to a PS2 Slim while keeping the original OEM power supply input available.

This project is not intended to replace the OEM power input completely. The OEM power supply remains the preferred/default power source when connected.

---

## Basic Idea

PowerOR is being developed around a simple idea:

- Keep the original PS2 Slim OEM power input.
- Add an optional USB-C PD power input.
- Allow either source to power the console.
- Give the OEM power supply priority.
- Prevent the OEM PSU and USB-C PD source from directly fighting each other.
- Improve testing, documentation, and safety before any kit is released.

The project is currently in the prototype and testing stage.

---

## What This Project Is

PowerOR is:

- An experimental hardware project.
- A power OR-ing concept for PS2 Slim consoles.
- A way to test USB-C PD as an alternate power source.
- A project focused on documentation, testing, and feedback.
- A possible future assembled kit for specific PS2 Slim builds.

The intent is to develop this carefully instead of simply wiring a USB-C PD trigger board directly into a console.

---

## What This Project Is Not

PowerOR is not:

- A finished product.
- A universal USB-C power mod for every PS2.
- A proven install-ready kit yet.
- A replacement for proper power testing.
- A design intended for heavily modified consoles.
- A public release of final production Gerbers or manufacturing files.

This repository is for documenting the project, explaining the design direction, and collecting testing information.

---

## Experimental Status

This project should be treated as experimental.

USB-C PD power mods for the PS2 are a sensitive topic because poor power designs can damage consoles. Problems can come from many areas, including:

- Incorrect voltage negotiation.
- Poor-quality trigger boards.
- Underrated DC-DC converters.
- Thin wiring.
- Poor grounding.
- Voltage sag under load.
- Ripple and noise.
- Heat buildup.
- Poor switchover behavior.
- Backfeeding between power sources.

Because of this, PowerOR should not be treated as safe just because it powers on a console.

A console powering on is only the first step. Long-term testing, current testing, thermal testing, and voltage stability testing are required.

---

## Intended Consoles

PowerOR is mainly intended for lower-power PS2 Slim builds.

The best candidates are likely to be lightly modified Slim consoles, especially builds where the optical drive has been removed or is not used.

Possible target models include:

- SCPH-750xx (Later Models)
- SCPH-770xx
- SCPH-790xx

The SCPH-790xx series is especially interesting because these boards are commonly used in Ultra Slim style builds and generally draw less current than earlier Slim models.

## Out-of-Scope Consoles

This project will not target:

- Any consoles prior to SCPH-750xx (Earlier Models)
- SCPH-900xx

Earlier consoles are outside the current scope of this project because they may have different power requirements, board layouts, current draw, and fitment concerns.

The SCPH-900xx series is also outside the current scope because it uses an internal power supply and is generally sufficient as-is for this type of project.

---

## Not Intended For Heavy Builds

At this stage, PowerOR is not intended for heavily modified consoles.

This project is not currently recommended for consoles with high-power internal upgrades, such as:

- RetroGEM
- Internal IDE interfaces
- Internal hard drives
- Large internal SSD setups
- High-current HDMI mods
- Multiple internal wireless modules
- Multiple power-hungry accessories
- Builds with unknown or untested current draw

Those builds may need a more robust power system with higher current capacity, better thermal handling, and more complete protection.

PowerOR may be useful for lighter builds, but heavy builds require additional testing and may need a different design.

---

## Why Keep the OEM PSU?

The OEM PS2 Slim power supply is already designed for the console.

Keeping the OEM power option has several advantages:

- It gives the console a known-good power source.
- It allows the USB-C PD side to remain optional.
- It gives a fallback if a USB-C charger or trigger board does not behave correctly.
- It makes testing easier.
- It reduces the risk of fully depending on an unproven USB-C power setup.

The goal is not to remove the original power option. The goal is to add another option while keeping the original one available.

---

## Public Repository Scope

This repository is intended to include:

- Project overview
- Design goals
- USB-C PD discussion
- PS2 power notes
- Risk discussion
- Testing notes
- Fitment notes
- Public progress updates
- Prototype discussion
- Release planning

This repository is not intended to include:

- Final production Gerbers
- Final production KiCad source files
- Pick-and-place files
- Assembly files
- Complete manufacturing package
- Anything required to directly clone the final sellable kit

The public documentation is meant to explain the project and provide transparency while still protecting the final kit design.

---

## Future Kit Goal

The long-term goal is to develop PowerOR into an assembled kit that may be sold through my website, Etsy, and/or eBay.

Before that happens, the design needs to go through proper testing and revision.

A future kit may include:

- Assembled PowerOR board
- Recommended wiring
- Installation guidance
- Compatibility notes
- Testing results
- Safety warnings

The final kit should not be released until the design is proven reliable enough for the intended use case.

---

## Development Approach

The development process should follow this general path:

1. Define the project goals.
2. Research USB-C PD behavior.
3. Study PS2 Slim power requirements.
4. Design the USB-C PD input stage.
5. Design the voltage conversion and protection stage.
6. Design the power OR-ing section.
7. Build and test prototypes.
8. Test with dummy loads.
9. Test with real consoles.
10. Revise the design as needed.
11. Document results.
12. Decide whether the design is ready for a small kit release.

The project should move forward based on testing, not assumptions.

---

## Current Status

Current project status:

**Prototype / Experimental**

PowerOR is not finished, not fully validated, and not ready to be treated as a proven install solution.

Testing and documentation will be added as the project develops.

---

## Disclaimer

PowerOR modifies the power system of a PlayStation 2 console.

Incorrect voltage, unstable power, excessive current draw, poor wiring, or poor USB-C PD behavior can damage a console.

Use this information at your own risk.

This project is being documented as an experimental hardware development project, not as a guaranteed safe installation guide.
