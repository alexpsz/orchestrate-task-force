# Antigravity Task and Subagent Adapter

This adapter maps the core to Google Antigravity (AGY) hosts: the Antigravity IDE and Antigravity 2.0 Desktop. It selects no model. Discover live platform tools and follow their schemas; unavailable operations stay unavailable. Tool contracts were verified on 2026-09-29 and must be rechecked when used.

## Respect host contracts

Host instructions outrank this skill. Delegation never expands authorization: actions denied to the coordinator must never be routed to child subagents, and permissions remain scoped to individual sessions. Subagents start in isolated conversation contexts without the coordinator's history; provide a self-contained package prompt with clear baseline, write scope, dependencies, and acceptance checks. Put no-write prerequisites upfront, since dispatch starts execution immediately.

## Use internal helpers

The `invoke_subagent` tool launches autonomous workers that report back to the coordinator. Choose `TypeName: "research"` for read-only analytical packages or pre-implementation audits; choose `TypeName: "self"` for execution workers requiring file modifications and terminal access. Use `define_subagent` when a specialized role needs a custom system prompt or restricted toolset (`enable_write_tools`, `enable_mcp_tools`, `enable_subagent_tools`).

Concurrent writers in a git repository use `Workspace: "branch"` (isolated cloned branch) for verified filesystem isolation; integrate by validating and merging their branches. `Workspace: "share"` creates a workspace sharing the repository directory (similar to a git worktree or Mercurial share) to avoid duplicating storage. Verify separate working directories/checkouts before allowing overlapping file edits. Otherwise require disjoint write scopes or serialize writers. Shared repository storage alone neither proves nor disproves working-file isolation. `Workspace: "inherit"` shares the caller's working directory and is reserved for read-only workers or strictly disjoint file edits.

Workers run in the background. The runtime delivers messages automatically and wakes the coordinator reactively when each worker finishes or reports. Advance independent work meanwhile; do not poll, sleep, or predict pending results. Send updates or corrections to an existing worker with `send_message(Recipient: <conversationId>, Message: "...")` rather than replacing it. A timeout or stop request does not prove release: inspect the workspace and active tasks before a replacement writes.

## Resolve owners before dispatch

Use `manage_subagents(Action: "list")` to inspect live direct subagents, their roles, conversation IDs, transcripts, and execution states (`running`, `idle`, `waiting_for_input`, `waiting_for_dependents`, `waiting_for_message`, `canceling`, `errored`). Check existing subagents and local changes before dispatching new ones; reuse existing owners where possible.

## Create and verify visible sessions

Create subagents only for explicitly requested new work packages. Specify a descriptive `Role` (2–5 words, e.g., "Metrics Module Specialist", "Schema Migrator") and a concise natural language contract in `Prompt`.

Subagents appear immediately in the Antigravity Auxiliary Pane under the **Subagents** tab, providing visible tracking and transcript logs at `<appDataDir>\brain\<conversationId>\.system_generated\logs\transcript.jsonl`. When referencing subagents in chat or handoff reports, use clickable conversation links: `[Role](conversation://<conversationId>)`.

If subagent invocation is unavailable, explain the gap. Do not substitute hidden background commands for a requested visible owner; keep dependent work pending and continue independent authorized work.

Preserve user configuration. Workers default to `Model: "inherit"`; select `"flash"` or `"pro"` only for a concrete reasoning need or when explicitly requested. Never change global configuration to route a package.

## Group and read back

Antigravity groups subagents natively under the active conversation within the Auxiliary Pane (`Subagents` tab). The host does not provide arbitrary user-created sidebar section tools (such as Codex's `create_sidebar_section` or Claude's `create_group`).

When sidebar grouping is requested, report this grouping gap, retain the visible subagents, and maintain membership and role mapping in the coordinator's note. Grouping limitations do not invalidate visible subagents or authorization.

## Follow through and recover

Message subagents with `send_message` addressed by `conversationId`. Do not use `send_message` to communicate with the user; communicate with the user via standard chat output. Workers transmit deliverables and validation evidence back to the coordinator. Do not loop on `manage_subagents` status or send "are you done?" inquiries.

Before terminating workers, inspect their deliverables, verify reported checks against the contract, and ensure required code and generated files are integrated or safely persisted. Terminating a subagent with `manage_subagents(Action: "kill", ConversationIds: [...])` permanently deletes its branched workspace (`Workspace: "branch"`) while preserving its transcript log and conversation artifacts; unintegrated workspace changes will be lost. Target only verified, completed subagents owned by this workflow. Never use `Action: "kill_all"` as a routine cleanup pattern, as it terminates all active direct subagents across the host session, including unrelated tasks.

To prevent context loss in long orchestrations or before handoff, write the recovery note into the conversation, or optionally save structured coordination artifacts in `<appDataDir>\brain\<conversationId>\` using `write_to_file`. Artifacts provide a host-native persistence format for inspection without context flooding, but are not a mandatory run ledger. On resumption, reconcile recorded state against live status (`git status`, `manage_subagents`) before dispatching replacements.

## Models and effort

No preset applies. Keep the user's model choices and host defaults (Gemini Flash, Pro, or Flash-Lite). The [GPT-6 Astra preset](astra-effort-preset.md) targets GPT models: if selected on an Antigravity host, report that it is unavailable and ask whether to keep defaults or specify a supported Gemini model; do not map effort levels onto Antigravity models silently.
