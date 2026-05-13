# Testing and Validation

This document covers testing and validation for the PowerOR project.

PowerOR is an experimental power OR-ing project for selected PlayStation 2 Slim consoles. The goal is to test whether USB-C PD can be used as an optional alternate power source while keeping the OEM PS2 power supply as the preferred/default input.

Testing is the most important part of this project.

A board should not be considered safe just because it powers on a console.

---

## Testing Goal

The goal of testing is to prove that PowerOR behaves safely and predictably before it is trusted in a console or released as a kit.

Testing should verify:

- Correct voltage
- Sufficient current capacity
- Stable output under load
- Low enough voltage drop
- Acceptable ripple and noise
- Safe startup behavior
- Safe source switching behavior
- OEM PSU priority
- No unsafe backfeeding
- Acceptable heat
- Reliable long-term operation
- Compatibility with selected PS2 Slim builds

The design should move forward based on measured results, not assumptions.

---

## Important Safety Rule

The console should not be the first test load.

Before PowerOR is connected to a PS2, it should be tested with:

- Visual inspection
- Continuity checks
- Short checks
- No-load voltage testing
- Dummy-load testing
- Heat testing
- Source switching tests
- Backfeed checks

Only after those tests pass should console testing begin.

---

## Test Stages

PowerOR testing should be broken into stages.

Suggested stages:

1. Visual inspection
2. Continuity and short testing
3. USB-C PD trigger testing
4. OEM PSU input testing
5. PowerOR no-load testing
6. Dummy-load testing
7. Power OR-ing behavior testing
8. Backfeed testing
9. Thermal testing
10. Ripple and oscilloscope testing
11. Console startup testing
12. Console runtime testing
13. Long-term validation
14. Beta testing, if applicable

Each stage should be documented.

---

## Stage 1 - Visual Inspection

Before applying power, inspect the board.

Check for:

- Solder bridges
- Missing parts
- Incorrect parts
- Wrong component orientation
- Damaged components
- Damaged USB-C port
- Damaged pads
- Poor solder joints
- Loose connectors
- Burn marks
- Debris on the board
- Flux residue near fine-pitch parts
- Exposed copper that could short to the RF shield

Do not power a board that looks questionable.

---

## Stage 2 - Continuity and Short Testing

Before applying power, use a multimeter to check for obvious problems.

Check:

- VBUS to ground
- OEM input to ground
- USB-C input to ground
- PowerOR output to ground
- Output polarity
- Continuity through expected power paths
- No continuity where isolation is expected
- No shorts across input capacitors
- No shorts around the USB-C connector

A short check should be done before every first power-up of a new board revision.

---

## Stage 3 - USB-C PD Trigger Testing

The USB-C PD trigger section should be tested by itself before connecting it to the rest of the system or to a console.

Tests should include:

- Confirm requested voltage
- Confirm charger negotiation
- Confirm no-load voltage
- Confirm voltage under dummy load
- Check behavior with the intended charger
- Check behavior with the intended cable
- Check heat
- Check recovery after unplugging and reconnecting
- Check behavior with more than one charger if possible

The output voltage should always be measured before continuing.

---

## Stage 4 - OEM PSU Input Testing

The OEM PS2 power supply should also be tested.

Tests should include:

- Confirm OEM PSU output voltage
- Confirm polarity
- Check connector condition
- Check voltage under load if possible
- Check for excessive voltage drop
- Check behavior when connected to the PowerOR OEM input
- Check that OEM input does not backfeed into the USB-C PD side

The OEM PSU is the reference power source for this project.

---

## Stage 5 - No-Load PowerOR Testing

After the input sources are checked, test the PowerOR board with no console connected.

No-load tests should include:

- USB-C PD input only
- OEM PSU input only
- Both inputs connected
- Output voltage measurement
- Input voltage measurement
- Check for unexpected voltage on inactive inputs
- Check for heat
- Confirm expected source behavior

No-load testing does not prove the board is ready for a console, but it is an important first step.

