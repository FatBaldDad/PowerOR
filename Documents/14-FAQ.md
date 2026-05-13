# FAQ

This document answers common questions about the PowerOR project.

PowerOR is an experimental power OR-ing project for selected PlayStation 2 Slim consoles. The goal is to explore USB-C PD as an optional alternate power source while keeping the original OEM PS2 power supply as the preferred/default input.

---

## Is PowerOR a finished product?

No.

PowerOR is currently an experimental hardware project.

It should not be treated as a finished product, a proven install kit, or a universal USB-C power mod for every PlayStation 2 console.

---

## What is PowerOR?

PowerOR is a prototype power OR-ing board for selected PS2 Slim builds.

The goal is to allow two possible power sources:

- Original OEM PS2 Slim power supply
- Optional USB-C PD power input

The OEM power supply is intended to remain the preferred/default source when connected.

---

## What does power OR-ing mean?

Power OR-ing means allowing more than one power source to feed one load while preventing those sources from directly fighting each other.

For PowerOR, the load is the PS2 Slim console.

The two sources are:

- OEM PSU
- USB-C PD

The goal is to let either source power the console while preventing unsafe backfeeding between them.

---

## Why not just wire a USB-C PD trigger board directly to the PS2?

A direct USB-C PD trigger board install may power on a console, but that does not make it safe.

A direct setup may not include:

- OEM PSU priority
- Backfeed prevention
- Reverse-current protection
- Power conditioning
- Overvoltage protection
- Source switching control
- Proper current handling
- Proper test points
- Fitment planning
- Thermal testing

PowerOR exists because the full power path should be treated as a system, not just a connector swap.

---

## Is USB-C PD safe for the PS2?

USB-C PD is not automatically safe for the PS2.

A USB-C PD setup can be safe or unsafe depending on the design, charger, cable, trigger board, wiring, voltage stability, current capacity, protection, and testing.

PowerOR does not claim that USB-C PD is always safe.

PowerOR also does not claim that USB-C PD is impossible to use safely.

The position of this project is simple:

USB-C PD may be useful for selected PS2 Slim builds, but it needs to be designed, tested, and documented properly.

---

## Why is USB-C PD controversial for PS2 mods?

USB-C PD power mods are controversial because poor implementations can damage consoles or cause unreliable behavior.

Common concerns include:

- Wrong voltage
- Cheap trigger boards
- Poor USB-C cables
- Insufficient current
- Voltage sag
- Startup dips
- Ripple and noise
- Heat
- Backfeeding
- Poor grounding
- Weak wiring
- Lack of testing

A console powering on does not prove the power system is safe.

---

## What consoles is PowerOR intended for?

PowerOR is currently focused on selected PS2 Slim consoles.

Current target range:

- SCPH-750xx
- SCPH-770xx
- SCPH-790xx

The SCPH-790xx series is especially interesting because it is commonly used in Ultra Slim style builds and generally has lower power demand than earlier Slim models.

---

## What consoles are out of scope?

PowerOR is not currently targeting:

- Any consoles prior to SCPH-750xx
- SCPH-900xx

Earlier consoles may have different power requirements, board layouts, current draw, and fitment concerns.

The SCPH-900xx series uses an internal power supply and is generally sufficient as-is for this type of project.

---

## Can PowerOR be used on a PS2 Fat?

No.

PowerOR is not currently intended for PS2 Fat consoles.

PS2 Fat consoles use a different power design and are outside the current scope of this project.

---

## Can PowerOR be used on SCPH-700xx Slim consoles?

Not currently.

Although SCPH-700xx consoles are Slim models, they are outside the current scope of this project.

PowerOR is currently focused on SCPH-750xx, SCPH-770xx, and SCPH-790xx consoles.

---

## Can PowerOR be used on SCPH-900xx Slim consoles?

Not currently.

The SCPH-900xx series uses an internal power supply and is outside the current scope of this project.

---

## Is PowerOR intended for heavily modified consoles?

No.

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

Those builds may require a stronger power design with higher current capacity, better thermal handling, and additional protection.

---

## Can PowerOR be used with RetroGEM?

Not currently.

RetroGEM builds may require more power and more careful power planning.

PowerOR is currently aimed at lighter PS2 Slim builds, not heavily modified high-current builds.

---

## Can PowerOR be used with an internal IDE interface?

Not currently.

Internal IDE interfaces and internal hard drive setups may increase power demand and are outside the current intended scope.

---

## Can PowerOR be used with an internal SSD or HDD?

Not currently recommended.

Large internal storage setups may require more current than the current PowerOR target use case.

Any build with internal SSD or HDD power should be tested separately with a more robust power budget.

