# Board Design

This document covers the board design direction for the PowerOR project.

PowerOR is an experimental power OR-ing board for selected PlayStation 2 Slim builds. The goal is to support the original OEM PS2 power supply and an optional USB-C PD input while keeping the OEM supply as the preferred/default power source.

This document is a public design discussion and development log. It is not a release of final production files.

---

## Board Design Goal

The goal of the PowerOR board is to combine several power-related functions into a compact board that can be tested, revised, and eventually developed into an assembled kit.

The board may include:

- USB-C input
- USB-C PD trigger section or trigger board interface
- Voltage conversion, if needed
- Input protection
- Power conditioning
- Power OR-ing
- OEM PSU priority behavior
- Test points
- Mounting and fitment features
- Clear labeling for installation and testing

The design should be compact enough for selected PS2 Slim builds, but not so small that safety, trace width, heat, or testability are ignored.

---

## What This Board Is

PowerOR is intended to be:

- A prototype power board
- A controlled way to test USB-C PD power on selected PS2 Slim builds
- A dual-input power system with OEM PSU priority
- A safer alternative to directly wiring a USB-C PD trigger board to the console
- A possible future assembled kit

The board is being developed to test the idea properly before it is treated as a finished solution.

---

## What This Board Is Not

PowerOR is not:

- A finished product yet
- A universal USB-C power mod for every PS2
- A board intended for all PS2 models
- A high-current power solution for heavily modified consoles
- A public release of final Gerbers or manufacturing files
- A guarantee that USB-C PD is safe for every PS2 build

This board should be treated as experimental until testing proves otherwise.

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

Those builds may require a more robust power system with higher current capacity, better thermal handling, and additional protection.

---

# Design Discussion

The board design can be broken into several major sections:

- Part I - USB-C Port
- Part II - Trigger Board
- Part III - Voltage Conversion, Protection, and Conditioning
- Part IV - Power OR-ing
- Part V - PCB Layout Direction
- Part VI - Mechanical Fitment
- Part VII - Release and Kit Planning

Each section should be developed and tested as part of the full power system.

---

# Part I - USB-C Port

The USB-C port is the physical entry point for the USB-C PD power source.

This part of the design is important because the connector must handle both electrical and mechanical stress.

---

## USB-C Port Goals

The USB-C port should:

- Support USB-C PD power input
- Be mechanically strong
- Fit the intended console shell
- Be easy to mount cleanly
- Avoid stressing solder joints
- Allow repeatable installation
- Support the expected current
- Connect cleanly to the trigger section

The USB-C connector should not be treated as just a cosmetic upgrade. It is part of the power path.

---

## Connector Strength

USB-C ports can be damaged if the shell or board does not support them properly.

A weak USB-C install may fail because of:

- Cable insertion force
- Cable removal force
- Side loading
- Poor mounting
- Thin PCB material
- Weak solder joints
- No strain relief
- Poor shell fitment

For a kit, the USB-C port should be mechanically supported so the PCB solder joints are not carrying all the force.

---

## USB-C Port Mounting

Possible mounting approaches include:

- Board-mounted USB-C connector
- Small daughterboard for the USB-C port
- Panel-mounted USB-C connector
- 3D printed bracket
- Laser-cut mounting plate
- Shell-mounted support
- RF shield support, if appropriate

The final choice should be based on fitment, strength, and ease of installation.

A connector that works electrically is not enough if it cannot survive normal cable use.

---

## USB-C Pin Access

For USB-C PD, the design needs access to the correct pins.

Important signals may include:

- VBUS
- GND
- CC1
- CC2

The CC pins are required for USB-C PD negotiation.

A connector that only exposes VBUS, GND, D+, and D- is not enough for normal USB-C PD negotiation.

---

## USB-C Port Testing

USB-C port testing should include:

- Visual inspection
- Continuity check
- Short check
- Mechanical fitment check
- Cable insertion/removal test
- Voltage check at the port
- Heat check under load
- Wiggle test during load testing
- Strain check after mounting

The port should be tested before connecting the board to a console.

---

# Part II - Trigger Board

The trigger board or trigger circuit is the section that requests the desired USB-C PD voltage from the charger.

This section controls what voltage enters the rest of the PowerOR system.

---

## Trigger Section Goals

The trigger section should:

- Request the intended USB-C PD voltage
- Behave predictably with supported chargers
- Be easy to test
- Avoid user-adjustable mistakes if used in a kit
- Support the required current
- Fit the mechanical design
- Provide clear output pads or routing
- Avoid becoming the weak point in the power path