---

## Stage 6 - Dummy-Load Testing

Dummy-load testing is required before console testing.

A dummy load allows the board to be tested without risking a console.

Suggested dummy-load levels:

- Light load
- 1A
- 2A
- 3A
- Extended runtime at expected load

For higher-current designs, additional load levels may be needed.

During dummy-load testing, check:

- Output voltage
- Voltage drop
- Heat
- Stability
- Charger behavior
- Cable behavior
- Trigger board behavior
- OR-ing behavior
- Ripple, if an oscilloscope is available

---

## Stage 7 - Power OR-ing Behavior Testing

The OR-ing section is the core of PowerOR.

Testing should confirm that the two sources do not fight each other.

Test conditions:

| OEM PSU | USB-C PD | Expected Behavior |
|---|---|---|
| Connected | Not connected | Output powered by OEM PSU |
| Not connected | Connected | Output powered by USB-C PD |
| Connected | Connected | OEM PSU preferred |
| Removed | Connected | USB-C PD may continue if switchover is stable |
| Connected | Removed | OEM PSU continues normally |
| Not connected | Not connected | Output off |

This behavior must be measured.

Do not assume the circuit behaves correctly just because the schematic looks right.

---

## Stage 8 - Backfeed Testing

Backfeed testing checks whether voltage appears where it should not.

Backfeeding is one of the major risks in a dual-input power system.

Suggested backfeed tests:

| Test | Expected Result | Notes |
|---|---|---|
| OEM only, USB-C disconnected | No unsafe voltage on USB-C input | Measure USB-C side |
| USB-C only, OEM disconnected | No unsafe voltage on OEM input | Measure OEM side |
| Both connected | OEM priority confirmed | Check output behavior |
| OEM removed while USB-C remains | No dangerous spike or dip | Oscilloscope preferred |
| USB-C removed while OEM remains | No dangerous spike or dip | Oscilloscope preferred |
| Dummy load connected | No excessive heat | Check OR-ing parts |

Any unsafe backfeeding needs to be solved before console testing.

---

## Stage 9 - Thermal Testing

Heat testing is required because the board may behave differently inside a closed console shell than it does on the bench.

Check heat at:

- USB-C charger
- USB-C cable ends
- USB-C port
- Trigger board or trigger circuit
- Buck converter IC, if used
- Inductor, if used
- Diode, if used
- MOSFETs
- eFuse or power mux
- OR-ing components
- Input capacitors
- Output capacitors
- Wires
- Connectors
- PCB traces
- Console power input area

Thermal testing should be done:

- At no load
- Under dummy load
- During console startup
- During gameplay
- During long runtime
- With the shell closed, if safe

A board that is only warm on the bench may become too hot inside a console.

---

## Stage 10 - Ripple and Oscilloscope Testing

A multimeter is not enough to fully validate power quality.

An oscilloscope should be used where possible.

Use an oscilloscope to check:

- Startup ramp
- Voltage dips
- Voltage overshoot
- Ripple
- Switching noise
- Load transients
- Source switching behavior
- USB-C PD negotiation behavior
- Charger shutdown or renegotiation events

Suggested folder for captures:

<pre>
Testing/Oscilloscope-Captures/
</pre>

Oscilloscope screenshots should be saved with notes about the charger, cable, load, board revision, and test condition.

---

## Stage 11 - Console Startup Testing

Console testing should only begin after bench and dummy-load testing pass.

Startup testing should include:

- OEM PSU only
- USB-C PD only
- Both sources connected
- Repeated cold starts
- Repeated resets
- Startup with internal mods connected
- Startup with the intended charger and cable
- Voltage measurement at the console input
- Heat check after startup

The console should boot consistently.

One successful boot is not enough.

---

## Stage 12 - Console Runtime Testing

After startup testing, runtime testing should be performed.

Runtime testing should include:

- Main menu idle
- Gameplay
- Controller use
- Memory card access
- Storage access, if applicable
- Internal mod activity
- Long play session
- Power source behavior over time
- Heat checks during and after runtime

