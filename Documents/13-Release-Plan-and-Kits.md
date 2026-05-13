# Release Plan and Kits

This document covers the release plan and possible kit direction for the PowerOR project.

PowerOR is an experimental power OR-ing project for selected PlayStation 2 Slim consoles. The goal is to explore USB-C PD as an optional alternate power source while keeping the original OEM PS2 power supply as the preferred/default input.

The long-term goal may be to offer PowerOR as an assembled kit, but the project should not move to kit release until the design has been properly tested, revised, and documented.

---

## Release Goal

The goal is to eventually turn PowerOR into a controlled, assembled kit for specific lower-power PS2 Slim builds.

The kit should be designed around:

- OEM PSU priority
- Optional USB-C PD input
- Safe power OR-ing
- Backfeed prevention
- Proper current handling
- Clear installation instructions
- Clear compatibility limits
- Clear charger and cable requirements
- Clear testing instructions
- Honest safety warnings

PowerOR should not be released as a universal PS2 USB-C power mod.

---

## What the Kit Is Intended to Be

A future PowerOR kit may be:

- An assembled power OR-ing board
- A dual-input power solution for selected PS2 Slim builds
- A way to keep the OEM PSU while adding optional USB-C PD
- A tested board for lower-power builds
- A documented install option for experienced modders
- A cleaner alternative to directly wiring a USB-C PD trigger board into the console

The kit should be aimed at a narrow, tested use case.

---

## What the Kit Is Not Intended to Be

A future PowerOR kit should not be advertised as:

- A universal PS2 power solution
- A guaranteed safe mod for every PS2 Slim
- A power solution for every internal mod setup
- A high-current replacement for the OEM PSU
- A solution for heavily modified consoles without additional testing
- A beginner plug-and-play mod
- A replacement for proper testing
- A replacement for understanding the console’s current draw

The kit should not be treated as safe outside the tested scope.

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

## Intended Build Type

PowerOR is currently intended for lighter PS2 Slim builds.

Possible intended use cases include:

- Lightly modified PS2 Slim consoles
- Ultra Slim style builds
- Builds without the optical drive
- Builds with lower-current internal mods
- Builds where the OEM PSU input is retained
- Builds where USB-C PD is optional

The design should be tested and documented around this intended use case first.

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

A future kit should clearly state these limits.

---

## Development Stages

The release path should be broken into clear stages:

1. Concept stage
2. Prototype stage
3. Bench testing stage
4. Dummy-load testing stage
5. Console testing stage
6. Revision stage
7. Controlled beta stage
8. Release candidate stage
9. Small kit release
10. Post-release feedback and revision

The project should only move forward when the previous stage has been properly tested and documented.

---

## Stage 1 - Concept Stage

The concept stage defines the project goals.

This stage includes:

- Defining the purpose of PowerOR
- Defining the target consoles
- Defining unsupported consoles
- Defining light-build vs heavy-build limits
- Identifying USB-C PD risks
- Identifying power OR-ing requirements
- Deciding that OEM PSU priority is required
- Deciding what information can be public
- Deciding what production files remain private

The concept stage should clearly explain what the project is and what it is not.

---

## Stage 2 - Prototype Stage

The prototype stage is where early hardware is built and tested.

Prototype goals include:

- Testing basic USB-C PD input behavior
- Testing purchased trigger boards
- Testing charger and cable behavior
- Testing power OR-ing methods
- Testing backfeed prevention
- Testing voltage drop
- Testing heat
- Testing board fitment
- Identifying layout problems
- Finding what needs to change

Prototype boards should not be treated as finished products.

---

## Stage 3 - Bench Testing Stage

Bench testing should happen before connecting the board to a console.

Bench testing includes:

- Visual inspection
- Short checks
- Continuity checks
- No-load voltage testing
- OEM PSU input testing
- USB-C PD input testing
- Output voltage testing
- Source priority testing
- Backfeed testing
- Basic heat checks

Bench testing helps catch problems before a console is at risk.

---

## Stage 4 - Dummy-Load Testing Stage

Dummy-load testing should happen before console testing.

Dummy-load testing includes:

- Light-load testing
- 1A load testing
- 2A load testing
- 3A load testing
- Extended runtime load testing
- Heat testing under load
- Voltage drop testing
- Source switching under load
- Backfeed checks under load
- Ripple testing if an oscilloscope is available

The console should not be the first test load.

---

## Stage 5 - Console Testing Stage

Console testing should only happen after bench and dummy-load tests pass.

Console testing should include:

- OEM PSU only
- USB-C PD only
- Both sources connected
- Repeated startup testing
- Idle testing
- Gameplay testing
- Controller testing
- Memory card testing
- Internal mod testing, if installed
- Source switching testing, if safe
- Long runtime testing
- Heat checks
- Voltage checks at the console input

