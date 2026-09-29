# Optional GPT-6 Astra Effort Preset

Load this file only when the user explicitly selects this preset. It is an optional routing preference, not a requirement for the skill or evidence of superior quality, latency, or cost. Normal orchestration preserves user choices and host defaults.

## Scope

For newly dispatched workers covered by the user's choice, use `gpt-6-astra` where the active tool permits it. Preserve the root's existing settings and later explicit overrides. Never change global settings. The preset does not authorize a new task, model substitution, or an unsupported configuration.

If a tool requires explicit user model choice, the user's request must identify GPT-6 Astra; the agent choosing to read this file is insufficient. If the selected model or setting is unavailable, report the limitation rather than silently substituting.

## Effort choices

| Setting | Starting point within this preset |
| --- | --- |
| medium | Settled requirements and reliable checks, including routine work |
| high | Coupled design decisions or complex root-cause analysis |
| xhigh | A named serious failure that existing checks can miss, or a demonstrated semantic failure needing deeper analysis |
| max | An unusually hard remaining reasoning problem with adequate evidence and acceptable latency |
| ultra | Only where the host defines and supports it, and its delegation behavior benefits useful independent work |

This preset does not automatically choose low; a user's explicit choice still takes precedence. Effort does not grant authority, extra slots, or permission to nest. Any supported effort may use helpers when the host allows them; no setting requires filler agents. Ordinary test failures, missing facts, and resource waits do not trigger an upgrade.

## Configuration evidence

Distinguish recommended, requested, and observed effective settings. Mark unobservable settings as unverified and known differences as mismatches. Gate only work whose acceptance requires the exact setting; do not repeatedly recreate tasks to repair an observation gap.

Keep active turns stable. Change settings only at a supported, authorized checkpoint; release writers and exclusive resources before a replacement starts. Apply the current tool's fork/inheritance rules. Do not infer a desktop switching feature or an API effort value from a different interface.
