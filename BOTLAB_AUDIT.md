# ROB550 Botlab comparison audit

Compared the local `f26` Markdown pages with the current source for [ROB550 Botlab](https://rob550-docs.github.io/docs/botlab/) on September 2, 2026.

## Matching page pairs

The following pages have local equivalents. Apart from navigation metadata, local permalinks, and image/link paths adjusted for this site, their instructional content matches the ROB550 source unless noted below.

| Published ROB550 page | Local equivalent | Difference |
| --- | --- | --- |
| `checkpoints/checkpoint0.md` | `f26/checkpoints/checkpoint0.md` | The local page removes the sentence about BotLab being more intensive than ArmLab and changes “No submission is required” to “See Canvas for submission requirements.” |
| `checkpoints/checkpoint1.md` | `f26/checkpoints/checkpoint1.md` | No content difference; only navigation and image paths differ. |
| `checkpoints/checkpoint2.md` | `f26/checkpoints/checkpoint2.md` | The ROB550 Design Lab announcement/link is commented out locally. The associated published `design-lab.md` page is not present locally. |
| `checkpoints/checkpoint3.md` | `f26/checkpoints/checkpoint3.md` | No content difference; only navigation and the SLAM-toolbox link differ. |
| `checkpoints/checkpoint4.md` | `f26/checkpoints/checkpoint4.md` | The local page changes “No submission is required” to “See Canvas for submission requirements.” |
| `checkpoints/competition.md` | `f26/drafts/competition.md` | Content matches, but the local copy is a draft and therefore is not a published checkpoint page. |
| `get-started.md` | `f26/resources/get-started.md` | No content difference; navigation, internal link, and image paths differ. |
| `how-to-guide/mbot-servo-lib-guide.md` | `f26/resources/how-to-guide/mbot-servo-lib-guide.md` | No content difference; navigation and image paths differ. |
| `how-to-guide/misc.md` | `f26/resources/how-to-guide/misc.md` | No content difference; navigation and image paths differ. |
| `how-to-guide/slam-toolbox-guide.md` | `f26/resources/how-to-guide/slam-toolbox-guide.md` | No content difference; only navigation metadata differs. |
| `mbot-hardware-design.md` | `f26/resources/mbot-hardware-design.md` | No content difference; navigation and PDF paths differ. |
| `mbot-hardware-setup-Pi5.md` | `f26/resources/mbot-hardware-setup-Pi5.md` | The local page intentionally removes the link to the Pi troubleshooting page and leaves a TODO because that page was not migrated. Other differences are navigation and image paths. |
| `mbot-system-setup-Pi5.md` | `f26/resources/mbot-system-setup-Pi5.md` | Step 3 uses the local, fixed current timestamp (`2026-09-02 12:38:04`) and polished wording instead of ROB550’s placeholder timestamp plus replacement instruction. Other differences are navigation, image paths, and minor whitespace. |

## Published ROB550 pages with no local equivalent

- `docs/botlab/index.md` — Botlab landing page
- `docs/botlab/checkpoints/index.md` — Checkpoints landing page
- `docs/botlab/checkpoints/design-lab.md` — Design Lab Guide
- `docs/botlab/how-to-guide/index.md` — How-to Guide landing page
- `docs/botlab/mbot-software-library.md` — MBot Software Library

## Local pages outside the ROB550 Botlab scope

These local pages have no direct counterpart in the published ROB550 Botlab section: `f26/index.md`, `office-hours.md`, `resources.md`, `checkpoints.md`, `schedule.md`, `syllabus.md`, all `f26/drafts/*` pages other than `drafts/competition.md`, and `checkpoints/_template.md`.