One successful power-on test is not enough.

---

## Stage 6 - Revision Stage

After testing, the design may need revisions.

Possible revision reasons include:

- Voltage drop too high
- Heat too high
- Poor fitment
- USB-C port too weak
- Backfeed issue found
- Source priority not reliable
- Charger compatibility issue
- Cable sensitivity issue
- Board too difficult to install
- Test points missing
- Labels unclear
- Trace width too small
- Protection needs improvement

Each revision should be documented.

---

## Stage 7 - Controlled Beta Stage

A beta stage may be useful before a public kit release.

Beta boards should only go to controlled testers who understand that the design is still experimental.

Beta testing should require documentation of:

- Console model
- Console board revision
- PowerOR board revision
- Installed mods
- Charger used
- Cable used
- Runtime
- Heat
- Voltage readings
- Fitment notes
- Problems found
- Failure reports
- Photos if possible

Beta testing should not be treated as a full public release.

---

## Stage 8 - Release Candidate Stage

A release candidate should be the version believed to be close to final.

Before a board becomes a release candidate, it should have:

- Passed bench testing
- Passed dummy-load testing
- Passed console testing
- Passed thermal testing
- Passed source priority testing
- Passed backfeed testing
- Passed fitment testing
- Clear install notes
- Clear compatibility notes
- Clear charger requirements
- Clear cable requirements
- Clear safety warnings

A release candidate should still be reviewed carefully before being sold as a kit.

---

## Stage 9 - Small Kit Release

If testing is successful, the first release should be small.

A small kit release allows real-world feedback without overcommitting.

A first kit release should include:

- Assembled PowerOR board
- Basic install guide
- Wiring notes
- Compatibility notes
- Unsupported build warnings
- Charger recommendations
- Cable recommendations
- Testing checklist
- Safety disclaimer

The first release should be treated as a careful rollout, not a mass release.

---

## Stage 10 - Post-Release Feedback

After release, feedback should be collected and documented.

Useful feedback includes:

- Install difficulty
- Fitment issues
- Charger compatibility
- Cable compatibility
- Heat observations
- Runtime stability
- Console model results
- Board revision results
- User mistakes
- Failure reports
- Suggested improvements

Feedback should guide future revisions.

---

## Possible Kit Contents

A future PowerOR kit may include:

- Assembled PowerOR board
- USB-C port or USB-C input board, if separate
- Recommended wiring
- Mounting hardware, if applicable
- Insulation material, if applicable
- Installation notes
- Testing checklist
- Compatibility sheet
- Safety warning sheet

The exact kit contents should depend on the final tested design.

---

## Possible Kit Add-Ons

Possible optional add-ons may include:

- Recommended USB-C PD charger
- Recommended USB-C cable
- Pre-cut wire set
- Mounting bracket
- Shell cutting template
- Test lead adapter
- Dummy-load testing accessory
- Printed install card

Add-ons should only be included if they make the install safer or easier.

---

## What May Not Be Included

A future kit may not include:

- Final Gerber files
- Full KiCad source files
- Pick-and-place files
- Assembly files
- Manufacturing package
- Final production BOM
- Tools required for install
- A PlayStation 2 console
- A guarantee that every charger will work
- A guarantee that every PS2 Slim build is compatible

The public documentation can remain available while the final production files remain private.

---

## Public Documentation Scope

This repository may include:

- Project overview
- Design goals
- Safety notes
- USB-C PD research
- Charger and cable notes
- Trigger board discussion
- Power signal quality discussion
- Power conditioning discussion
- Power OR-ing discussion
- Fitment planning
- Testing plans
- Public test results
- Public photos
- Release planning

The goal is to keep the project transparent while protecting the final sellable kit design.

---

## Private Production File Scope

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

This allows the project to be documented publicly while still allowing assembled kits to be sold through FBD channels.

---

## Sales Direction

If the project reaches release, kits may be sold through:

- FBD website
- Etsy
- eBay

The sales listing should clearly state:

- The kit is for selected PS2 Slim builds
- The kit is not universal
- The kit is not intended for heavy builds
- The OEM PSU remains the preferred/default source
- USB-C PD requires a compatible charger and cable
- Installation requires soldering and testing
- Incorrect installation can damage the console

The listing should avoid overstating the safety or compatibility of the kit.

---

## Website Documentation

The FBD website may be used for:

- Product page
- Install guide
- Compatibility chart
- Testing results
- Charger recommendations
- Cable recommendations
- FAQ
- Revision history
- Safety notes
- Support notes

GitHub can remain the technical project documentation, while the website can become the customer-facing version.

---

## Etsy and eBay Listing Notes

Etsy and eBay listings should be clear and careful.

The listing should avoid making the kit sound universal or risk-free.

Good listing points may include:

