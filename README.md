
<div align="center">

# 🐱 3NyanTracker

### Ultra-Low-Cost MIPI-Direct Mouth Tracker for Steam Frame

*A concept-stage, hardware-only, source-available Steam Frame accessory design*

[![License: 3NyanTracker HDL 1.0](https://img.shields.io/badge/License-3NyanTracker%20HDL%201.0-lightgrey.svg)](./LICENSE)
![Status](https://img.shields.io/badge/status-component%20selection%20%2F%20pre--PCB-orange)
![Target](https://img.shields.io/badge/target-Valve%20Steam%20Frame-1b2838)
![Scope](https://img.shields.io/badge/scope-hardware--only-blue)
![Interface](https://img.shields.io/badge/interface-MIPI%20CSI--2-blueviolet)

</div>

---

## ⚡ TL;DR

| | |
|---|---|
| **What** | A single-camera mouth/lower-face module connected directly to the Steam Frame front expansion port via MIPI CSI-2 |
| **Proposed hardware** | **1 × OV7251** monochrome global-shutter camera + **1 × 940 nm IR LED** + the minimum circuitry needed to run them |
| **What it eliminates** | USB bridge, ESP32/other MCU, wireless link, on-device video processing, and battery |
| **What it's not** | Tracking software, eye tracking, or an affiliate of any software/tracking project |
| **Status** | Official expansion-port interface published; camera, optics, PCB, and host integration remain unverified |
| **Cost goal** | As inexpensive as practical; aspirational component/PCB target **under US$10 per unit at volume**, not a quote |

---

## 📖 Table of Contents

- [Summary](#-summary)
- [Scope](#-scope)
- [Steam Frame Reference](#-steam-frame-reference)
- [Expansion Port](#-expansion-port)
- [Hardware Safety & Warranty](#-hardware-safety--warranty)
- [Design Goals](#-design-goals)
- [Hardware Overview](#-hardware-overview)
- [Electrical Interface](#-electrical-interface)
- [Mechanical & Optical Design](#-mechanical--optical-design)
- [Status & Roadmap](#-status--roadmap)
- [Bill of Materials](#-bill-of-materials-draft)
- [Open Questions](#-open-questions)
- [Contributing](#-contributing)
- [License](#-license)
- [Changelog](#-changelog)
- [Project Info](#-project-info)

---

## 📝 Summary

**3NyanTracker** is a low-cost, hardware-only design for a mouth/lower-face camera module connecting directly to the Valve Steam Frame's front expansion port over **MIPI CSI-2**.

The proposed first revision uses **exactly one IR-sensitive image sensor and one IR LED**. Video is delivered to the headset over MIPI; the design has **no USB bridge, external compute board, MCU, wireless video link, or dedicated battery**. The headset is expected to provide the host-side image capture and processing resources, **subject to driver and firmware support**.

> **🔧 Hardware only.** This repository covers the camera/illumination hardware and its physical/electrical interface to the Steam Frame. It does not include, require, or endorse any tracking algorithm, calibration tool, client, or other software project. Producing and consuming raw camera frames on SteamOS is a separate integration problem and is **not yet demonstrated** by this design.

This project was first published on **2026-09-18**. Valve has since published its expansion-port reference material; the hardware direction below reflects that documentation. The project is **still pre-schematic/pre-PCB**, not a working or certified accessory.

## 📦 Scope

**✅ In scope**
- One mouth-facing MIPI CSI-2 camera and its optics
- One mouth-facing 940 nm IR LED with appropriate current limiting
- Power conversion, I²C identification EEPROM, and required passives
- Custom 44-contact expansion-port paddle/interface PCB and flexible interconnect
- Lightweight mounting and raw-image-capable electrical design
- Low-cost, reproducible PCB/BOM/mechanical documentation once designed

**❌ Out of scope**
- Face-tracking algorithms, calibration, plugins, or client software
- Firmware/SteamOS camera pipeline modifications **within this repo**
- Eye tracking or any modification to the Frame's built-in eye cameras
- Circumventing accessory checks, authentication, or platform security

> **👁️ The Steam Frame's built-in eye-tracking cameras are not part of this project.** The module is intended to view the mouth/lower face only and must avoid blocking the headset's existing sensors.

## 🥽 Steam Frame Reference

Valve reference links (the official documents remain the source of truth):

- 🔗 [Steam Frame product page](https://store.steampowered.com/hardware/steamframe)
- 🔗 [Steam Frame developer documentation](https://partner.steamgames.com/doc/steamframe)
- 🔗 [Valve Steam Frame hardware repository](https://gitlab.steamos.cloud/SteamHardware/SteamFrame)
- 🔗 [Front expansion-port document](https://gitlab.steamos.cloud/SteamHardware/SteamFrame/-/blob/master/documents-expansion-port/20261001_External_Interface_Front_Port.pdf)

The Frame's battery is shared with accessories powered from its expansion port. Low idle and active power consumption are therefore core design priorities.

## 🔌 Expansion Port

The **official front/nose-bridge expansion-port electrical and mechanical specification is now public**. It describes two four-lane MIPI D-PHY camera paths, one PCIe Gen4 ×1 interface sharing pins with the left camera path, power, and low-speed control/CCI signals.

| Item | Published interface specification |
|---|---|
| Physical connection | **44 contacts** (22 per PCB side), **0.5 mm pitch**, 0.35 mm contact width |
| Card-edge PCB thickness | **0.8 mm** at the mating edge |
| Supply | **3.1 V**, rated **2 A continuous** for the port as a whole (~6.2 W maximum), with ~3 A current limit |
| Logic level | **1.8 V** for digital IO; **not 3.3 V tolerant** |
| Camera link | MIPI **D-PHY v1.2**, up to **2.5 Gbps per lane**, two four-lane paths available in camera mode |
| Camera master clock | **19.2 MHz** (right camera MCLK available on pin 22) |
| Control bus | **400 kHz I²C/CCI**, pull-ups on the accessory side |
| USB | **No native USB data interface** on the expansion-port pins |

### Power-up and device identification

1. Connect **pin 44 (`RGB_DET/GND`) to GND** to request the port's initial power.
2. The host subsequently validates a recognized configuration; pin 44 alone **does not** guarantee that power stays on.
3. For a **custom MIPI camera**, the reference design calls for an **I²C EEPROM**, e.g. a CAT24C32-compatible device, responding at **7-bit address `0x51`** with **16-bit memory addressing**. Its actual configuration contents and host integration must still be established.
4. Fit **2.2 kΩ pull-up resistors from both CCI lines to 1.8 V** on the accessory. Do not pull these pins up to 3.1 V or 3.3 V.

> **⚠️ Important:** Shorting `R_STROBE` (pin 38) and `CAM_RESET` (pin 42) is described by Valve for **power-only or PCIe-only** accessories. It is **not the intended identification scheme for a custom MIPI camera**. An EEPROM/proper configuration and host-side support are separate requirements.

## ⚠️ Hardware Safety & Warranty

This project is unofficial and **not certified as "Steam Frame Compatible."**

Valve's [Steam Frame Hardware Reference](https://gitlab.steamos.cloud/SteamHardware/SteamFrame) warns that uncertified interfaces may damage hardware. The reference documents are provided AS IS and hardware designs may change.

**No prototype has been validated for electrical safety or compatibility.**

Verify pin orientation, voltage, current limiting, ESD, MIPI routing, and IR eye-exposure safety before connecting hardware.

Warranty consequences depend on the circumstances and applicable law.

## 🎯 Design Goals

- **MIPI CSI-2 directly into the Steam Frame**; no USB conversion
- **Exactly one camera + one IR LED** in the baseline design
- Monochrome/global-shutter/IR-sensitive image capture preferred
- **940 nm** mouth illumination; minimize stray light toward the eyes
- **640 × 480 at 60 fps** as an initial *target*, not a verified Frame capability
- Short, controlled-impedance MIPI routing and a light, flexible mount
- Very low BOM and power consumption; **<0.3 W active** is a provisional stretch target to be measured, not a confirmed specification
- Raw camera output only; software integration belongs elsewhere

## 🛠️ Hardware Overview

### Preferred sensor: OmniVision OV7251 (candidate, not locked)

The **OV7251** is the leading low-cost candidate because it offers a **monochrome 640 × 480 global-shutter** image sensor with **MIPI CSI-2**, and existing Linux driver code accepts a **19.2 MHz** external clock. A one-data-lane configuration is the intended starting point.

- Planned image stream: **one MIPI data lane + one MIPI clock pair**
- Planned capture target: **640 × 480 / 60 fps**, subject to validation
- Lens: **short working distance / close focus** for the mouth region; exact focal length and focus distance TBD
- **Sensor module vs. bare die/package:** compare total cost including lens, alignment, assembly, and availability; do not optimize sensor price alone
- Linux having an OV7251 driver **does not establish Steam Frame compatibility**. Camera enumeration, CCI setup, CSI routing, platform camera pipeline, and access to frames must be verified separately.

Upstream driver reference: [Linux `ov7251.c`](https://github.com/torvalds/linux/blob/master/drivers/media/i2c/ov7251.c).

### Illumination: exactly one 940 nm IR LED

- Use one **wide-angle 940 nm SMD IR emitter**, facing the mouth, not the eyes
- Provide proper LED current limiting and verify safe optical output
- A single emitter may be insufficient for even illumination; **test before adding another LED**
- Start with low drive current; prioritize battery life and thermal comfort
- Final emitter, viewing angle, drive current, resistor/driver, and on/off behavior **TBD**

### Minimal proposed architecture

```text
Steam Frame front expansion port (3.1 V + 1.8 V CCI + MIPI CSI-2)
       |
       +-- MIPI D-PHY (1 data lane + clock) ---> OV7251 camera
       |                                        + short-focus lens
       |
       +-- 19.2 MHz MCLK / CCI I²C / RESET ---> sensor control
       |
       +-- CCI I²C ---------------------------> identification EEPROM (0x51)
       |
       +-- 3.1 V --> power rails / filtering --> camera sensor
       |
       +-- 3.1 V --> current limiting --------> 1 × 940 nm IR LED
       |
       +-- GND / detection -------------------> paddle identification
```

No ESP32, USB controller, Wi-Fi module, image-processing MCU, battery, or charging circuitry is planned.

## 🔧 Electrical Interface

### Planned single-camera connection (right camera path)

The table below is a **design planning subset**, not the complete 44-pin pinout or a finished schematic. Pin numbers and signal names are from Valve's published front-port specification.

| Port pin(s) | Signal(s) | Intended use |
|---|---|---|
| **3 / 5** | `R_L0_P / R_L0_M` | MIPI CSI-2 data lane 0 differential pair |
| **4 / 6** | `R_CLK_P / R_CLK_M` | MIPI CSI-2 clock differential pair |
| **22** | `R_MCLK` | 19.2 MHz camera reference clock, 1.8 V logic |
| **28 / 30 / 32** | `3V1_CAM` | Shared 3.1 V accessory supply |
| **34 / 36** | `CCI_SCL / CCI_SDA` | 1.8 V I²C bus for sensor and EEPROM |
| **42** | `CAM_RESET` | Host-controlled 1.8 V camera reset; polarity/sequence to verify |
| **44** | `RGB_DET/GND` | Tie to ground for initial device detection |
| **GND contacts** | `GND` | Ground return and high-speed reference |

Key implementation rules:

- **85 Ω differential impedance** for MIPI D-PHY pairs.
- Maximum published **intra-pair skew: 150 µm**, **inter-pair length mismatch: 350 µm**; keep the interconnect short.
- Sensor supply rails are **not** the port's 3.1 V rail by default. Provide the required analog/IO/core regulation **after checking the selected sensor/module datasheet**.
- Use proper decoupling, ESD considerations, power sequencing, and 1.8 V compatibility.
- The host's port-enable sequence, EEPROM configuration, camera address conflicts, and CSI/driver setup must be validated before attaching a prototype to valuable hardware.

## 📐 Mechanical & Optical Design

The published mating-edge geometry calls for:

- **0.8 mm** PCB thickness at the paddle edge
- **0.5 mm** contact pitch; **0.35 mm** pad width
- Pad length from the board edge: **2.51 mm** on the visor-facing side, **2.01 mm** on the user-facing side
- **45°** lead-in corners and a **20° / 0.3 mm** edge chamfer
- Contact finish and manufacturing tolerances to be verified with the PCB manufacturer; do not assume a standard thick PCB/edge connector will fit

Prefer a **flexible interconnect** between the rigid paddle and the camera mount to avoid loading the headset connector. Prototype mounts can be 3D printed.

Optics should cover the mouth from the actual installed position at a short working distance, without obscuring the built-in cameras or creating irritating pressure points. A 940 nm emitter still requires an **IR eye-exposure / photobiological safety assessment**, especially this close to the face.

## 🗺️ Status & Roadmap

| Phase | What | Status |
|:---:|---|:---:|
| 0 | Concept + hardware-only scope | ✅ Done |
| 1 | Official expansion-port documents and initial pin planning | ✅ Available / reviewed |
| 2 | OV7251 vs. alternative camera/module, close-focus optics, 940 nm LED | 🔍 Selecting |
| 3 | Power rails, EEPROM configuration, schematic, PCB, and flex/mount design | 📋 Planned |
| 4 | Safe electrical bring-up and port detection | 📋 Planned |
| 5 | Host-side camera enumeration and raw MIPI capture validation *(external integration dependency)* | ❓ Not verified |
| 6 | Optical / IR safety, power, heat, and image-quality testing | 📋 Planned |
| 7 | Release of manufacturing files and a first small batch | 📋 Planned |

**There is no verified working prototype yet.** Publishing a host-driver source file or an official port pinout is not proof that this particular camera works on SteamOS.

## 💰 Bill of Materials (Draft)

<details>
<summary>Click to expand — indicative 200+ unit component-cost scenario, not supplier quotes</summary>

| Component | Planning range (USD/unit) | Notes |
|---|---:|---|
| OV7251 bare image sensor | $2.60–4.00 | Tentative volume target; stock and qualification unverified |
| Short-focus lens / sensor holder | $1.00–3.00 | Mandatory for usable mouth images; part TBD |
| **One** 940 nm SMD IR LED | $0.03–0.05 | Optical power and current TBD |
| I²C configuration EEPROM | $0.10–0.30 | 1.8 V-compatible CAT24C32-type device |
| Regulators + passives + LED current control | $0.50–1.50 | Sensor voltage rails TBD |
| Paddle PCB + interconnect | $1.50–4.00 | Depends on finish, flex approach, yield, quantity |
| Mount / housing | $0.50–2.50 | Prototype may cost more |
| **Estimated component + fabrication subtotal** | **$6.23–15.35** | **Not** a validated quote or finished-product cost |

**Not included:** PCB assembly, sensor/optical alignment, tooling, failed prototypes, test fixtures, certification/safety checks, packaging, shipping, import fees, tax, or support.

The **under-$10 goal** is aspirational at volume, not a promise. A ready-made camera module may cost more per unit but be cheaper overall for early prototypes because it avoids lens alignment and specialist assembly.

</details>

## ❓ Open Questions

- Can Steam Frame's camera firmware / CSI pipeline enumerate and capture data from the OV7251? **Unverified.**
- What EEPROM data must the host read to sustain power and configure a third-party MIPI camera? **Not yet established.**
- Is the proposed right-camera one-lane wiring and power-up sequence sufficient for a usable image stream? **Needs hardware validation.**
- Which specific OV7251 module or bare-sensor/lens combination gives reliable **5–15 cm** focus and enough 940 nm sensitivity?
- Is **one** wide-angle IR LED bright and uniform enough while remaining safe and low power?
- What are the actual current consumption, heat, effective frame rate, and manufacturing yield?
- What mechanical load, insertion cycles, and strain relief can the mount tolerate?
- Any consumer software's ability to use captured frames is **out of this project's scope**.

## 🤝 Contributing

Issues and PRs welcome — **hardware-related only**: electrical design, connector tolerances, sensor/LED sourcing, optics, PCB layout, mechanical design, testing, and manufacturing documentation. Please distinguish measured/verified data from proposals and price targets. Camera driver and tracking-client implementations belong to separate projects.

## ⚖️ License

<div align="center">

**3NyanTracker Hardware Distribution License 1.0**
*(Custom source-available license inspired by Apache 2.0; not Apache-2.0)* — [full text](./LICENSE)

</div>

| | |
|---|---|
| ✅ Personal use, modification, reverse engineering | Always allowed, explicitly stated |
| ❌ Commercial manufacture or sale | Not without maintainer's written permission |
| 📌 Physical attribution | Must be kept on any built/conveyed unit (e.g. QR code to this repo, silkscreened on the PCB) |
| 🔁 Source availability (copyleft-style) | When conveying a physical unit, provide its Corresponding Source to the recipient under this license, with the unit or through a durable public link maintained as required by Section 10(d)(2). This also applies to downstream derivatives. |
| 🔒 No further restrictions | You can't bolt on extra terms of your own on top of this license |

Just building one for yourself and never handing it to anyone else? None of the source-availability or attribution terms are triggered — only *conveying* a unit to a third party does that.

**Upstream-material notice:** Valve reference CAD and drawings have their own **CC BY-NC-SA 4.0** terms. This repository currently links to but does not redistribute Valve CAD, PCB designs, or schematics. Future adaptations must retain applicable upstream licensing, attribution, and change notices. The 3NyanTracker license does not override Valve's terms. Commercial reuse of Valve-licensed material requires Valve authorization.

*Because this license restricts commercial use, it is a custom **source-available** license rather than an OSI/OSHWA-standard open-source/open-hardware license.*

## 📅 Changelog

- **2026-10-10** — Clarified custom licensing, source delivery, Valve licensing, and prototype safety. Hardware design unchanged.

- **2026-10-10** — Updated the concept after Valve's official front-port hardware publication; added an OV7251 + single 940 nm IR LED baseline, port electrical/mechanical constraints, an EEPROM detection plan, BOM targets, and explicit host-integration risks. **No functional hardware claimed.**
- **2026-09-18** — Initial commit. Concept, goals, roadmap. Hardware-only scope; no software integration implied.

---

## ℹ️ Let's Stay in Touch!

| | |
|---|---|
| **License** | 3NyanTracker Hardware Distribution License 1.0 — see [LICENSE](./LICENSE) |
| **First published** | 2026-09-18 |
| **Maintainer** | Samsacknyan · `rumored-prosy-9j@icloud.com` |

---

™️ **Trademark & Third-Party Notice**

"Steam," "Steam Frame," "SteamOS," "SteamVR," and related logos are trademarks and/or registered trademarks of Valve Corporation in the US and/or other countries. This project is an independent, fan-made, unofficial concept, and is not affiliated with, sponsored by, or endorsed by Valve Corporation.

References to Valve, Steam, or Steam Frame in this repository (including publicly documented electrical parameters and links to Valve-operated pages) describe intended compatibility only and do not claim official certification. No Valve-authored CAD, schematic, or complete technical document is redistributed here; the authoritative reference files remain linked at Valve's repository. Future reuse of any Valve-licensed design files must comply with the upstream license.

Any other trademarks, product names, or company names mentioned in this repository (e.g. OmniVision, Snapdragon/Qualcomm) belong to their respective owners and are used for identification purposes only.