---

## Can PowerOR be used with BlueRetro?

Possibly, depending on the full build power draw.

BlueRetro by itself may not be a heavy load, but the total system current matters.

The full build needs to be tested, including:

- Console model
- Board revision
- Installed mods
- Charger
- Cable
- PowerOR revision
- Runtime behavior
- Heat
- Voltage stability

---

## Can PowerOR be used with ElectronAnalog or other HDMI adapters?

Possibly, depending on the power draw and the full build.

PowerOR is aimed at lighter builds. If the HDMI adapter and other installed mods keep the total current within the tested range, it may be possible.

However, it should not be assumed safe without testing.

---

## Why keep the OEM power supply?

The OEM PS2 Slim power supply is the known original power source for the console.

Keeping the OEM PSU has several advantages:

- It keeps a known-good power option available.
- It allows USB-C PD to remain optional.
- It gives a fallback during testing.
- It reduces dependence on charger and cable behavior.
- It supports OEM priority behavior.

PowerOR is not designed to remove the OEM power option completely.

---

## What does OEM PSU priority mean?

OEM PSU priority means the original PS2 power supply should be the preferred source when it is connected.

The intended behavior is:

| OEM PSU | USB-C PD | Desired Behavior |
|---|---|---|
| Connected | Not connected | Console runs from OEM PSU |
| Not connected | Connected | Console runs from USB-C PD |
| Connected | Connected | Console prefers OEM PSU |
| Removed | Connected | USB-C PD may continue if switchover is stable |
| Connected | Removed | OEM PSU powers the console normally |
| Not connected | Not connected | Console is off |

This behavior must be tested and verified.

---

## Will PowerOR allow seamless switching between OEM PSU and USB-C PD?

Maybe, but seamless switching is not the first priority.

Safe behavior is more important than seamless behavior.

The first goals are:

- No backfeeding
- No overvoltage
- No dangerous spikes
- No excessive heat
- Predictable source behavior
- Stable operation under normal use

A console reset during early source switching tests may be acceptable if the power path remains safe.

A hidden backfeed, voltage spike, or overheating condition is not acceptable.

---

## What voltage does the PS2 Slim use?

The PS2 Slim OEM adapter is commonly associated with 8.5V DC.

USB-C PD commonly offers a 9V profile.

That makes 9V interesting for this project, but it does not automatically make it safe.

The voltage must be tested at:

- USB-C trigger output
- PowerOR input
- PowerOR output
- Console input
- Under real load

The voltage at the console input is the most important measurement.

---

## Is 9V safe for the PS2 Slim?

9V may be close to the expected PS2 Slim input voltage, but it should not be assumed safe without testing.

The project needs to verify:

- No-load voltage
- Loaded voltage
- Startup behavior
- Voltage sag
- Overshoot
- Ripple
- Heat
- Long-term runtime behavior

The goal is not just “about 9V.”

The goal is stable, console-safe power.

---

## Why target 9V at 3A?

9V at 3A is a practical early USB-C PD target.

It equals about 27W.

This may be useful for selected lower-power PS2 Slim builds, especially builds without the optical drive and without high-current internal mods.

However, 9V at 3A should not be treated as enough for every console or every build.

It must be tested.

---

## Why not use 20V and buck down?

A higher USB-C PD voltage, such as 20V, can provide more power with lower current on the USB-C input side.

That may be useful for higher-power designs.

However, it adds complexity.

A 20V input design would require a proper buck converter and careful testing for:

- Output voltage accuracy
- Current capacity
- Heat
- Efficiency
- Ripple
- Load transients
- Layout
- Protection
- Failure behavior

Never connect 20V directly to the console.

---

## Does PowerOR need a buck converter?

It depends on the design path.

If PowerOR requests 9V directly from USB-C PD, a buck converter may not be needed.

If PowerOR requests 12V, 15V, or 20V, then a buck converter is required to step the voltage down before the console receives power.

The final direction should be based on testing.

---

## What is a USB-C PD trigger board?

A USB-C PD trigger board is a small circuit that communicates with a USB-C PD charger and requests a specific voltage profile.

For example:

- 9V
- 12V
- 15V
- 20V

The charger must support the requested profile.

The trigger board output must be measured before connecting it to PowerOR or a console.

---

## Should PowerOR use a purchased trigger board or a custom trigger circuit?

Early testing may use purchased trigger boards because they are quick and useful for experiments.

A custom trigger circuit may be better for a future kit because it can provide:

- Better fitment
- Better documentation
- Known components
- Better protection integration
- Better test points
- Cleaner assembly