The trigger section should never be trusted without measurement.

---

## Purchased Trigger Board Direction

For early prototypes, purchased USB-C PD trigger boards may be useful.

They allow testing of:

- Charger behavior
- Cable behavior
- 9V output
- Current capability
- Heat
- Fitment
- PowerOR input behavior

Purchased trigger boards should be treated as prototype tools, not automatically as the final kit solution.

---

## Custom Trigger Section Direction

A custom trigger section may be considered later.

A custom trigger design could provide:

- Better fitment
- Better test points
- Better documentation
- Known components
- Stronger connector support
- Better integration with protection circuitry
- Cleaner kit assembly

However, a custom trigger section adds design risk and should only be developed after enough testing has been completed.

---

## Fixed vs Adjustable Trigger

For prototype testing, adjustable trigger boards may be useful.

For a final kit, a fixed or locked voltage configuration may be safer.

Adjustable boards can create risk if:

- The wrong voltage is selected
- A button changes the setting
- The display is misunderstood
- The board resets to a different mode
- The installer assumes the voltage without measuring it

For PowerOR, the trigger voltage must always be verified before connecting to a console.

---

## Early Trigger Target

One early target for PowerOR is:

<pre>
9V at up to 3A
</pre>

This may be useful for lower-power PS2 Slim builds.

However, 9V at 3A should not be assumed suitable for every console or every mod setup.

The full system must be tested with:

- The actual console model
- The actual board revision
- The actual internal mods
- The actual charger
- The actual cable
- The actual trigger board
- The actual PowerOR board revision

---

# Part III - Voltage Conversion, Protection, and Conditioning

This section covers the parts of the board that make the power safer and more stable before it reaches the console.

This may include voltage conversion, input protection, filtering, test points, and safety features.

---

## Voltage Conversion

If the USB-C PD side requests 9V directly, voltage conversion may not be needed.

If the USB-C PD side requests a higher voltage, such as 12V, 15V, or 20V, a buck converter is required to step the voltage down.

Possible approaches:

- Direct 9V USB-C PD input
- 12V input with buck conversion
- 15V input with buck conversion
- 20V input with buck conversion

Higher voltage with buck conversion may allow more available power, but it adds complexity, heat, ripple, layout concerns, and more failure points.

---

## Buck Converter Design Concerns

If a buck converter is used, the design must consider:

- Input voltage range
- Output voltage target
- Output current rating
- Efficiency
- Heat
- Inductor selection
- Catch diode or synchronous design
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

## Protection Goals

Protection should reduce the chance that one fault immediately damages the console.

Protection areas may include:

- Overvoltage protection
- Undervoltage behavior
- Reverse-current blocking
- Backfeed prevention
- Fuse or eFuse protection
- TVS diode protection
- Inrush current control
- Soft-start behavior
- Thermal protection
- Proper grounding
- Proper wire size
- Proper connector ratings

Protection does not make the board impossible to damage. It is layered risk reduction.

---

## Power Conditioning Goals

Power conditioning should help keep the output stable and clean.

Power conditioning may include:

- Bulk capacitance
- Ceramic capacitors
- Ripple reduction
- Noise filtering
- Ferrite beads, if appropriate
- Proper grounding
- Short high-current paths
- Wide copper pours
- Proper capacitor placement
- Test points

Power conditioning should be based on real measurements, not guesswork.

---

## Test Points

PowerOR should include useful test points where practical.

Helpful test points may include:

- USB-C input voltage
- OEM input voltage
- Trigger output voltage
- Buck converter output voltage
- PowerOR final output voltage
- Ground
- Enable signal, if used
- Fault signal, if used
- Source-detect signal, if used

Test points make the board easier to verify before connecting to a console.

---

# Part IV - Power OR-ing

Power OR-ing is the core of the PowerOR project.

The goal is to allow two possible power sources while preventing them from directly fighting each other.

The two sources are:

- OEM PSU
- USB-C PD

---

## Basic OR-ing Concept

The basic concept is:

<pre>
OEM PSU Input
      \
       \
        +---- Power OR-ing ---- PS2 Console Input
       /
      /
USB-C PD Input
</pre>

The console should be able to receive power from either source.

The two sources should not be directly tied together.

---

## OEM PSU Path

The OEM PSU path should remain the preferred/default power path.

Goals for the OEM path:

- Preserve the original power option
- Keep the console compatible with the OEM power supply
- Give OEM power priority when connected
- Avoid unnecessary voltage drop
- Avoid backfeeding into USB-C PD
- Support safe testing
- Maintain predictable behavior

The OEM power supply is the known original power source for the console.

---

## USB-C PD Path

The USB-C PD path should act as an optional alternate input.

Goals for the USB-C PD path:

- Provide a modern alternate power input
- Support selected lower-power PS2 Slim builds
- Avoid backfeeding into the OEM PSU path
- Avoid unsafe voltage at the console
- Support proper testing
- Remain optional, not mandatory

USB-C PD should not be treated as a universal replacement for the OEM PSU.

---

## OEM Priority Behavior

The intended source behavior is:

| OEM PSU | USB-C PD | Desired Behavior |
|---|---|---|
| Connected | Not connected | Console runs from OEM PSU |
| Not connected | Connected | Console runs from USB-C PD |
| Connected | Connected | Console prefers OEM PSU |
| Removed | Connected | USB-C PD may continue powering the console if switchover is stable |
| Connected | Removed | OEM PSU powers the console normally |
| Not connected | Not connected | Console is off |

This behavior must be tested.

---

## Backfeed Prevention

Backfeeding must be prevented.

Backfeeding could happen if:

- OEM PSU feeds into the USB-C PD trigger board
- USB-C PD feeds into the OEM input
- One source powers a section that should be off
- A disconnected input still shows voltage
- Capacitors discharge into the wrong side of the circuit

Backfeed prevention is one of the main reasons this board exists.

---

## OR-ing Methods

Possible OR-ing methods include:

- Schottky diode OR-ing
- MOSFET ideal diode OR-ing
- Power mux IC
- eFuse/load switch arrangement
- Controlled source selection
- Manual source selection for early testing

Each method has tradeoffs.

The final method should be chosen based on voltage drop, heat, current handling, backfeed prevention, source priority, size, cost, and testing results.

---

# Part V - PCB Layout Direction

The PCB layout must support the current, heat, and testing requirements of the design.

A good schematic is not enough if the PCB layout is weak.

---

## Layout Goals

The PCB layout should focus on:

- Short high-current paths
- Wide traces or copper pours
- Strong ground return
- Proper capacitor placement
- Proper buck converter layout, if used
- Clear input/output labeling
- Useful test points
- Mechanical connector support
- Thermal copper where needed
- Safe spacing
- Easy inspection
- Easy assembly

The board should be compact, but not at the expense of safety or reliability.

---

## High-Current Path

The main power path should be treated as a high-current path.

High-current layout concerns include:

- Trace width
- Copper thickness
- Copper pour area
- Via count, if changing layers
- Connector current rating
- Wire pad size
- Heat
- Voltage drop
- Mechanical strain

Thin traces should be avoided in the main power path.

---

## Ground Return

The ground path matters as much as the positive voltage path.

A weak ground return can cause:

- Voltage drop
- Noise
- Controller issues
- Audio/video instability
- Unreliable internal mods
- Strange reset behavior
- Poor measurements

The board should use a strong ground return and avoid long thin ground paths.

---

## Thermal Layout

Power parts may need extra copper area to spread heat.

Parts to watch include:

- Buck converter IC
- Inductor
- Diode
- MOSFETs
- Power mux
- eFuse
- USB-C connector
- Output connector
- High-current traces

Thermal performance should be tested with the board installed in the intended environment.

---

## Labeling

The board should be clearly labeled.

Useful labels include:

- USB-C input
- OEM input
- Output to console
- Ground
- Voltage test points
- Source detect, if used
- Enable, if used
- Fault, if used
- Board revision
- Warning or polarity markings

Clear labeling reduces mistakes during testing and installation.

---

## Board Revision Tracking

Each prototype should have a clear revision number.

Example revision naming:

- PowerOR v0.1
- PowerOR v0.2
- PowerOR v0.3
- PowerOR Beta
- PowerOR Release Candidate

Each revision should document:

- What changed
- What worked
- What failed
- What needs testing
- Whether it is safe for bench testing only
- Whether it is safe for console testing

No prototype should be treated as final until it has passed testing.

---

## Public vs Private Board Files

This repository is for public documentation and design discussion.

The public repo may include:

- Project notes
- Design goals
- Testing notes
- Public diagrams
- Fitment photos
- Prototype discussion
- Non-production examples

Final production files are not planned for public release at this time.

This may include:

- Final Gerbers
- Complete KiCad source
- Pick-and-place files
- Assembly files
- Final production BOM
- Manufacturing package