The test should look for:

- Random resets
- Audio/video instability
- Controller problems
- Storage problems
- Charger shutdown
- Voltage sag
- Heat buildup
- Strange behavior from internal mods

---

## Stage 13 - Source Switching Testing

Source switching should be tested carefully.

Suggested tests:

| Test | Desired Result | Notes |
|---|---|---|
| OEM connected first, then USB-C | OEM remains preferred | Check for dip/spike |
| USB-C connected first, then OEM | OEM takes priority | Check transition |
| Both connected at startup | OEM preferred | Verify behavior |
| OEM removed with USB-C connected | USB-C takes over if supported | Check stability |
| USB-C removed with OEM connected | OEM continues normally | Check stability |
| USB-C removed while console is running on USB-C | Console powers off safely | Expected if no other source |
| OEM removed while console is running on OEM only | Console powers off safely | Expected if no other source |

Safe behavior is more important than seamless behavior.

A console reset during early source switching tests may be acceptable if the power path remains safe.

A voltage spike, backfeed, or overheating condition is not acceptable.

---

## Stage 14 - Long-Term Validation

Long-term validation helps find problems that do not appear during short tests.

Long-term tests may include:

- 30-minute runtime
- 1-hour runtime
- 2-hour runtime
- Multiple cold starts
- Multiple power cycles
- Multiple cable insertions/removals
- Multiple source switching tests
- Testing with the console shell closed
- Testing after the board has warmed up
- Testing with the intended internal mods installed

Long-term testing should document heat, voltage, stability, and any failures.

---

## Test Equipment

Useful test equipment may include:

- Multimeter
- Oscilloscope
- USB-C PD meter
- USB-C cable tester
- Dummy load
- Bench power supply
- Thermal camera
- Infrared thermometer
- Clamp meter or inline current meter
- Known-good OEM PS2 power supply
- Known-good USB-C PD charger
- Known-good USB-C cable

Not every tool is required for every test, but the more measurements collected, the better.

---

## Multimeter Testing

A multimeter is useful for:

- No-load voltage
- Loaded voltage
- Continuity
- Short testing
- Polarity checks
- Voltage drop checks
- Output voltage confirmation
- Basic current measurement, if set up safely

A multimeter is the first tool to use, but it will not show fast dips, ripple, or switching noise clearly.

---

## USB-C PD Meter Testing

A USB-C PD meter can help show what the charger and trigger board are doing.

A PD meter may show:

- Negotiated voltage
- Current draw
- Power draw
- Charger profile
- Cable behavior
- Voltage drop
- PD renegotiation behavior

A PD meter is useful, but it should not replace measuring the PowerOR output and console input directly.

---

## Dummy Load Testing Notes

The dummy load should be rated for the voltage and current being tested.

During dummy-load testing:

- Start with a low load.
- Increase current gradually.
- Monitor voltage.
- Monitor heat.
- Watch for charger shutdown.
- Watch for voltage sag.
- Do not leave the setup unattended.
- Stop if anything gets too hot or unstable.

The dummy load should be used before risking a console.

---

## Current Draw Documentation

Each test build should have a current draw table.

Suggested current draw table:

| Test Condition | Voltage | Current | Power | Notes |
|---|---:|---:|---:|---|
| No load | TBD | TBD | TBD |  |
| Dummy load 1A | TBD | TBD | TBD |  |
| Dummy load 2A | TBD | TBD | TBD |  |
| Dummy load 3A | TBD | TBD | TBD |  |
| Console startup | TBD | TBD | TBD |  |
| Console idle | TBD | TBD | TBD |  |
| Gameplay | TBD | TBD | TBD |  |
| Long runtime | TBD | TBD | TBD |  |

Measured data is more useful than estimates.

---

## Voltage Measurement Documentation

Voltage should be measured at more than one point.

Suggested voltage table:

| Measurement Point | OEM Only | USB-C Only | Both Connected | Notes |
|---|---:|---:|---:|---|
| OEM input | TBD | TBD | TBD |  |
| USB-C input | TBD | TBD | TBD |  |
| Trigger output | TBD | TBD | TBD |  |
| PowerOR output | TBD | TBD | TBD |  |
| Console input | TBD | TBD | TBD |  |

The voltage at the console input is the most important measurement.

---

## Thermal Documentation

Thermal behavior should be documented.

Suggested thermal table:

| Test Condition | Part Checked | Temperature | Time | Notes |
|---|---|---:|---:|---|
| No load | TBD | TBD | TBD |  |
| 1A load | TBD | TBD | TBD |  |
| 2A load | TBD | TBD | TBD |  |
| 3A load | TBD | TBD | TBD |  |
| Console idle | TBD | TBD | TBD |  |
| Gameplay | TBD | TBD | TBD |  |
| Long runtime | TBD | TBD | TBD |  |

If a part becomes too hot to safely touch, testing should stop until the cause is understood.

---

## Charger and Cable Documentation

The charger and cable are part of the power system and should be documented.

Suggested charger/cable table:

| Item | Details | Notes |
|---|---|---|
| Charger brand/model | TBD |  |
| Charger rated wattage | TBD |  |
| Supported PD profiles | TBD |  |
| Cable brand/model | TBD |  |
| Cable length | TBD |  |
| Cable current rating | TBD |  |
| E-marked cable | TBD |  |
| USB-C PD meter used | TBD |  |

Changing the charger or cable can change the test results.

---

## Console Test Documentation

Each console test should be documented.

Suggested console test table:

| Item | Details | Notes |
|---|---|---|
| Console model | TBD | Example: SCPH-79001 |
| Board revision | TBD | Example: GH-061 or GH-062 |
| Optical drive installed | TBD | Yes / No |
| Installed mods | TBD | List mods |
| PowerOR revision | TBD |  |
| Charger used | TBD |  |
| Cable used | TBD |  |
| Test duration | TBD |  |
| Result | TBD | Pass / Fail / Needs retest |

Testing should be tied to the exact console and board revision when possible.

---

## Pass / Fail Criteria

Testing should use clear pass/fail criteria.

A test may be considered a pass if:

- Output voltage is correct.
- Voltage remains stable under load.
- No unsafe backfeeding is found.
- No dangerous dips or spikes are observed.
- Heat stays within an acceptable range.
- OEM PSU priority works as expected.
- The console boots reliably.
- The console runs without random resets.
- Internal mods behave normally.
- Source switching does not create unsafe behavior.

A test should be considered a fail if:

- Output voltage is wrong.
- Voltage sags too low.
- Voltage overshoots.
- Backfeeding is present.
- Parts overheat.
- Charger shuts down unexpectedly.
- Console resets randomly.
- Controller or storage behavior becomes unstable.
- Source switching causes unsafe spikes or dips.
- The result cannot be repeated.

---

## Failure Documentation

Failures are useful and should be documented.

When a failure happens, record:

- Board revision
- Console model
- Charger used
- Cable used
- Test condition
- Load current
- Voltage readings
- Temperature readings
- What failed
- When it failed
- Whether it was repeatable
- Photos or oscilloscope captures, if available
- Possible cause
- Next action

A failure is not wasted time if it improves the design.

---

## Revision Testing

Each board revision should have its own test notes.

Suggested revision table:

| PowerOR Revision | Status | Notes |
|---|---|---|
| v0.1 | Prototype | Initial bench testing |
| v0.2 | Prototype | Changes after first test |
| v0.3 | Prototype | Fitment and power changes |
| Beta | Future | Small controlled test batch |
| Release Candidate | Future | Final validation before kit |

Do not assume a new revision passes just because an older one did.

Every revision should be tested.

---

## Test Result Status Terms

Suggested status terms:

