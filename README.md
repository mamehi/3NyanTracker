<div align="center">

# 🐱 3NyanTracker

### MIPI-Direct Mouth Tracker for Steam Frame

*A concept-stage, hardware-only, open accessory design*

[![License: 3NyanTracker HDL 1.0](https://img.shields.io/badge/License-3NyanTracker%20HDL%201.0-lightgrey.svg)](./LICENSE)
![Status](https://img.shields.io/badge/status-concept%20%2F%20pre--CAD-orange)
![Target](https://img.shields.io/badge/target-Valve%20Steam%20Frame-1b2838)
![Scope](https://img.shields.io/badge/scope-hardware--only-blue)

</div>

---

## ⚡ TL;DR

| | |
|---|---|
| **What** | A mouth/lower-face camera module, MIPI CSI-2 direct to the Steam Frame's expansion port |
| **What it's not** | Software. Eye tracking. Affiliated with any tracking project. |
| **Status** | Concept only — blocked on Valve's official port spec |

---

## 📖 Table of Contents

- [Summary](#-summary)
- [Scope](#-scope)
- [Steam Frame Reference](#-steam-frame-reference)
- [Expansion Port](#-expansion-port)
- [Design Goals](#-design-goals)
- [Hardware Overview](#-hardware-overview)
- [Status & Roadmap](#-status--roadmap)
- [Bill of Materials](#-bill-of-materials-draft)
- [Open Questions](#-open-questions)
- [Contributing](#-contributing)
- [License](#-license)
- [Changelog](#-changelog)
- [Project Info](#-project-info)

---

## 📝 Summary

**3NyanTracker** is a concept-stage, open hardware design for a
mouth/lower-face camera module connecting through the Steam Frame's
front expansion port via **MIPI CSI-2** — no USB bridge, no external
compute board.

> **🔧 Hardware only.** This repo defines a camera module and its
> physical/electrical interface to the Frame, and nothing else. It
> does not include, require, or endorse any tracking software or
> client. Consuming the raw video output is left entirely to
> whoever wants to build that — this project has no opinion on it
> and isn't affiliated with any software project.

It's published now, ahead of Valve's official CAD/pinout release,
mainly to put a timestamped concept on record and invite
hardware-side feedback before real development starts.

## 📦 Scope

**✅ In scope**
- Camera module hardware
- Mounting
- Physical/electrical interface to the expansion port
- Raw video output — mouth/lower-face only

**❌ Out of scope**
- Tracking algorithms, calibration, any client software
- DRM/auth circumvention on the expansion port

> **👁️ Not covered here: the Frame's built-in eye-tracking
> cameras.** This project doesn't touch them in any way — no
> hardware, firmware, or software work on them happens here.
> Several other public repos already cover eye tracking; send
> anything related to that their way instead.

## 🥽 Steam Frame Reference

Specs live on Valve's own pages, linked rather than copied so this
doesn't go stale:

- 🔗 [Product page](https://store.steampowered.com/hardware/steamframe)
- 🔗 [Developer docs](https://partner.steamgames.com/doc/steamframe)

What actually matters for this project: SoC is Snapdragon 8 Gen 3,
battery is 21.6Wh with no official runtime published (early reports
suggest it's short) — **assume tight power headroom** for any
add-on hardware.

## 🔌 Expansion Port

- Nose of the headset, user-accessible
- 1-lane PCIe Gen4 + a MIPI camera interface (reported as dual
  2.5Gbps lanes; some sources say up to 8 MIPI lanes total). Exact
  pinout **not officially published yet**
- Valve has named face tracking, depth sensors, full-body tracking,
  and color passthrough as example use cases, and says CAD files
  are coming
- **Proof the port works in practice:** Arcturus Industries (who
  built the Frame's internal camera system) already shipped a color
  passthrough module through it as an official "Steam Frame
  Compatible" accessory, ahead of any public CAD

## 🎯 Design Goals

- MIPI CSI-2 direct — no USB bridge
- Mouth/lower-face only — no eye-tracking function attempted
- Camera + any IR illumination face the mouth, physically clear of
  the built-in eye cameras
- Minimal, low-BOM single-camera design — small-batch/DIY friendly
- Raw video output only; downstream processing is someone else's job

## 🛠️ Hardware Overview

> Draft direction — will firm up once Valve's port spec is public.

- MIPI CSI-2 camera module *(small-format, IR-sensitive; sensor TBD)*
- Optional mouth-facing IR illumination
- Minimal interface PCB: module's native MIPI → Frame's expansion port
- 3D-printed mount on the Frame's front housing

## 🗺️ Status & Roadmap

| Phase | What | Status |
|:---:|---|:---:|
| 0 | Concept + problem statement, block diagram | ✅ Done |
| 1 | Camera/connector selection | 📋 Planned |
| 2 | Valve's official port pinout/electrical spec | 🚧 Blocked, waiting |
| 3 | PCB draft, MIPI-direct hardware | 🚧 Blocked on Phase 2 |
| 4 | Prototype (raw output only) | 📋 Planned |
| 5 | First small-batch build | 📋 Planned |

## 💰 Bill of Materials (Draft)

<details>
<summary>Click to expand — placeholder, not a committed price</summary>

| Component | Est. Cost | Notes |
|---|:---:|---|
| MIPI CSI camera module | TBD | Sensor under evaluation |
| Interface PCB | TBD | Minimal, single-purpose |
| IR LED(s) | TBD | Optional, mouth-facing |
| Mount/housing | TBD | 3D-printed initially |
| Cable/connector | TBD | Pending official port spec |

</details>

## ❓ Open Questions

- Exact expansion port pinout/voltage/protocol — unknown until
  Valve publishes it
- Whether the port needs any auth/handshake for third-party MIPI
  devices to be recognized by SteamOS — unconfirmed
- Thermal/battery impact of an active camera on an already
  power-tight platform — unverified
- Whether any given tracking software can actually consume this
  module's raw output depends entirely on that software, not on
  anything this project controls

## 🤝 Contributing

Issues and PRs welcome — **hardware-related only** (mechanical,
PCB, component selection). Software integration belongs in a
separate, unaffiliated project. If you have early access to Valve's
port docs, that's especially useful.

## ⚖️ License

<div align="center">

**3NyanTracker Hardware Distribution License 1.0**
*(Apache 2.0 base + custom Section 10)* — [full text](./LICENSE)

</div>

| | |
|---|---|
| ✅ Personal use, modification, reverse engineering | Always allowed, explicitly stated |
| ❌ Commercial manufacture or sale | Not without maintainer's written permission |
| 📌 Physical attribution | Must be kept on any built/conveyed unit (e.g. QR code to this repo, silkscreened on the PCB) |
| 🔁 Source availability (GPLv3-style) | If you **convey** any built unit to anyone — even one, even free — you must make the Corresponding Source for it publicly available under this same license, and that obligation carries through every downstream derivative |
| 🔒 No further restrictions | You can't bolt on extra terms of your own on top of this license |

Just building one for yourself and never handing it to anyone else?
None of the source-availability or attribution terms are triggered —
only *conveying* a unit to a third party does that.

## 📅 Changelog

- **2026-09-18** — Initial commit. Concept, goals, roadmap.
  Hardware-only scope; no software integration implied.

---

## ℹ️ Let's Stay in Touch!

| | |
|---|---|
| **License** | 3NyanTracker Hardware Distribution License 1.0 — see [LICENSE](./LICENSE) |
| **First published** | 2026-09-18 |
| **Maintainer** | Samsacknyan · `rumored-prosy-9j@icloud.com` |

---

™️ Trademark & Third-Party Notice

"Steam," "Steam Frame," "SteamOS," "SteamVR," and related logos are trademarks and/or registered trademarks of Valve Corporation in the US and/or other countries. This project is an independent, fan-made, unofficial concept, and is not affiliated with, sponsored by, or endorsed by Valve Corporation.

References to Valve, Steam, or Steam Frame in this repository (including specifications, product names, and links to Valve-operated pages) are made solely to describe hardware compatibility and are believed to fall under fair/nominative use. No proprietary Valve documentation, CAD files, or other confidential/partner-only material is reproduced, copied, or derived from in this repository. All such references point to Valve's own publicly accessible pages rather than reproducing their content.

Any other trademarks, product names, or company names mentioned in this repository (e.g. Arcturus, Snapdragon/Qualcomm) belong to their respective owners and are used here for identification purposes only.
