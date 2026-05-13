# Fitment and Installation Planning

This document covers fitment and installation planning for the PowerOR project.

PowerOR is not only an electrical project. The board also needs to physically fit inside selected PlayStation 2 Slim builds, route wires safely, support the USB-C port mechanically, avoid interference with other internal mods, and remain serviceable.

A board that works electrically on the bench may still be unsuitable if it cannot be mounted safely inside the console.

---

## Fitment Goal

The goal of the PowerOR fitment plan is to create a board and installation method that can be used in selected PS2 Slim builds without creating unnecessary mechanical or electrical risk.

The installation should focus on:

- Safe power routing
- Strong USB-C port mounting
- Proper wire gauge
- Short power paths
- Good ground return
- Minimal stress on solder joints
- Avoiding shorts to the RF shield
- Avoiding interference with the motherboard
- Avoiding interference with other mods
- Serviceability
- Repeatable installation

PowerOR should not be designed only to fit once. It should be designed so the installation process can be repeated cleanly.

---

## Target Console Scope

PowerOR is currently focused on selected PS2 Slim consoles.

Current target range:

- SCPH-750xx
- SCPH-770xx
- SCPH-790xx

Current out-of-scope consoles:

- Any consoles prior to SCPH-750xx
- SCPH-900xx

Earlier consoles may have different power requirements, board layouts, current draw, and fitment concerns.

The SCPH-900xx series uses an internal power supply and is generally sufficient as-is for this type of project.

---

## Best Fit Candidates

The best early fitment candidates are likely lower-power Slim builds, especially Ultra Slim style builds.

Good candidates may include:

- SCPH-790xx boards
- Builds without the optical drive
- Builds with lower-current internal mods
- Builds where the OEM PSU option is still retained
- Builds where the USB-C port can be mounted cleanly
- Builds with enough room for safe wire routing

The SCPH-790xx series is especially interesting because these boards are commonly used in Ultra Slim style builds and generally draw less current than earlier Slim models.

---

## Not Intended for Heavy Builds

PowerOR is not currently intended for heavily modified consoles with large power demands.

This project is not currently recommended for builds with:

- RetroGEM
- Internal IDE interfaces
- Internal hard drives
- Large internal SSD setups
- High-current HDMI mods
- Multiple internal wireless modules
- Multiple internal power converters
- Builds with unknown current draw

Those builds may require a stronger power design with more current capacity, better thermal handling, and additional protection.

Fitment should not be considered separately from power demand.

---

## Installation Philosophy

The installation should be treated as a power-system modification, not a simple connector swap.

The install should be:

- Mechanically secure
- Electrically safe
- Easy to inspect
- Easy to test
- Clearly labeled
- Serviceable if needed
- Documented with photos
- Limited to known-compatible console models

The installer should be able to test the board before connecting it to the console.

---

## Board Placement

Board placement matters.

A good location should provide:

- Clearance from the motherboard
- Clearance from the shell
- Clearance from the RF shield
- Room for wiring
- Room for the USB-C port
- Room for test access
- Reduced risk of shorts
- Reduced heat buildup
- Mechanical support

A poor location may cause:

- Pinched wires
- Stress on the USB-C connector
- Shorts to the RF shield
- Heat buildup
- Difficult testing
- Difficult service
- Interference with other mods

Board placement should be tested with the console fully assembled, not only with the shell open.

---

## USB-C Port Location

The USB-C port location is one of the most important fitment decisions.

The port needs to be:

- Easy to access
- Mechanically supported
- Aligned cleanly with the shell
- Protected from side loading
- Strong enough for repeated cable use
- Positioned so the cable does not interfere with other ports or accessories
- Routed so the power path stays short and safe

The USB-C port should not rely only on solder joints for strength.

---

## USB-C Port Mechanical Support

USB-C cable insertion and removal can create mechanical stress.

Possible support methods include:

