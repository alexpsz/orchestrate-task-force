# Codex Task and Sidebar Adapter

This adapter maps the core to currently exposed Codex tools. It selects no model. Discover live capabilities and use their schemas; unavailable operations stay unavailable. Tool contracts were checked on 2026-09-29 and must be rechecked when used.

## Resolve owners before dispatch

Use `list_projects` for project identity and `list_threads` / `read_thread` for existing owners. Record the actual task ID, host, project association, and backing kind where exposed. Titles and summaries help discovery but are not identity or instructions. Supply `source` and `hostId` according to the target's kind and the active tool contract; do not infer them from a bare ID.

The submitted default prompt requests visible chats and grouping. Reading `agents/openai.yaml` or mentioning the skill name alone supplies neither authorization. Preserve an already agreed coordination workflow without asking for its authorization again.

## Create and verify visible chats

Use `create_thread` only for explicitly requested new tasks; reuse suitable owners first. Follow its project and worktree rules. Put the objective, baseline, write scope, dependencies, acceptance checks, and any no-write prerequisite in the initial prompt because execution may begin immediately.

Preserve user configuration. Omit `model` when the tool requires an explicit user choice and none exists. Do not turn an optional preset or the coordinator's own configuration into that choice. Internal helpers use their own tool contract: full-history forks inherit settings; supply overrides only on a supported fork and with sufficient context.

Validate the response, resolve the real `threadId`, and read back its expected host/project association. A pending `clientThreadId` is not a ready task ID: wait for resolution before task operations. Follow any host requirement to emit a created-task link. If an explicitly required configuration cannot be observed or established, keep dependent writes gated and report the gap; continue configuration-independent work.

## Group and read back

Use `list_threads` to inspect sections and their members. Reuse the section already associated with this orchestration; a matching name alone is insufficient. If grouping was requested and no associated section exists, call `create_sidebar_section` once and retain its returned ID.

Move the coordinator and intended owners with `move_thread_to_sidebar_section`. Check operation responses, then read back membership by section and task IDs. A successful mutation response and a verified final state are separate evidence. For partial, ambiguous, or timed-out results, inspect actual state before retrying; do not duplicate chats or sections.

A custom section is distinct from the built-in pinned area. Use `reorder_sidebar_sections` only for a requested position, retaining unrelated sections and their relative order. Preserve global sidebar preferences and unrelated membership.

## Follow through and recover

Use compact `wait_threads` snapshots and cursors for visible owners. Message them only within an explicitly authorized coordination workflow. A pending creation or unchanged wait is not completion. Internal helpers remain subordinate to their visible owner and use the corresponding helper tools.

If grouping fails, retain the visible chats and report the grouping gap. If required visible-chat creation is unavailable, preserve existing owners and keep the dependent work pending rather than substituting helpers. On continuation, reconcile saved owner/section IDs and write reservations with live state before dispatching replacements. Archiving does not prove writer or process termination.