| Status | Meaning |
|---|---|
| Not started | Test has not been performed yet |
| In progress | Test is currently being worked on |
| Pass | Test passed under documented conditions |
| Fail | Test failed under documented conditions |
| Needs retest | Test result is unclear or conditions changed |
| Not applicable | Test does not apply to this revision or setup |

Use clear status terms so the project remains easy to follow.

---

## Main Test Checklist

Suggested main checklist:

| Test | Status | Notes |
|---|---|---|
| Visual inspection | Not started |  |
| Short check | Not started |  |
| USB-C trigger voltage verified | Not started |  |
| OEM PSU voltage verified | Not started |  |
| PowerOR no-load output verified | Not started |  |
| Dummy-load test completed | Not started |  |
| 1A load test | Not started |  |
| 2A load test | Not started |  |
| 3A load test | Not started |  |
| Heat checked under load | Not started |  |
| Ripple checked | Not started |  |
| Backfeed checked | Not started |  |
| OEM priority checked | Not started |  |
| Source switching checked | Not started |  |
| Console startup tested | Not started |  |
| Console runtime tested | Not started |  |
| Long-term test completed | Not started |  |
| Fitment checked | Not started |  |
| Shell closed test completed | Not started |  |

---

## Test Notes Folder

Testing notes should be saved in the repository.

Suggested folders:

<pre>
Testing/Bench-Testing/
Testing/Load-Testing/
Testing/Console-Testing/
Testing/Oscilloscope-Captures/
Testing/Results/
Images/Testing/
</pre>

Photos and screenshots should be named clearly so they can be matched to the test notes.

---

## Beta Testing

If the project reaches a beta stage, beta testing should be controlled.

Beta boards should only be used with:

- Known console models
- Known board revisions
- Known charger and cable combinations
- Clearly documented install instructions
- Clear warnings that the design is still experimental
- Clear feedback requirements

Beta testing should collect:

- Fitment notes
- Install notes
- Runtime notes
- Heat observations
- Failure reports
- Charger/cable behavior
- Console model compatibility

Beta testing should not be treated as a public release.

---

## Kit Release Validation

Before a kit is released, the design should pass the intended tests.

A kit should not be released until:

- The target console range is clearly defined.
- The unsupported console range is clearly defined.
- The power limit is clearly defined.
- The charger requirements are clearly defined.
- The cable requirements are clearly defined.
- OEM PSU priority has been tested.
- USB-C PD input has been tested.
- Backfeed prevention has been tested.
- Thermal behavior has been tested.
- Fitment has been tested.
- Installation notes are ready.
- Safety warnings are clear.

A kit should not be advertised as universal.

---

## Public Documentation and Final Kit Files

This repository may document:

- Testing plans
- Test results
- Fitment notes
- Public measurements
- Photos
- Failures
- Revision notes
- Safety findings

Final production files are not planned for public release at this time.

This may include:

- Final Gerbers
- Complete KiCad source
- Pick-and-place files
- Final production BOM
- Assembly files
- Manufacturing package

The goal is to document the project while protecting the final assembled kit design.

---

## Practical Testing Rule

For PowerOR, the practical testing rule is:

Test the power system before trusting the power system.

That means:

- Do not connect to a console first.
- Do not trust seller claims.
- Do not trust no-load voltage alone.
- Do not ignore heat.
- Do not ignore backfeeding.
- Do not ignore source switching.
- Do not assume one charger behaves like another.
- Do not assume one cable behaves like another.
- Do not assume one PS2 Slim behaves like another.

Testing should guide the design.

---

## Project Position

Testing and validation are central to PowerOR.

The project is experimental until the design has been measured, tested, revised, and proven under the intended use conditions.

A successful power-on test is not enough.

PowerOR should only move toward a kit release after the power behavior, fitment, heat, compatibility, and safety limits are understood.

---

## Disclaimer

This document is part of an experimental hardware project.

Incorrect testing, unsafe power connections, wrong voltage, insufficient current, overheating, poor wiring, poor source switching, or untested assumptions can damage a PlayStation 2 console.

Use this information at your own risk.
