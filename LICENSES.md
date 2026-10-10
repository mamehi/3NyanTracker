# File-level licensing

Copyright 2026 Samsacknyan. This original policy document is licensed under the [3NyanTracker Hardware Distribution License 1.0](LICENSE).

## Policy by material origin

| Material | License |
|---|---|
| Independently developed hardware designs | 3NyanTracker Hardware Distribution License 1.0 (3NyanTracker HDL 1.0) |
| Original KiCad schematics and PCB layouts | 3NyanTracker HDL 1.0 |
| Original CAD and mechanical designs | 3NyanTracker HDL 1.0 |
| Original project documentation | 3NyanTracker HDL 1.0 |
| Valve-authored or Valve-derived files covered by Valve's hardware-reference license | CC BY-NC-SA 4.0 |

Copyright ownership and licensing follow the actual origin and contents of each file. The table describes original materials independently developed by Samsacknyan and Valve materials covered by the upstream license; it does not claim ownership of other authors' work. Other third-party materials retain their own applicable licenses.

The root [LICENSE](LICENSE) remains the existing custom 3NyanTracker Hardware Distribution License 1.0. It is not replaced by Apache 2.0 or Creative Commons. This document explains the licensing boundaries; it does not amend that license or relicense third-party work.

## Independently developed project materials

Original design materials independently developed by Samsacknyan remain under 3NyanTracker HDL 1.0. Its existing provisions cover non-commercial use, modification and redistribution, physical attribution for conveyed units, Corresponding Source availability, and derivative hardware designs. Sections 4 and 10 govern these obligations; the full LICENSE controls over this summary.

Section 10(b) requires the Licensor's separate, explicit written permission for prohibited commercial activity involving the Work or its derivatives. These terms protect covered design materials against unauthorized commercial copying and manufacture within the rights the Licensor can grant. They do not establish exclusive rights to an abstract hardware idea or every independently created implementation of it.

Independently developed files retain their original license when distributed alongside separately licensed materials, provided they are genuinely independent works. Sharing a repository does not itself relicense those files.

## Valve-authored and Valve-derived materials

Valve's [Steam Frame Hardware Reference](https://gitlab.steamos.cloud/SteamHardware/SteamFrame) supplies digital plans and drawings under [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), as stated in its [license.txt](https://gitlab.steamos.cloud/SteamHardware/SteamFrame/-/blob/master/license.txt). Preserve Valve's attribution, original copyright and license notices, source URLs, and indications of previous modifications when copying or adapting covered material. Identify subsequent modifications and their authors. Do not imply Valve affiliation or endorsement.

Valve-authored files and adaptations of those files remain under their applicable CC BY-NC-SA 4.0 terms. Contributions to such adaptations are distributed under CC BY-NC-SA 4.0 in accordance with its ShareAlike terms. The custom 3NyanTracker license does not add restrictions to them: its physical-attribution and Corresponding Source conditions must not be imposed on Valve-derived material. Commercial permissions for Valve-licensed material must come from Valve; permission from the 3NyanTracker maintainer cannot grant Valve's rights.

Directory names, file extensions, a new header, or redrawing an upstream design do not establish independent authorship. Review the actual derivation of a schematic, layout, CAD model, or document, including any copied or adapted expression. A file incorporating Valve-derived design material cannot be classified as independent merely because it is stored separately. Referencing published interface facts alone does not establish that a file copies a protected design; the classification depends on what was actually used.

## Current inventory and future attribution

At the reviewed baseline commit [fa4db366caf153d8a357682b6571073484a82499](https://github.com/mamehi/3NyanTracker/commit/fa4db366caf153d8a357682b6571073484a82499), the repository tracks README.md and LICENSE only. There are no tracked KiCad, PCB, CAD, schematic, or Valve reference files. LICENSES.md and PROVENANCE.md are original project documentation added by this documentation update. The hardware categories above are a policy for future files, not a claim that manufacturing files already exist.

For future hardware files, record author, copyright year, applicable license, original source where relevant, and modifications to upstream material. Prefer a file header or the file's native metadata; where those are unsuitable, use an adjacent attribution record naming the exact file. For upstream material, retain its original notices and identify the source revision or permanent URL and the modification history. Use actual creation years and authors, and distinguish the upstream author from the adapter.

These metadata recommendations do not create additional mandatory requirements for CC BY-NC-SA 4.0 materials. Never mark a Valve-derived design as independently created or replace its upstream notices with a project-wide custom-license label.

See [PROVENANCE.md](PROVENANCE.md) for the verified development and license history and [README.md](README.md) for the technical concept and safety notices.