- Shell-mounted bracket
- Board-mounted connector with strong anchoring
- Panel-mount USB-C connector
- Laser-cut mounting plate
- 3D printed bracket
- RF shield support
- Standoffs
- Epoxy or adhesive support, if appropriate
- Combination bracket and PCB mount

The final method should avoid putting all force onto the PCB pads.

A USB-C port that wiggles or flexes is not acceptable for a kit.

---

## Shell Modification

Some installations may require shell modification.

Possible shell work may include:

- Cutting a USB-C opening
- Filing the opening cleanly
- Creating a mounting point
- Adding a bracket
- Adding clearance for the board
- Removing plastic ribs
- Adjusting internal supports

Shell modification should be done carefully.

The USB-C opening should be:

- Clean
- Centered
- Strong
- Repeatable
- Not oversized
- Not positioned where the cable stresses the board

If this becomes a kit, a template or guide may be needed.

---

## RF Shield Clearance

The PS2 Slim RF shield can be useful for structure and grounding, but it can also create short-circuit risk.

PowerOR must avoid accidental contact with:

- Exposed pads
- Power traces
- USB-C connector shell
- Test points
- Component leads
- Solder joints
- High-current pads

Possible solutions include:

- Kapton tape
- Insulating sheet
- Plastic spacer
- Standoffs
- Controlled board placement
- Rounded solder joints
- Avoiding exposed high-current pads near the shield

Any insulation should be heat-safe and should not shift during assembly.

---

## Motherboard Clearance

The PowerOR board and wiring must not press against the PS2 motherboard.

Important concerns:

- Component height
- Solder joint height
- Wire routing
- Pressure points
- RF shield contact
- Flexing during assembly
- Heat transfer
- Access to existing connectors

A board may look like it fits until the shell is fully closed.

Fitment should be checked with the full console assembled.

---

## Wire Routing

Wire routing is part of the power design.

Power wires should be:

- Short
- Secure
- Properly sized
- Routed away from sharp edges
- Routed away from moving parts
- Routed away from high-heat areas
- Routed away from sensitive signal wires when possible
- Strain relieved
- Easy to inspect

The main power path should not use thin wire.

Both positive and ground wires need to be sized for the expected current.

---

## Wire Gauge

Wire gauge should be selected based on current, length, temperature, and installation method.

For the main power path:

- Avoid very thin wire.
- Keep wire runs short.
- Use a strong ground return.
- Avoid using signal wire for power.
- Avoid long unsupported wire runs.
- Avoid routing power through weak connectors.

If the build may draw several amps, the wiring must be treated as a real power path.

Wire choice should be documented in the kit instructions.

---

## Solder Joints

Power solder joints must be mechanically and electrically solid.

Poor solder joints can cause:

- Voltage drop
- Heat
- Intermittent resets
- Charger shutdown
- Random console behavior
- Long-term failure

Power solder joints should be:

- Clean
- Properly wetted
- Mechanically supported
- Inspected under magnification if possible
- Strain relieved
- Protected from movement

A solder joint should not be used as a mechanical anchor for a cable or connector.

---

## Strain Relief

Strain relief is important because the console may be moved, opened, closed, or plugged in repeatedly.

Strain relief may be needed for:

- USB-C port
- Power input wires
- Output wires to the console
- Ground wires
- Any connector harness
- Any board-mounted cable

Possible strain relief methods:

- Adhesive cable anchors
- Kapton tape
- Small brackets
- Zip ties where appropriate
- Wire loops with slack
- Hot glue only where appropriate
- Mechanical clamps
- Standoffs

Strain relief should prevent movement from reaching delicate solder joints.

---

## Connector Planning

PowerOR may use direct solder pads or connectors.

Connectors can make installation cleaner, but they must be rated properly.

Connector concerns include:

- Current rating
- Contact resistance
- Mechanical strength
- Size
- Fitment
- Locking behavior
- Ease of installation
- Wire gauge support
- Heat
- Long-term reliability

A connector that is convenient but underrated should not be used in the main power path.