The goal is to document the project while protecting the final assembled kit design.

---

# Part VI - Mechanical Fitment

PowerOR must fit inside the intended console build.

Electrical design and mechanical design need to be developed together.

---

## Fitment Goals

Fitment goals include:

- Fit inside selected PS2 Slim shells
- Avoid interference with the motherboard
- Avoid interference with the RF shield
- Avoid interference with other mods
- Allow safe wire routing
- Keep the USB-C port accessible
- Keep heat away from sensitive areas
- Avoid stress on solder joints
- Allow reasonable installation repeatability

The board should be designed around real console space, not just schematic convenience.

---

## Ultra Slim Builds

PowerOR may be especially useful for Ultra Slim style builds.

These builds may have:

- Optical drive removed
- Lower current draw
- More internal space in some areas
- Custom shell modifications
- Need for compact power routing
- Desire for modern external power options

The SCPH-790xx boards may be a good testing platform because they are lower-power and commonly used in compact builds.

---

## Wire Routing

Wire routing matters for both safety and reliability.

Wire routing should consider:

- Current capacity
- Wire length
- Ground return
- Strain relief
- Heat
- Avoiding sharp edges
- Avoiding moving parts
- Avoiding RF shield shorts
- Avoiding sensitive signal lines
- Keeping power wiring mechanically secure

The install should not rely on fragile wires or unsupported solder joints.

---

## Mounting Options

Possible mounting options include:

- Adhesive mounting
- Screws
- Standoffs
- Brackets
- RF shield mounting
- 3D printed support
- Laser-cut bracket
- Shell-mounted support
- Combined USB-C port bracket and board mount

The mounting method should be strong enough for normal use.

The USB-C port especially needs mechanical support.

---

# Part VII - Release and Kit Planning

The long-term goal is to develop PowerOR into an assembled kit.

The kit should not be released until the design has been properly tested.

---

## Release Goals

A future PowerOR kit should ideally include:

- Assembled PowerOR board
- Clearly marked input/output points
- Recommended wiring
- Installation notes
- Compatibility notes
- Charger recommendations
- Cable recommendations
- Testing instructions
- Safety warnings

The kit should be aimed at selected lower-power PS2 Slim builds only unless later testing proves a wider use case.

---

## Prototype Stage

The prototype stage should focus on:

- Testing basic circuit behavior
- Verifying voltage
- Testing trigger boards
- Testing chargers and cables
- Testing OR-ing behavior
- Checking for backfeed
- Checking heat
- Checking voltage drop
- Testing dummy loads
- Revising the layout

The console should not be the first test load.

---

## Beta Stage

A beta stage may include a small number of assembled boards tested in controlled builds.

Beta testing should document:

- Console model
- Board revision
- Installed mods
- Charger used
- Cable used
- Current draw
- Runtime
- Heat
- Any failures
- Any unexpected behavior

Beta boards should still be treated as experimental.

---

## Final Kit Stage

A final kit should only be considered after:

- Bench testing is complete
- Dummy-load testing is complete
- Console testing is complete
- Thermal testing is complete
- Source switching is tested
- OEM priority is verified
- Backfeed prevention is verified
- Documentation is ready
- Installation risks are understood
- Compatibility limits are clearly stated

The kit should not be advertised as universal.

---

## Kit Sales Direction

The long-term goal may be to offer assembled kits through:

- FBD website
- Etsy
- eBay

The public documentation can remain available while final production files remain private.

The purpose of the public repo is transparency, feedback, and documentation, not cloning the final sellable kit.

---

## Practical Board Design Rule

For PowerOR, the practical board design rule is:

The board should be designed around testing first and release second.

That means:

- Include test points.
- Label the board clearly.
- Avoid underrated parts.
- Avoid thin high-current traces.
- Avoid weak USB-C mounting.
- Avoid unsupported assumptions.
- Test before connecting to a console.
- Keep the intended console scope narrow.
- Do not release a kit until the design is proven.

---

## Project Position

The PowerOR board design is still experimental.

This board is not simply a USB-C connector swap.

It is a dual-input power system that must handle USB-C PD behavior, OEM PSU priority, protection, conditioning, OR-ing, fitment, and testing.

Until the board has been tested and revised, it should not be treated as a finished product.

---

## Disclaimer

This document is part of an experimental hardware project.

Incorrect board design, poor layout, unsafe power switching, insufficient current handling, excessive heat, wrong voltage, or poor installation can damage a PlayStation 2 console.

Use this information at your own risk.