The project may start with purchased trigger boards and move toward a custom design later if testing supports it.

---

## Are cheap USB-C PD trigger boards safe?

Not automatically.

Cheap trigger boards may have:

- Unknown component quality
- Weak USB-C connectors
- Thin traces
- Poor soldering
- Poor documentation
- Unknown current handling
- No meaningful protection
- Inconsistent behavior

Every trigger board should be tested before use.

---

## What charger should be used?

For early testing, a known-quality USB-C PD charger that supports at least 9V at 3A is a good starting point.

The charger should be documented and tested.

Important charger details include:

- Brand/model
- Rated wattage
- Supported PD profiles
- 9V current rating
- Single-port behavior
- Multi-port behavior
- Heat
- Stability under load

Not all USB-C PD chargers behave the same.

---

## Can any USB-C charger be used?

No.

A charger must support the voltage and current required by the PowerOR design.

A phone charger may not be enough.

A charger advertised as 65W or 100W may still have limits at 9V.

Always check the actual PD output profiles.

---

## Can a USB-A charger be used?

No, not for normal USB-C PD operation.

PowerOR is intended around a USB-C PD setup:

- USB-C PD charger
- USB-C to USB-C cable
- USB-C PD trigger/input board

USB-A to USB-C power paths should not be used unless specifically testing a separate behavior.

---

## Does the USB-C cable matter?

Yes.

The cable is part of the power system.

A poor cable can cause:

- Voltage drop
- Heat
- Charger shutdown
- Failed negotiation
- Random console resets
- Unstable behavior

Use a known-good USB-C to USB-C cable with the proper current rating.

---

## Is a 5A USB-C cable required?

Not for every test.

For a 9V at 3A target, a good 3A-rated USB-C to USB-C cable may be enough for testing.

For higher-power designs, especially anything involving 20V at higher current, a proper e-marked 5A cable may be required.

Do not assume all USB-C cables are equal.

---

## What should be tested before connecting to a console?

Before connecting PowerOR to a PS2, test:

- Visual inspection
- Short checks
- USB-C trigger output voltage
- OEM PSU voltage
- PowerOR output voltage
- Dummy-load behavior
- Voltage under load
- Heat
- Backfeed behavior
- Source priority
- Source switching
- Ripple and noise, if possible

The console should not be the first test load.

---

## What is dummy-load testing?

Dummy-load testing means testing the power board with a controlled load instead of a console.

This helps reduce the risk of damaging a console during early testing.

Suggested load testing may include:

- Light load
- 1A load
- 2A load
- 3A load
- Extended runtime load

During dummy-load testing, check voltage, heat, ripple, and stability.

---

## Why is oscilloscope testing useful?

A multimeter shows average voltage.

An oscilloscope can show fast events that a multimeter may miss, such as:

- Startup dips
- Voltage spikes
- Ripple
- Switching noise
- Load transient response
- Source switching events
- USB-C PD negotiation behavior

Oscilloscope testing is strongly recommended where possible.

---

## What is backfeeding?

Backfeeding happens when current flows backward into a power source or circuit section where it should not go.

Examples:

- OEM PSU feeding into the USB-C PD trigger board
- USB-C PD feeding into the OEM input
- One input showing voltage even when disconnected
- A capacitor discharging into the wrong side of the circuit

Backfeeding is one of the main risks PowerOR is designed to avoid.

---

## What is an eFuse?

An eFuse is an electronic fuse IC.

Depending on the part, it may provide features such as:

- Current limiting
- Overvoltage protection
- Undervoltage lockout
- Reverse-current blocking
- Thermal shutdown
- Soft start
- Fault reporting

An eFuse may be useful, but it adds design complexity and must be tested.

---

## What is a TVS diode?

A TVS diode is a transient voltage suppression diode.

It can help clamp short voltage spikes.

A TVS diode is not a complete protection system by itself. It is usually part of a larger protection design.

---

## What is voltage sag?

Voltage sag is when the voltage drops under load.

Voltage sag can cause:

- Failed boot
- Random resets
- Controller instability
- Storage instability
- Audio/video issues
- Charger shutdown

Voltage should be tested under real load, not only with no load.

---

## What is ripple?

Ripple is the repeating AC variation that rides on top of the DC output voltage.

Too much ripple can cause instability or noise problems.

Ripple should be checked with an oscilloscope when possible.

---

## What is inrush current?

Inrush current is the current drawn when power is first applied and capacitors charge.

Too much inrush can cause:

- Charger shutdown
- Trigger board reset
- Voltage dip
- Stress on parts
- Source switching problems

Inrush behavior should be tested during startup.

---

## What are the biggest risks with PowerOR?