- Assembled PowerOR board
- Designed for selected PS2 Slim builds
- OEM PSU priority
- Optional USB-C PD input
- Experimental development background
- Requires proper installation
- Requires compatible charger and cable
- Not for heavily modified high-current builds
- Not for RetroGEM or internal IDE builds unless specifically tested

The listing should be honest about limitations.

---

## Compatibility Chart

A compatibility chart should be created before release.

Suggested chart:

| Console Model | Board Revision | Fitment | Power Testing | Notes |
|---|---|---|---|---|
| SCPH-750xx | TBD | Not tested | Not tested |  |
| SCPH-770xx | TBD | Not tested | Not tested |  |
| SCPH-790xx | TBD | Not tested | Not tested |  |
| SCPH-900xx | Out of scope | Not supported | Not supported | Internal PSU |

Fitment and power testing should be tracked separately.

A console may physically fit but still fail power testing.

---

## Charger Compatibility Chart

A charger compatibility chart should also be created.

Suggested chart:

| Charger | Rated Output | Tested Voltage | Result | Notes |
|---|---|---:|---|---|
| TBD | TBD | TBD | Not tested |  |

The charger chart should include the exact charger model when possible.

Not all USB-C PD chargers behave the same.

---

## Cable Compatibility Chart

A cable compatibility chart may also be useful.

Suggested chart:

| Cable | Length | Rated Current | E-Marked | Result | Notes |
|---|---:|---:|---|---|---|
| TBD | TBD | TBD | TBD | Not tested |  |

Changing the cable can change the test results.

---

## Revision History

Each PowerOR board revision should be tracked.

Suggested revision history table:

| Revision | Status | Notes |
|---|---|---|
| v0.1 | Prototype | Initial concept board |
| v0.2 | Prototype | Changes after early testing |
| v0.3 | Prototype | Fitment and protection updates |
| Beta | Future | Controlled test batch |
| Release Candidate | Future | Final review before kit |
| Release | Future | Public assembled kit |

Revision history helps users understand the maturity of the design.

---

## Release Readiness Checklist

Before a kit release, the following should be complete:

| Requirement | Status | Notes |
|---|---|---|
| Target console range defined | Not complete |  |
| Unsupported consoles defined | Not complete |  |
| Heavy-build warning written | Not complete |  |
| Board revision selected | Not complete |  |
| Bench testing completed | Not complete |  |
| Dummy-load testing completed | Not complete |  |
| Console testing completed | Not complete |  |
| Thermal testing completed | Not complete |  |
| Backfeed testing completed | Not complete |  |
| OEM priority tested | Not complete |  |
| USB-C PD input tested | Not complete |  |
| Charger requirements written | Not complete |  |
| Cable requirements written | Not complete |  |
| Fitment guide written | Not complete |  |
| Installation guide written | Not complete |  |
| Safety warning written | Not complete |  |
| Support process planned | Not complete |  |

The kit should not be released until the major release requirements are complete.

---

## Support Planning

If kits are sold, support should be considered.

Support topics may include:

- Charger compatibility
- Cable compatibility
- Wrong voltage troubleshooting
- No power
- Console resets
- USB-C not negotiating
- OEM PSU not taking priority
- Heat concerns
- Fitment questions
- Install mistakes
- Damaged pads
- Unsupported console models

Good documentation reduces support problems.

---

## Warranty and Risk Notes

Because this project modifies the console power system, the risk needs to be clearly explained.

A future kit should make clear:

- Installation is at the user’s risk.
- Incorrect installation can damage the console.
- Incorrect charger selection can cause problems.
- Incorrect cable selection can cause problems.
- Unsupported builds are not covered.
- Heavily modified consoles may exceed the intended power range.
- The kit does not make USB-C PD universally safe for all PS2 consoles.

The wording should be honest and direct.

---

## Practical Release Rule

For PowerOR, the practical release rule is:

Do not release the kit until the intended use case has been tested and documented.

That means:

- Do not release based on one successful power-on test.
- Do not release before dummy-load testing.
- Do not release before heat testing.
- Do not release before backfeed testing.
- Do not release before fitment testing.
- Do not release before charger and cable requirements are written.
- Do not advertise the kit as universal.
- Do not target heavy builds unless they are tested separately.

The kit should be released only when the design is ready for the stated scope.

---

## Project Position

PowerOR may become an assembled kit in the future, but the project is still experimental until testing proves the design reliable for its intended use case.

The public repository exists to document the project, explain the risks, collect testing information, and provide transparency.

The final kit design may remain protected while still allowing the project to be discussed and documented publicly.

---

## Disclaimer

This document is part of an experimental hardware project.

PowerOR modifies the power system of a PlayStation 2 console. Incorrect installation, wrong charger selection, poor cable selection, insufficient current, unsafe source switching, excessive heat, or unsupported console use can damage a console.

Use this information at your own risk.
