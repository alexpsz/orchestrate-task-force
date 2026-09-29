---
name: orchestrate-task-force
description: "Coordinate independent work packages with user-requested visible tasks (Codex chats, Claude Code sessions, or Antigravity subagents), bounded helpers, adaptive concurrency, and integrated acceptance. Use for execution, monitoring, or read-only orchestration audits. Loading it does not authorize new tasks or helpers."

---

# Orchestrate Task Force

Coordinate only where independent work or integration benefits from separate ownership. Keep a small, coherent task with its current owner.

## Choose the workflow

Follow platform/tool contracts, explicit user decisions, project instructions and authoritative state, then this skill. Delegation never expands authorization. External, protected, or destructive actions need matching authority already present or obtained for that action.

Distinguish execution from audit and monitoring. An audit inspects permitted evidence without visible-task dispatch or state changes; permitted internal helpers stay read-only. Monitoring follows authorized existing work until completion, required input, or a concrete blocker.

Create new visible tasks only when explicitly requested and supported. Reuse suitable existing owners. Loading the skill alone does not authorize task creation. An agreed visible owner survives handoffs and context summaries; internal helpers may assist but cannot replace it. Confirm real task IDs before reporting visible dispatch as complete. If the host cannot provide a required visible owner, explain the gap and keep dependent work pending.

When grouping is requested, place the coordinator and owner tasks in one named section and verify membership. Reuse that section on continuation. Grouping failure preserves the existing tasks.

## Assign independent outcomes

Read the relevant project instructions and current state. Check existing owners, local changes, and the capabilities each worker actually needs. Do not assume a child inherits the parent's access or restrictions.

Define each package in concise natural language: outcome, owner, baseline, allowed write scope, dependencies, needed resources, acceptance checks, and expected return. Put no-write prerequisites in the initial prompt, since dispatch may start execution immediately. Give workers enough context to act without transferring unrelated history. Combine or sequence work whose shared decisions or writes cannot be isolated.

Each conflicting mutable target has one writer. Independent writers may run concurrently; shared files, schemas, databases, caches, ports, devices, and external records require isolation or serialization. The coordinator does not write into a worker's reserved scope. A waiting, blocked, or unobserved writer retains its reservation until release is confirmed. A timeout, stop request, or archived chat alone does not prove release.

## Schedule from current conditions

This skill sets no fixed task, reader, writer, or nesting count. Use live host limits, applicable user/project constraints, dependencies, write isolation, and resource pressure. Count coordinators, waiting owners, and helpers according to the host's actual definitions.

Dispatch useful ready work while the coordinator advances independent work or integration. Reconsider capacity as dependencies clear or resources change. Do not create filler tasks or ask again solely because several authorized units can run concurrently. Explain material resource or cost pressure before unusually large fan-out.

Preserve the user's model and effort choices; otherwise use host defaults. When configuration changes are permitted and useful, select supported settings for the actual reasoning problem. Keep the active turn stable and make changes at a supported checkpoint; do not alter global settings to route a package. If acceptance requires an exact configuration, verify it before dependent writes; report unsupported or unobservable settings and continue independent work. Missing facts, ordinary test failures, and resource waits call for retrieval, repair, or scheduling. A named model preset is optional, never implied by using this skill.

## Continue and recover

Use the host's task lifecycle and compact status updates. Distinguish planned, pending, active, delivered, and accepted work. A creation acknowledgement is not proof of readiness, and a worker's completion claim is not acceptance evidence. Inspect uncertain state before retrying or replacing an owner.

Route corrections to the existing owner when possible. Update affected contracts after user changes and reject results based on superseded requirements. Confirm old writers and exclusive resources are released before replacements write.

Before handoff, a long pause, or context loss, preserve a short recovery note: objective, current constraints and authorization, owner/group IDs, baseline, verified results, unresolved work, retained resources, and next action. On resumption, check it against live state. Keep it in the existing task or authorized project context; no separate ledger is required.

## Integrate and finish

Workers return their artifact or findings, targeted validation, unrun checks, and remaining concerns. Inspect those results against the package contract. Integrate accepted work and perform one cumulative acceptance check for the declared critical properties. Add independent review or broader checks only for a specific unresolved risk, material change, failure, or project requirement.

Map every current user requirement, including later corrections, to evidence or an explicit unfinished status. Report the integrated result, owners, checks, unresolved risks, and external-action status. Finish missing evidence with the existing owner where possible. Close or explicitly transfer owned processes and resources; never terminate unrelated work by a broad pattern.

Keep private project names, paths, real task IDs, credentials, and runtime records out of reusable skill files and public examples. Keep recommendations, requested settings, observed configuration, and measured outcomes distinct. Unavailable evidence is not a successful check.

## Read only what applies

- For Codex visible tasks or sidebar grouping, read [codex-profile.md](references/codex-profile.md).
- On Claude Code hosts (CLI, desktop Code tab, or web), read [claude-profile.md](references/claude-profile.md) before dispatching helpers or sessions, grouping, messaging, or changing configuration.
- On Google Antigravity hosts (IDE or Desktop), read [antigravity-profile.md](references/antigravity-profile.md) before dispatching subagents, using workspace isolation, or reporting Auxiliary Pane state.
- Only when the user explicitly selects the Astra preset, read [astra-effort-preset.md](references/astra-effort-preset.md). Do not load it for ordinary orchestration. On Claude or Antigravity hosts, follow their respective profiles instead; the preset's model is unavailable there.
- For an unclear routing or recovery decision, read [decision-guide.md](references/decision-guide.md).
- For skill maintenance, use [behavior-cases.md](evals/behavior-cases.md). These are review scenarios, not benchmark results.