The biggest risks include:

- Wrong voltage
- Insufficient current
- Backfeeding
- Voltage sag
- Voltage spikes
- Excessive ripple
- Heat
- Poor wiring
- Poor USB-C port mounting
- Poor charger/cable selection
- Installing in unsupported heavy builds
- Assuming one successful boot means the design is safe

These risks are why the project is still experimental.

---

## Will Gerbers be released?

Final production Gerbers are not currently planned for public release.

This repository is intended for public documentation, testing notes, design discussion, and transparency.

Final production files may remain private because the long-term goal is to offer assembled kits.

---

## Will KiCad source files be released?

Final production KiCad source files are not currently planned for public release.

The public repo may include documentation, diagrams, notes, testing results, and prototype discussion, but not necessarily the final manufacturing package.

---

## What files are not planned for public release?

Final production files are not planned for public release at this time.

This may include:

- Final Gerbers
- Complete KiCad source
- Pick-and-place files
- Assembly files
- Final production BOM
- Manufacturing package
- Final panelization files
- Final test fixture files
- Final kit templates, if considered private

---

## Why keep final production files private?

The goal is to document the project publicly while still allowing assembled kits to be sold through FBD channels.

The public documentation can explain the project, risks, testing, and design direction without giving away the final sellable kit design.

---

## Will assembled kits be available?

Possibly.

The long-term goal may be to offer assembled PowerOR kits through:

- FBD website
- Etsy
- eBay

However, kits should not be released until the design has been properly tested and documented.

---

## Will this be a beginner-friendly kit?

Probably not at first.

PowerOR modifies the console power system and requires careful installation and testing.

A future kit may be aimed at experienced modders who understand soldering, power testing, charger selection, and the risks of console power modifications.

---

## What might be included in a future kit?

A future kit may include:

- Assembled PowerOR board
- USB-C port or input board, if separate
- Recommended wiring
- Mounting hardware, if applicable
- Insulation material, if applicable
- Installation notes
- Testing checklist
- Compatibility sheet
- Safety warning sheet

The exact kit contents will depend on the final tested design.

---

## Will the kit include a charger and cable?

Maybe as optional add-ons.

A charger and cable may be offered or recommended if testing shows specific models behave reliably.

Charger and cable compatibility should be documented before release.

---

## Will this work with any USB-C PD charger?

No.

The charger must support the required voltage and current profile.

The charger must also behave reliably under load.

PowerOR testing should document which chargers have been tested.

---

## What should a user measure after installation?

After installation, useful checks include:

- USB-C PD input voltage
- OEM input voltage
- PowerOR output voltage
- Voltage at the console input
- Heat under load
- Source priority behavior
- No unsafe backfeed
- Startup behavior
- Long runtime behavior

The exact test process should be included in the install guide before any kit release.

---

## Can PowerOR damage a PS2?

Yes, if designed, installed, tested, or used incorrectly.

Possible damage causes include:

- Wrong voltage
- Overvoltage
- Poor wiring
- Backfeeding
- Short circuit
- Excessive heat
- Unsupported charger
- Unsupported console model
- Unsupported heavy build
- Poor installation

This is why the project is being treated as experimental.

---

## Should PowerOR be installed in a valuable console?

Not during early testing.

Early prototypes should be tested with dummy loads first, then with appropriate test consoles.

Do not install experimental power hardware into a valuable or heavily modified console without proper testing.

---

## Can I use PowerOR without testing?

No.

PowerOR should not be used without testing.

At minimum, testing should include:

- Voltage verification
- Short checks
- Dummy-load testing
- Heat checks
- Backfeed checks
- Console input voltage measurement

Skipping testing increases the risk of damaging the console.

---

## Where should test results be stored?

Suggested folders include:

- Testing/Bench-Testing/
- Testing/Load-Testing/
- Testing/Console-Testing/
- Testing/Oscilloscope-Captures/
- Testing/Results/
- Images/Testing/

Photos and screenshots should be named clearly so they match the test notes.

---

## What is the current project status?

Current status:

**Prototype / Experimental**

PowerOR is not finished, not fully validated, and not ready to be treated as a proven install solution.

---

## What is the main rule for this project?

The main rule is:

Test the power system before trusting the power system.

Do not rely on assumptions, seller claims, or one successful power-on test.

---

## Disclaimer

PowerOR is an experimental hardware project.

It modifies the power system of a PlayStation 2 console.

Incorrect voltage, insufficient current, poor wiring, unsafe power OR-ing, backfeeding, excessive heat, unsupported charger selection, unsupported console use, or poor installation can damage a console.

Use this information at your own risk.
