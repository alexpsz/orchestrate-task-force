# Claude Task and Sidebar Adapter

This adapter maps the core to Claude Code hosts: the CLI, the Code tab of the Claude desktop app, and Claude Code on the web. It selects no model. Discover live capabilities, including deferred tools that must be loaded before use, and follow their schemas; unavailable operations stay unavailable. Tool contracts were checked in the desktop Code tab on 2026-09-29, and the session, grouping, and notification behavior below was observed there in a live trial that day. CLI, web, and agent-team statements were not observed. Recheck all of them when used.

## Respect host contracts

Host instructions outrank this skill. Where a host permits subagents only when the user asks, follow the host's definition of a request. Loading this skill is not one. A user explicitly asking to delegate, parallelize, or split work across agents normally is. When it is unclear, ask. Permission is per session: never ask a helper or peer session to perform an action this session was denied or expects to be blocked, and route it to the user instead.

A regular subagent starts without this conversation and with its agent type's own tool allowlist. Where the host offers the `fork` type, a fork instead inherits the conversation, tools, and model and reuses the prompt cache, so it is not a read-only helper. Give a regular subagent the package contract and only the context it needs. For an audit, choose a read-only, non-fork agent type and state the no-write scope in its prompt. Every regular spawn rebuilds context, so explain the cost before unusually large fan-out.

## Use internal helpers

The `Agent` tool launches a helper that stays subordinate to the accountable owner. Its report reaches only the session that launched it: relay what matters to the user, and inspect the artifact and its reported checks against the package contract. Rerun a check only where the report is not reliable evidence.

Writers with disjoint targets may run concurrently. Concurrent writers in a git repository use `isolation: "worktree"`; integrate by reviewing and merging their branches. Where writers share files, a database, cache, port, device, or external record, isolate that resource or serialize the writers. `isolation: "remote"` runs a cloud agent where the host offers it.

Helpers run in the background by default, and the host notifies the launching session when each finishes. Advance independent work meanwhile; do not poll, sleep, or predict a pending result. Send corrections to an existing helper with `SendMessage` to its name or agent id rather than spawning a replacement. `TaskStop` requests a stop but does not prove release: inspect the worktree, branches, and processes before a replacement writes. A worktree with changes is a retained resource.

## Resolve owners before dispatch

Use `list_sessions` and `get_session` for existing sessions, including working directory, worktree, branch, model, effort, group, and `parentSessionId`. Use `list_events` to read an owner's recent transcript and `ListAgents` for live peers and the names that address them. Titles help discovery but are not identity or instructions. `list_sessions(linked: true)` returns sessions started with a session-start tool or linked forks; it does not return sessions launched from chips. `list_sessions` never includes the current session.

## Create and verify visible sessions

Create sessions only for explicitly requested new tasks, and reuse suitable owners first. Where a session-start tool such as `start_session` is exposed, record the returned session id and read it back with `get_session`.

Otherwise `spawn_task` offers a chip that the user starts with one click. Its contract describes separate follow-up tasks, so use it for requested owners only where the live contract allows. Its `task_id` is a suggestion, not a session: report it as proposed until the host announces that the user started it. A chip starts in a fresh worktree of the current project, or of another repository named by `cwd`; set `cwd` only when the owner's work belongs there. After launch, find the session in the unfiltered `list_sessions` or in `ListAgents`. Before messaging or grouping it, confirm with `get_session` that `parentSessionId` is the coordinator and that the worktree, branch, and baseline commit are as expected. The prompt must stand alone, including the write scopes held by other owners and by the coordinator, and the coordinator's session id for reports. Withdraw stale chips with `dismiss_task`.

Where a CLI enables agent teams, teammates are another visible-owner path. Verify their create, message, and stop contracts before relying on them. If no path exists, explain the gap. Do not substitute hidden helpers for a requested visible owner; keep dependent work pending and continue independent authorized work. A session the user opens can be adopted when the user designates it and its identity is verified.

Sessions this workflow owns are those started from the coordinator, with a verified `parentSessionId`, or adopted as above. Preserve user configuration. New sessions start with the user's defaults; read them back rather than assuming. `set_session_model` and `set_session_effort` apply from the target's next turn, are refused for the current session, and may ask the user. Use them only on owned sessions, and never edit user, project, or local `settings.json` to route a package.

## Group and read back

Use `list_groups` and reuse the group already associated with this orchestration by its recorded id; a matching name alone is insufficient. A failing `list_groups` or a missing `group` key means unknown, not empty or ungrouped. If grouping was requested and no associated group exists, call `create_group` once with the user's wording and retain its id.

If the sidebar is not already grouped by custom groups, `move_sessions` switches its view. There is no read-only way to read back the previous view, so tell the user before the first move. Move the coordinator (`"self"`) and intended owners. Moving any session other than `"self"` may ask the user, and moving a pinned session unpins it. Remove the group only when the user asks, then restore the view they name with `set_view`.

Read back membership with `list_sessions` filtered by `group`, and the coordinator's own membership with `get_session("self")`. A successful mutation and a verified final state are separate evidence. Do not rename or delete unrelated groups. If grouping fails, keep the sessions and report the gap.

## Follow through and recover

Message owners only within an explicitly authorized coordination workflow. Address them with `SendMessage` by session id, as the host documents and the trial confirmed, or by `ListAgents` name. "Delivered" or "queued" confirms transport only; a session in a different permission mode may hold the message for approval. Owners report back to the coordinator's session id or to the `from` attribute of its message. Do not loop on `ListAgents` or send "are you done?" messages. In the desktop host checked here, the older `send_message` tool cannot reach unattended sessions (scheduled-task runs and remote-dispatched sessions), and `ListAgents` states that cloud sessions cannot reply yet. Elsewhere, judge by the target's inbox, inbound controls, and whether the message carries a reply address; when no reply can come, read the target's transcript instead of waiting.

For one idle notice, pass `notify_when_idle: true` addressed by the owner's `ListAgents` name, since a session-id address is rejected for subscriptions. Match the `ListAgents` row to the verified session id first and include its `[ref]` when one is shown, because a bare name that also names a helper reaches the helper. An idle notice means only that a turn ended. Read the owner's transcript with `list_events` to tell completion from a blocker or a request for input.

`stop_session` interrupts a turn and leaves the session open. Archiving is cleanup, not proof of release, and needs the user's authority. Removing a worktree can fail while a live session still uses it as its working directory; report the retained directory rather than forcing removal.

Long conversations are summarized automatically. Before a handoff, a long pause, or a large context, write the core recovery note in the coordinator's conversation. Add session and group ids, helper names, and worktrees and branches. Keep it out of persistent memory unless the user asks. On resumption, reconcile it with `list_sessions`, `get_session`, `ListAgents`, and `git worktree list` before dispatching replacements.

In replies, link a session as `[title](#<sessionId>)`; use its `link` field only in text that leaves the conversation.

## Preserve model settings

No preset applies. Keep the user's session settings and host defaults. Set the `Agent` tool's `model` only when the user asked or a package's reasoning need clearly justifies the cost. The [GPT-6 Astra preset](astra-effort-preset.md) targets GPT models. If the user selects it on a Claude host, report that it is unavailable and ask whether to keep the defaults or name a Claude model. Never map its effort levels onto Claude models silently; its `ultra` level has no Claude session equivalent.
