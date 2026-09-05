# HFC Coax Signal Loss Calculator

## Overview

The **HFC Coax Signal Loss Calculator** is a standalone browser-based tool for estimating signal attenuation through coaxial cable used in Hybrid Fiber-Coaxial (HFC) networks.

The calculator is designed for field technicians, installers, maintenance technicians, and anyone working with CATV or broadband coaxial systems.

It estimates cable loss based on:

- Cable type
- Signal frequency in MHz
- Cable length
- Optional starting signal level in dBmV

The calculator then provides the estimated cable attenuation in dB and, when a starting level is entered, the estimated signal level at the far end of the cable.

---

## Supported Cable Types

### Drop Cable

- RG59 / Series 59
- RG6 / Series 6
- RG11 / Series 11

### Hardline Cable

- 0.500 inch
- 0.565 inch
- 0.625 inch
- 0.700 inch
- 0.750 inch
- 0.875 inch
- 1.000 inch legacy hardline

The attenuation values in this version are based primarily on published CommScope foam drop cable and P3 hardline specifications.

Actual attenuation may vary depending on manufacturer, cable construction, cable age, temperature, and physical condition.

---

## How It Works

Coaxial cable loss increases with both:

1. Cable length
2. Signal frequency

Higher-frequency signals experience more attenuation than lower-frequency signals over the same length of cable.

The calculator stores known attenuation values in:

**dB per 100 feet**

for multiple frequencies for each supported cable type.

When the entered frequency falls between two published reference frequencies, the calculator interpolates between the closest attenuation values.

### Basic Calculation

The total cable loss is calculated using:

```text
Total Loss (dB) = Attenuation (dB/100 ft) × Cable Length (ft) / 100
```

For example, if a cable has an attenuation of:

```text
2.00 dB / 100 ft
```

and the cable length is:

```text
350 ft
```

then:

```text
2.00 × 350 / 100 = 7.00 dB
```

The estimated cable loss is therefore:

```text
7.00 dB
```

---

## Signal Level Calculation

The calculator also accepts an optional starting signal level in **dBmV**.

If a starting level is entered, the ending signal level is calculated as:

```text
Ending Level = Starting Level - Cable Loss
```

Example:

```text
Starting Level: +20 dBmV
Cable Loss:      7 dB

Ending Level:   +13 dBmV
```

---

## Frequency Interpolation

Cable manufacturers normally publish attenuation values only at selected frequencies.

For example, a cable may be rated at:

```text
750 MHz = 1.48 dB / 100 ft
865 MHz = 1.61 dB / 100 ft
```

If the technician enters:

```text
800 MHz
```

the calculator estimates the attenuation between the two published points.

This provides a more realistic result than using one fixed loss value for an entire frequency range.

The calculator does **not** extrapolate outside the stored frequency range.

If a frequency is entered beyond the available cable data, the calculator displays an error instead of estimating an unsupported value.

---

## Common HFC Frequency Presets

The interface includes quick-select buttons for several commonly encountered HFC frequencies:

- 5 MHz
- 42 MHz
- 85 MHz
- 204 MHz
- 550 MHz
- 750 MHz
- 1002 MHz
- 1218 MHz

These are intended to make it easier to compare low-frequency return-path loss with higher-frequency forward-path loss.

---

## Length Units

Cable length can be entered in:

- Feet
- Meters

When meters are selected, the calculator internally converts the distance to feet before calculating attenuation.

---

## Example

Assume the following:

```text
Cable:      0.750 inch hardline
Frequency:  1000 MHz
Length:     500 ft
```

If the cable attenuation is approximately:

```text
1.74 dB / 100 ft
```

then:

```text
1.74 × 500 / 100 = 8.70 dB
```

Estimated cable attenuation:

```text
8.70 dB
```

If the signal begins at:

```text
+30 dBmV
```

then the estimated ending level would be:

```text
+21.30 dBmV
```

---

## What the Calculator Includes

The current version calculates attenuation caused by the coaxial cable itself.

It includes:

- Cable attenuation
- Frequency-dependent loss
- Length-dependent loss
- Frequency interpolation
- Feet and meter conversion
- Optional starting signal level
- Estimated ending signal level

---

## What the Calculator Does Not Include

The current version does not automatically account for losses or gains from other HFC plant components.

Examples include:

- Taps
- Splitters
- Directional couplers
- Power inserters
- Connectors
- Splices
- Equalizers
- Amplifiers
- Line extenders
- Node output levels
- Passive insertion loss
- Temperature compensation

These losses must currently be considered separately.

---

## Accuracy

The calculator should be treated as an engineering and field-estimation tool rather than a replacement for actual RF measurements.

Real-world signal levels can differ because of:

- Cable manufacturer
- Cable temperature
- Cable age
- Water intrusion
- Damaged shielding
- Poor connectors
- Corrosion
- Improperly seated hardline connectors
- Passive device losses
- Amplifier alignment
- Plant distortion
- Frequency response differences

Whenever possible, calculated values should be compared with readings from a calibrated signal-level meter or spectrum analyzer.

---

## Installation

No installation is required.

The calculator is contained in a single HTML file.

To use it:

1. Download `hfc_signal_loss_calculator.html`.
2. Open the file in a modern web browser.
3. Select the cable type.
4. Enter the signal frequency.
5. Enter the cable length.
6. Optionally enter the starting signal level.
7. Read the calculated cable loss and ending level.

Because the calculator runs entirely in the browser, it does not require an internet connection or web server.

It can also be hosted on an internal technician web server if desired.

---

## File Structure

Current version:

```text
hfc_signal_loss_calculator.html
README.md
```

The calculator is self-contained, with the HTML, CSS, JavaScript, and cable attenuation tables stored in one file.

---

## Potential Future Features

A future version could expand the calculator into a complete HFC plant path calculator.

Possible additions include:

- Temperature compensation
- More cable manufacturers
- User-editable attenuation tables
- Connector loss
- Splice loss
- Tap values
- Splitter loss
- Directional couplers
- Amplifier gain
- Line extender gain
- Equalizer calculations
- Node output levels
- Upstream and downstream path calculations
- Multiple cable sections
- Full cascade calculations
- Frequency sweep comparisons
- Minimum and maximum signal limits
- Technician pass/fail indicators
- Printable reports
- Saved plant configurations

A more advanced path could look like:

```text
Node
 ↓
320 ft 0.750 hardline
 ↓
Line Extender
 ↓
180 ft 0.625 hardline
 ↓
17 dB Tap
 ↓
85 ft RG6
 ↓
Customer Modem
```

The program could then calculate and display the expected signal level at every point in the path.

---

## Intended Use

This tool is intended primarily for:

- CATV technicians
- Broadband technicians
- HFC maintenance technicians
- Cable installers
- Plant engineers
- Headend technicians
- Network troubleshooting
- Training
- HFC system planning

---

## Disclaimer

Calculated values are estimates based on reference attenuation data.

Always follow the specifications provided by the actual cable manufacturer when engineering or certifying an HFC system.

For troubleshooting active plant, verify calculated levels with appropriate RF test equipment whenever possible.
