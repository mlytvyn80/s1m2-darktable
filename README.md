# s1m2-darktable

# Panasonic Lumix S1M2 — darktable support

This repository contains RAW samples, JPEG references, ColorChecker measurements, white-balance tests, noise samples and other data collected to help develop and validate full support for the **Panasonic Lumix DC-S1M2** in [darktable](https://www.darktable.org/).

## Goal

The goal is to provide reproducible test material for:

* RAW decoding
* camera identification
* white-balance presets
* color matrix / color rendering
* ColorChecker calibration
* noise profile
* dynamic range
* highlight behavior
* EXIF / metadata
* lens correction data, where applicable

---

## Camera

| Parameter         | Value                        |
| ----------------- | ---------------------------  |
| Camera            | Panasonic Lumix DC-S1M2      |
| Firmware          | Ver. 1.4                     |
| RAW format        | RW2                          |
| Sensor            | BSI-CMOS 24.1 Mp             |
| Test lens         | Panasonic Lumix S 50mm F1.8  |
| darktable version | Ver. 5.6.2                   |

---

# Test material

## 01 — Basic RAW sample

Purpose: basic camera identification and RAW decoding.

* [ ] ISO 100
* [ ] Daylight
* [ ] Landscape / detailed subject
* [ ] RAW
* [ ] JPEG reference

Files:

```text
01_basic/
├── S1M2_ISO100_daylight.RW2
└── S1M2_ISO100_daylight.JPG
```

---

## 02 — White Balance

Purpose: determine and verify camera white-balance presets.

Test conditions:

* [ ] Daylight
* [ ] Cloudy
* [ ] Shade
* [ ] Tungsten
* [ ] Fluorescent
* [ ] Flash
* [ ] Custom Kelvin values
* [ ] Auto WB

For each test:

```text
RAW + JPEG
```

Files:

```text
02_white_balance/
├── daylight/
├── cloudy/
├── shade/
├── tungsten/
├── fluorescent/
├── flash/
└── kelvin/
```

---

## 03 — ColorChecker

Purpose: evaluate the camera color matrix and color rendering.

Target:

**Calibrite ColorChecker Passport Photo 2 — Classic 24 patches**

Test conditions:

* ISO 100
* fixed WB
* controlled daylight
* uniform illumination
* RAW + JPEG
* multiple exposures

Recommended exposure series:

```text
-1.0 EV
-0.5 EV
 0.0 EV
+0.5 EV
+1.0 EV
```

Files:

```text
03_colorchecker/
├── RAW/
├── JPEG/
├── XMP/
└── results/
```

Record:

* ColorChecker version
* WB
* exposure
* darktable version
* optimization strategy
* average ΔE
* maximum ΔE
* generated color calibration matrix

---

## 04 — ISO / Noise Profile

Purpose: create and validate the camera noise profile.

Recommended ISO values:

```text
100
200
400
800
1600
3200
6400
12800
25600
51200
```

Use the highest useful ISO values supported by the camera if additional native/extended values are available.

Keep constant:

* lighting
* aperture
* shutter strategy
* subject
* lens
* focal length

Files:

```text
04_noise/
├── ISO100/
├── ISO200/
├── ISO400/
├── ISO800/
├── ISO1600/
├── ISO3200/
├── ISO6400/
├── ISO12800/
├── ISO25600/
└── ...
```

---

## 05 — Dynamic Range

Purpose: evaluate sensor dynamic range and RAW highlight/shadow behavior.

Create an exposure bracket using a fixed scene:

```text
-5 EV
-4 EV
-3 EV
-2 EV
-1 EV
 0 EV
+1 EV
+2 EV
+3 EV
```

Record:

* shutter speed
* aperture
* ISO
* clipping point
* shadow recovery
* highlight recovery

Files:

```text
05_dynamic_range/
├── -5EV/
├── -4EV/
├── -3EV/
├── -2EV/
├── -1EV/
├──  0EV/
├── +1EV/
├── +2EV/
└── +3EV/
```

---

## 06 — Highlight Behavior

Purpose: determine RAW clipping and highlight roll-off.

Use a scene containing:

* specular highlights
* white objects
* bright sky
* high-contrast areas

Capture RAW + JPEG.

Record:

* exposure
* ISO
* clipping behavior
* whether clipped channels remain recoverable in RAW

---

## 07 — RAW Format / Compression

Purpose: verify all RAW recording modes supported by the camera.

Test all available modes, for example:

```text
Lossless RAW
Compressed RAW
Other RAW modes
```

Record:

* file size
* bit depth, if known
* resolution
* whether darktable opens the file correctly
* differences between modes

---

## 08 — Metadata / EXIF

Purpose: verify metadata extraction.

Check:

* camera make
* camera model
* firmware
* ISO
* shutter speed
* aperture
* focal length
* lens model
* white balance
* orientation
* exposure compensation
* image dimensions

---

## 09 — Lens Correction

Optional.

Purpose: collect data for lens correction support.

For each lens:

* focal lengths
* apertures
* RAW samples
* distortion
* vignetting
* chromatic aberration

Directory:

```text
09_lens_correction/
└── <lens-name>/
```

---

# File naming convention

Use:

```text
S1M2_<test>_<ISO>_<WB>_<exposure>_<lens>.<ext>
```

Example:

```text
S1M2_ColorChecker_ISO100_5000K_0EV_50mm.RW2
S1M2_ColorChecker_ISO100_5000K_0EV_50mm.JPG
```

Keep the original camera files unchanged.

**Do not convert RAW files to DNG unless specifically requested.**

---

# Test documentation

Each test should include a small text or Markdown file describing the conditions.

Example:

```text
Camera: Panasonic Lumix DC-S1M2
Firmware: 1.4
Lens: Panasonic Lumix S 50mm F1.8
ISO: 100
WB: 5000 K
Aperture: f/8
Shutter: 1/125 s
Exposure compensation: 0 EV
Light: daylight
Darktable: 5.6.2
```

---

# darktable results

For tests performed in darktable, preserve the corresponding XMP sidecar:

```text
image.RW2
image.RW2.xmp
```

Important results should also be documented in:

```text
results/
```

For ColorChecker tests record:

```text
Average ΔE:
Maximum ΔE:
Optimization strategy:
Input color profile:
White balance:
ColorChecker reference:
```

---

# Repository structure

```text
.
├── README.md
├── LICENSE
├── 01_basic/
├── 02_white-balance/
├── 03_colorchecker/
├── 04_noise/
├── 05_dynamic-range/
├── 06_highlights/
├── 07_raw-formats/
├── 08_metadata/
├── 09_lens-correction/
│   ├── lumix-s-20-60/
│   │   ├── 20mm/
│   │   ├── 35mm/
│   │   └── 60mm/
│   ├── lumix-s-50-1.8/
│   ├── lumix-s-85-1.8/
│   └── lumix-s-20-40/
│       ├── 20mm/
│       ├── 30mm/
│       └── 40mm/
└── results/
```

---

# Status


| Test                     | Status |
| ------------------------ | ------ |
| Basic RAW                | ⬜      |
| White Balance            | ⬜      |
| ColorChecker             | ⬜      |
| ISO / Noise              | ⬜      |
| Dynamic Range            | ⬜      |
| Highlight Behavior       | ⬜      |
| RAW Modes                | ⬜      |
| Metadata / EXIF          | ⬜      |
| Lens — Lumix S 20–60mm   | ⬜      |
| Lens — Lumix S 50mm F1.8 | ⬜      |
| Lens — Lumix S 85mm F1.8 | ⬜      |
| Lens — Lumix S 20–40mm   | ⬜      |


Legend:

* ⬜ Not started
* 🟨 In progress
* 🟩 Complete
* 🟥 Problem found

---

# Notes

All original RAW and JPEG files should be preserved without modification.

The purpose of this repository is to provide reproducible technical data that can be shared with the **darktable / RawSpeed community** when requesting or validating Panasonic Lumix S1M2 support.

# License

Unless otherwise stated, all RAW files, JPEG files, measurements, metadata, XMP files, test results and other original materials in this repository are dedicated to the public domain under the **CC0 1.0 Universal** license.

You can copy, modify, distribute and use the materials for any purpose without asking for permission.

See the [`LICENSE`](LICENSE) file for the complete license text.

This repository is intended to provide freely reusable test data for the development and validation of camera support in **darktable**, **RawSpeed**, and related open-source software.


