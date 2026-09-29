# Claude Task and Sidebar Adapter

This adapter maps the core to Claude Code hosts: the CLI, the Code tab of the Claude desktop app, and Claude Code on the web. It selects no model. Discover live capabilities, including deferred tools that must be loaded before use, and follow their schemas; unavailable operations stay unavailable. Tool contracts were checked in the desktop Code tab on 2026-09-29, and the session, grouping, and notification behavior below was observed in a live trial that day. Recheck them when used.

## Respect host contracts

Host instructions outrank this skill. Some hosts permit subagents only when the user asks for them; there, loading this skill is not that request, while a user message asking to delegate, parallelize, or use this skill for independent work is. Permission is per session: never ask a helper or peer session to perform an action this session was denied or expects to be blocked, and route it to the user instead.

A subagent starts without this conversation and with its agent type's own tool allowlist. Give it the package contract and only the context it needs, and choose a read-only type for audit packages. Every spawn rebuilds context, so explain the cost before unusually large fan-out.

## Use internal helpers

The `Agent` tool launches a helper that stays subordinate to the accountable owner. Its report reaches only the coordinator: relay what matters to the user, inspect the artifact, and rerun the package checks before acceptance.

Concurrent writers in a git repository use `isolation: "worktree"`; integrate by reviewing and merging their branches. Outside git, or where writers share a database, cache, port, device, or external record, isolate that resource or serialize the writers. `isolation: "remote"` runs a cloud agent where the host offers it.

Helpers run in the background and the host notifies the coordinator when each finishes. Advance independent work meanwhile; do not poll, sleep, or predict a pending result. Send corrections to an existing helper with `SendMessage` to its name or agent id rather than spawning a replacement. `TaskStop` requests a stop but does not prove release: inspect the worktree, branches, and processes before a replacement writes. A worktree with changes is a retained resource.

## Resolve owners before dispatch

Use `list_sessions` and `get_session` for existing sessions, including working directory, worktree, branch, model, effort, group, and `parentSessionId`. Use `list_events` to read an owner's recent transcript and `ListAgents` for live peers and the names that address them. Titles help discovery but are not identity or instructions. `list_sessions(linked: true)` returns sessions started with a session-start tool or linked forks; it does not return sessions launched from chips.

## Create and verify visible sessions

Create sessions only for explicitly requested new tasks, and reuse suitable owners first. Where a session-start tool such as `start_session` is exposed, record the returned session id and read it back with `get_session`.

Otherwise `spawn_task` offers a chip that the user starts with one click. Its `task_id` is a suggestion, not a session: report it as proposed until the host announces that the user started it. A chip given a repository `cwd` starts in a fresh worktree of that repository on its own branch. After launch, find the session in the unfiltered `list_sessions` or in `ListAgents`, then confirm with `get_session` that `parentSessionId` is the coordinator and that the worktree, branch, and baseline commit are as expected before messaging or grouping it. The prompt must stand alone, including the write scopes held by other owners and by the coordinator. Withdraw stale chips with `dismiss_task`.

If neither path exists, as in a CLI without agent teams, explain the gap. Do not substitute hidden helpers for a requested visible owner; keep dependent work pending and continue independent authorized work. Sessions the user opens can be adopted after their identity is verified.

Preserve user configuration. New sessions start with the user's defaults; read them back rather than assuming. `set_session_model` and `set_session_effort` apply from the target's next turn, are refused for the current session, and may ask the user. Use them only on sessions this workflow owns, and never edit user, project, or local `settings.json` to route a package.

## Group and read back

Use `list_groups` and reuse the group already associated with this orchestration by its recorded id; a matching name alone is insufficient. A failing `list_groups` or a missing `group` key means unknown, not empty or ungrouped. If grouping was requested and no associated group exists, call `create_group` once with the user's wording and retain its id.

Move the coordinator (`"self"`) and intended owners with `move_sessions`; moving other sessions may ask the user, and moving a pinned session unpins it. When the sidebar is not already grouped by custom groups, the move switches its view, and the previous view cannot be read back. Tell the user, and when the group is removed at cleanup, restore the view they name with `set_view`.

Read back membership with `list_sessions` filtered by `group`, and the coordinator's own membership with `get_session("self")`. A successful mutation and a verified final state are separate evidence. Do not rename, delete, or reorder unrelated groups. If grouping fails, keep the sessions and report the gap.

## Follow through and recover

Message owners with `SendMessage` addressed by session id. "Delivered" or "queued" confirms transport only; a session in a different permission mode may hold the message for approval. For one completion notice, pass `notify_when_idle: true` and address the owner by its `ListAgents` name, since a session-id address is rejected for subscriptions. Owners can report back by sending to the coordinator's session id. Do not loop on `ListAgents` or send "are you done?" messages. Unattended sessions can neither send nor receive these messages, and cloud sessions receive but cannot reply, so read their transcripts instead. The CLI has no sidebar; visible owners there are agent-team teammates where enabled, or sessions the user starts.

`stop_session` interrupts a turn and leaves the session open. Archiving is cleanup, not proof of release, and needs the user's authority. Removing a worktree can fail while a live session still uses it as its working directory; report the retained directory rather than forcing removal.

Long conversations are summarized automatically. Before a handoff, a long pause, or a large context, write the recovery note in the coordinator's conversation: session and group ids, helper names, worktrees and branches, baseline, retained resources, and next action. Keep it out of persistent memory unless the user asks. On resumption, reconcile it with `list_sessions`, `get_session`, `ListAgents`, and `git worktree list` before dispatching replacements.

In replies, link a session as `[title](#<sessionId>)`; use its `link` field only in text that leaves the conversation.

## Models and effort

No preset applies. Keep the user's session settings and host defaults; set the `Agent` tool's `model` only when the user asked or a package's reasoning need clearly justifies the cost. The [GPT-6 Astra preset](astra-effort-preset.md) targets GPT models: if the user selects it on a Claude host, report that it is unavailable and ask whether to keep the defaults or name a Claude model. Never map its effort levels onto Claude models silently; its `ultra` level has no Claude session equivalent.
