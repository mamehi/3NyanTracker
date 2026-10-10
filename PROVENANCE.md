# 3NyanTracker provenance

Copyright 2026 Samsacknyan. This original record is licensed under the [3NyanTracker Hardware Distribution License 1.0](LICENSE).

## Project and evidence

- Project: **3NyanTracker**
- Original creator: **Samsacknyan**
- Repository: [mamehi/3NyanTracker](https://github.com/mamehi/3NyanTracker)
- Evidence reviewed: the available main-branch Git history through `fa4db366caf153d8a357682b6571073484a82499`, its file contents, and GitHub repository metadata.

The earliest commit in the available history is **af3aef305aaa15314d18c60fefd156c3c57981de**, authored by Samsacknyan. Both its author and committer timestamps are **2026-09-18T19:10:30+09:00** (2026-09-18T10:10:30Z). Its permanent public GitHub URL is:

https://github.com/mamehi/3NyanTracker/commit/af3aef305aaa15314d18c60fefd156c3c57981de

GitHub's [repository API](https://api.github.com/repos/mamehi/3NyanTracker) reports `created_at` as `2026-09-18T10:10:29Z`; the repository is currently public. These records support September 18, 2026 as the project's recorded start date and are consistent with the README's initial-publication date. Git timestamps record author and committer dates, not the time a commit was first pushed or a repository first became public. The exact historical public-release time is not independently established by the available records. The earliest commit is publicly accessible now; its timestamp is not proof of its first public availability.

## Original concept and architecture

The first commit contains only README.md. Its original Simplified Chinese description is preserved here exactly:

> 3Nyantracker - SteamFrame是一款基于内置Mipi终端的面部表情追踪和Mipi通信设备。它集成了Mipi CSI设备管理、视频处理和OSC数据传输功能，使其适用于VRChat虚拟形象的动画和表情控制。

The [same-day README revision](https://github.com/mamehi/3NyanTracker/commit/a663c153f5a19636335dff3f51a5d5a7c0939158) narrows the documented scope to a hardware-only, mouth/lower-face camera module connected directly through the Steam Frame front expansion port over MIPI CSI-2, without a USB bridge or external compute board. It describes an IR-sensitive camera with the sensor still undecided, optional mouth-facing IR illumination, a minimal interface PCB, and a proposed 3D-printed front mount. Raw-video consumption is outside that revision's hardware scope. This distinction preserves the initial description and records how the scope developed.

The October 10 technical revision proposes one OV7251 monochrome global-shutter camera, one 940 nm IR LED, power regulation, an identification EEPROM, and a paddle/flexible interconnect. These are documented design proposals, not evidence of a validated prototype or manufactured hardware.

## Verified milestones

Dates below are Git author timestamps; the corresponding committer timestamps match for these commits. Times use the recorded +09:00 offset. Each SHA links to its permanent commit record.

| Recorded time | Commit SHA | Verified milestone |
|---|---|---|
| 2026-09-18 19:10:30 +09:00 | [af3aef305aaa15314d18c60fefd156c3c57981de](https://github.com/mamehi/3NyanTracker/commit/af3aef305aaa15314d18c60fefd156c3c57981de) | Initial README and project concept; no standalone LICENSE file in this tree. |
| 2026-09-18 19:28:55 +09:00 | [a663c153f5a19636335dff3f51a5d5a7c0939158](https://github.com/mamehi/3NyanTracker/commit/a663c153f5a19636335dff3f51a5d5a7c0939158) | Hardware-only MIPI mouth-camera scope and custom HDL 1.0 name and licensing provisions documented in README. |
| 2026-09-18 19:30:44 +09:00 | [1e3f69fa33b05732068b1f1e4474a2bcd079413c](https://github.com/mamehi/3NyanTracker/commit/1e3f69fa33b05732068b1f1e4474a2bcd079413c) | Full custom license added as LICENSE.md during the initial publication day's development. |
| 2026-09-18 19:45:27 +09:00 | [0e8d1e9ca6498e27ff8ec937fde019d7685b83ff](https://github.com/mamehi/3NyanTracker/commit/0e8d1e9ca6498e27ff8ec937fde019d7685b83ff) | LICENSE.md renamed to LICENSE with 100% identical contents. |
| 2026-09-21 13:25:13 +09:00 | [27bbc6220488ad6f652cf49d5a8107fa46249298](https://github.com/mamehi/3NyanTracker/commit/27bbc6220488ad6f652cf49d5a8107fa46249298) | Contact-section heading edited; no license or hardware change. |
| 2026-10-10 12:09:52 +09:00 | [c7e6bdef9bbb223a35dc263f2b5cd64969abbb5e](https://github.com/mamehi/3NyanTracker/commit/c7e6bdef9bbb223a35dc263f2b5cd64969abbb5e) | README expanded with Valve reference links, proposed OV7251/single-IR-LED baseline, electrical/mechanical planning, and unverified integration risks. |
| 2026-10-10 12:28:57 +09:00 | [fa4db366caf153d8a357682b6571073484a82499](https://github.com/mamehi/3NyanTracker/commit/fa4db366caf153d8a357682b6571073484a82499) | License introduction and README explanations clarified; hardware safety notice added. Sections 1-10 of LICENSE unchanged. |

This provenance document is a later record of those milestones. Its creation date is recorded by the commit adding it; it is not backdated to the project's start.

## Original license history

The custom **3NyanTracker Hardware Distribution License 1.0** is documented in the initial publication day's history, not introduced by the October documentation clarifications. The earliest commit itself has no license file; the same-day README explicitly names the license before the full text is committed. This records what the available history establishes without pretending that LICENSE existed in the first tree.

The original full text can be inspected at the permanent file URL:

https://github.com/mamehi/3NyanTracker/blob/1e3f69fa33b05732068b1f1e4474a2bcd079413c/LICENSE.md

Its initial provisions already include:

- Non-commercial use and separate written permission for prohibited commercial manufacture, sale, and distribution (Section 10(b)).
- Modification and redistribution permissions and notice retention (Sections 2 and 4, subject to Section 10), plus express reverse-engineering permission (Section 10(a)).
- Physical attribution on units distributed to third parties (Section 10(c)).
- Corresponding Source for conveyed units, supplied to the recipient with the unit or through a durable public link, maintained while conveyance continues and for at least three years from conveyance (Section 10(d)(2)).
- The same source obligations for downstream derivative hardware designs, with notices and descriptions of modifications (Section 10(d)(3)-(4)).
- No further restrictions, enforcement/termination provisions, and warranty/liability disclaimers (Sections 7-10).

The September 18 rename is purely editorial. Comparing the original LICENSE.md with the October 10 LICENSE shows that the introductory paragraphs changed, but the full text from `TERMS AND CONDITIONS FOR USE, REPRODUCTION, AND DISTRIBUTION` through the copyright/contact footer is byte-for-byte identical. The new introduction correctly describes the license as custom, explains the already modified Sections 1-9, and acknowledges separate third-party licenses. The operative provisions were not introduced or amended by that clarification. The original introduction's description of Sections 1-9 as reproduced Apache text was inaccurate even in the original file.

The October README source-delivery explanation was aligned with the already-existing Section 10(d)(2): delivery to the recipient can include source with the unit, rather than always requiring public hosting. This was a correction to the summary, not a new license entitlement. No substantive change to the numbered license provisions is found in the reviewed history. Any future substantive license change should be recorded separately with its actual date, scope, and affected materials; editorial explanations must not be used to imply retroactive changes.

This documentation update leaves the existing root LICENSE unchanged and preserves all historical commits.

## Sources and material origin

The October 10 technical README records the following external references. Their appearance in the documentation establishes a cited source, not proof of when an author first read it or of copying a particular design file.

| Source | Documented role and licensing boundary |
|---|---|
| [Valve Steam Frame product page](https://store.steampowered.com/hardware/steamframe) and [developer documentation](https://partner.steamgames.com/doc/steamframe) | Product/platform context; linked sources retain their own terms. |
| [Steam Frame Hardware Reference](https://gitlab.steamos.cloud/SteamHardware/SteamFrame) and [front expansion-port specification](https://gitlab.steamos.cloud/SteamHardware/SteamFrame/-/blob/master/documents-expansion-port/20261001_External_Interface_Front_Port.pdf) | Cited electrical/mechanical interface planning source. The filename is not independent proof of a publication date. Valve digital plans/drawings carry the terms in its [license.txt](https://gitlab.steamos.cloud/SteamHardware/SteamFrame/-/blob/master/license.txt), including CC BY-NC-SA 4.0. |
| [Linux ov7251.c](https://github.com/torvalds/linux/blob/master/drivers/media/i2c/ov7251.c) | Linked driver reference for sensor/clock feasibility; not redistributed here and not relicensed by this repository. Its own upstream terms apply to any future code reuse. |

The reviewed baseline tracks README.md and LICENSE only; no PCB, KiCad, CAD, schematic, or Valve design file is present. Future design files require an origin assessment rather than an assumption of independent authorship. See [LICENSES.md](LICENSES.md) for file-level policy and upstream attribution guidance.

## What this record establishes

These records establish documented authorship claims and development history, not exclusive ownership of an abstract idea, verified prototype functionality, or legal priority over independently created designs. Copyright can protect qualifying original expression in documents and design files; abstract ideas, systems, and methods themselves are outside that protection. See the [U.S. Copyright Office explanation](https://www.copyright.gov/help/faq/faq-protect.html); applicable law determines protection in a particular case.

This project is independent and unofficial. Citing Valve references does not imply affiliation, sponsorship, certification, or endorsement, and does not transfer Valve's rights to Samsacknyan.