---

## Test Access

The board should allow testing after installation where possible.

Useful test access points include:

- USB-C input voltage
- OEM input voltage
- PowerOR output voltage
- Ground
- Trigger output voltage
- Buck converter output, if used
- Source-detect signal, if used
- Enable signal, if used
- Fault signal, if used

Test points are useful during:

- Initial install
- Troubleshooting
- Load testing
- Source switching tests
- Customer support
- Revision comparison

A kit should be easy to verify before the console is fully closed.

---

## Heat Clearance

Power parts need room to dissipate heat.

Heat-sensitive placement concerns include:

- Buck converter location
- Inductor location
- Diode location
- MOSFET location
- eFuse location
- Power mux location
- USB-C connector
- High-current traces
- Nearby plastic shell
- Nearby wire insulation
- Nearby internal mods

A board that is safe on the bench may run hotter inside a closed console.

Thermal testing should be done in the intended installed position.

---

## Avoiding Other Mods

PowerOR may be installed in consoles that already have other mods.

Possible nearby mods may include:

- BlueRetro
- Bluetooth audio
- HDMI adapter
- MMCE / SD2PSX
- Internal USB storage
- LEDs
- Screens
- Microcontrollers
- Modchip
- Router or network module

PowerOR wiring and placement should avoid interfering with these mods.

However, PowerOR is not currently intended for heavy builds with high-current internal upgrades.

---

## Optical Drive Removed Builds

PowerOR may be especially useful in builds where the optical drive has been removed.

Benefits may include:

- Lower current draw
- More internal space
- More routing options
- Better fitment for Ultra Slim builds
- Easier access for mounting brackets
- Reduced heat from mechanical drive activity

Even without the optical drive, power testing is still required.

The console should not be assumed safe just because the optical drive is removed.

---

## Ultra Slim Installation Planning

Ultra Slim builds may provide a better fitment path for PowerOR.

Possible advantages:

- More custom shell control
- Optical drive removed
- Lower current draw on some board revisions
- More freedom for USB-C port placement
- More freedom for board mounting
- Cleaner external layout

Possible concerns:

- Less internal height
- More custom fabrication
- More interaction with other internal mods
- Need for repeatable installation
- Need for strong connector mounting
- Heat concentration in a smaller space

Ultra Slim fitment should be documented separately by board revision when possible.

---

## Fitment Photos

Fitment photos should be saved in the repository.

Suggested image folders:

- Images/Fitment/
- Images/USB-C-Port/
- Images/USB-C-Port-Mounting-Slim/
- Images/Installed-Photos/
- Images/Testing/

Useful photos include:

- Board placement
- USB-C port location
- Shell opening
- Wire routing
- RF shield clearance
- Mounting bracket
- Installed board
- Test points
- Before/after shell closure

Photos are important because fitment is difficult to explain with text alone.

---

## Installation Notes

Each installation should document:

- Console model
- Board revision
- PowerOR revision
- Installed mods
- USB-C port location
- Board mounting method
- Wire gauge
- Wire length
- Ground connection
- OEM PSU connection point
- USB-C PD connection point
- Output connection point
- Test results
- Heat observations
- Problems found

This information will help decide whether the design is ready for wider use.

---

## Compatibility Notes

Compatibility should be documented carefully.

Suggested compatibility table:

| Console Model | Board Revision | Fitment Status | Power Status | Notes |
|---|---|---|---|---|
| SCPH-750xx | TBD | Not tested | Not tested |  |
| SCPH-770xx | TBD | Not tested | Not tested |  |
| SCPH-790xx | TBD | Not tested | Not tested |  |

Fitment status and power status should be tracked separately.

A board may physically fit but still fail power testing.

---

## Installation Risk Checklist

Before installing PowerOR into a console, check:

| Item | Status | Notes |
|---|---|---|
| Console model supported | Not checked |  |
| Current draw understood | Not checked |  |
| Board inspected | Not checked |  |
| Shorts checked | Not checked |  |
| USB-C voltage verified | Not checked |  |
| OEM PSU voltage verified | Not checked |  |
| PowerOR output verified | Not checked |  |
| Dummy-load testing completed | Not checked |  |
| Heat checked under load | Not checked |  |
| Fitment checked before soldering | Not checked |  |
| USB-C port mechanically supported | Not checked |  |
| Wire gauge selected | Not checked |  |
| Ground path confirmed | Not checked |  |
| RF shield clearance verified | Not checked |  |
| Shell closes without pressure | Not checked |  |
| Final voltage checked at console input | Not checked |  |

---

## Suggested Installation Sequence

A safe installation sequence should move from mechanical planning to electrical testing.

Suggested sequence:

1. Confirm the console model is within scope.
2. Confirm the build is not a heavy high-current build.
3. Choose the board placement.
4. Choose the USB-C port location.
5. Check shell and RF shield clearance.
6. Plan wire routing.
7. Select proper wire gauge.
8. Mount or mock up the board.
9. Mount or mock up the USB-C port.
10. Check that the shell closes without pressure.
11. Remove the board for bench testing if needed.
12. Test the board without the console.
13. Test with a dummy load.
14. Verify voltage and heat.
15. Install wiring into the console.
16. Check for shorts before applying power.
17. Test OEM PSU input.
18. Test USB-C PD input.
19. Test PowerOR output.
20. Test voltage at the console input.
21. Power the console only after the above checks pass.
22. Monitor heat and voltage during runtime.
23. Document the installation.

The console should not be the first test load.

---

## Serviceability

A good installation should allow the console to be serviced later.

Serviceability concerns include:

- Can the shell be opened without ripping wires?
- Can the board be removed if needed?
- Can the USB-C port be repaired or replaced?
- Can test points still be reached?
- Can the OEM PSU path still be used?
- Can the install be inspected?
- Can other mods be serviced?

A clean install should not make future repairs impossible.

---

## Kit Planning Considerations

If PowerOR becomes a kit, fitment needs to be repeatable.

A future kit may need:

- Pre-assembled board
- Clearly marked pads
- Recommended wire
- Mounting hardware
- USB-C port bracket
- Shell cutting guide
- Console compatibility list
- Installation photos
- Testing checklist
- Safety warnings
- Charger and cable recommendations

The kit should make the safe path easier than the unsafe path.

---

## Public Documentation and Final Kit Files

This repository may document:

- Fitment notes
- Public install planning
- Photos
- Test results
- Compatibility findings
- Prototype mounting ideas
- Non-production diagrams

Final production files are not planned for public release at this time.

This may include:

- Final Gerbers
- Complete KiCad source
- Pick-and-place files
- Final production BOM
- Assembly files
- Manufacturing package
- Final kit templates, if considered private

The goal is to document the project while protecting the final assembled kit design.

---

## Practical Fitment Rule

For PowerOR, the practical fitment rule is:

If the board cannot be mounted safely, it is not ready for installation.

That means:

- Do not rely on loose wiring.
- Do not let the USB-C port flex.
- Do not allow exposed pads to touch the RF shield.
- Do not pinch power wires.
- Do not use thin wire for the main power path.
- Do not install in unsupported heavy builds.
- Do not close the shell if it presses on the board.
- Do not skip dummy-load testing.
- Do not skip voltage testing at the console input.

Fitment must be proven just like the electrical design.

---

## Project Position

Fitment and installation planning are central to PowerOR.

This project is not simply about designing a board that works on a bench.

The board must fit, mount securely, route power safely, support the USB-C port, avoid shorts, and remain testable.

Until fitment and installation behavior have been documented, the project should remain experimental.

---

## Disclaimer

This document is part of an experimental hardware project.

Poor fitment, weak USB-C mounting, thin wiring, poor solder joints, RF shield shorts, excessive heat, or unsafe installation can damage a PlayStation 2 console.

Use this information at your own risk.
