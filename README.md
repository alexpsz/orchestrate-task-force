# Orchestrate Task Force

English | [简体中文](README.zh-CN.md)

Coordinate independent work in Codex Desktop or Claude Code with visible owner chats or sessions, one shared sidebar group where the host has a sidebar, and concurrency that adapts to the work. The core also supports bounded internal assistance when separate chats are not requested.

This is an instruction-only skill: no extra service, control console, or mandatory run ledger. It uses the capabilities exposed by the current host and preserves the user's model settings by default.

## Use it

For visible owners and a group, submit:

> Use $orchestrate-task-force to coordinate this request. Create or reuse separate sidebar-visible owner chats for independent work packages and group them with this coordinator in one named sidebar section. Adapt concurrency to current capacity and conflicts, then verify the integrated result within the authorized scope.

The default prompt supplies this wording where supported. Check the submitted text: mentioning the skill name alone does not request new chats. For a read-only audit, say so; for internal assistance only, explicitly keep the work in the current chat.

In Claude Code, submit the same request after `/orchestrate-task-force`; there, owner chats are sessions and the sidebar section is a group. Claude may also load the skill from its description, which never authorizes new sessions or helpers. In the desktop app, new visible sessions may appear as suggestion chips that start only when you click them.

Continue the same orchestration with a request such as:

> Continue with the existing owners and sidebar group. Apply the revised requirement, keep unaffected work, and verify the integrated result.

The coordinator checks real task identities and group membership. Pending creation is not readiness. Grouping failure preserves existing chats; unavailable visible-task capability is reported rather than replaced with hidden helpers.

## What it preserves

- One owner per conflicting write scope; independent writers may run concurrently.
- Dynamic scheduling from dependencies, capacity, and resource pressure, without fixed task or writer counts.
- Corrections handled by the existing owner where possible, with stale results rejected.
- A short recovery note before handoff or significant context loss, reconciled with live state on return.
- Targeted worker checks and integrated acceptance covering every current requirement.
- Explicit reporting of unresolved work and retained resources.

## Models and host support

No model or effort preset is enabled by default. Keep user choices and host defaults; adapt permitted settings only for a concrete reasoning need. The [GPT-6 Astra effort preset](references/astra-effort-preset.md) is optional. To select it, explicitly request: "Use the GPT-6 Astra effort preset for new workers." Root settings remain unchanged.

The [Codex adapter](references/codex-profile.md) covers visible chats and grouping using available native tools. The [Claude adapter](references/claude-profile.md) covers Claude Code: subagents as bounded helpers with worktree isolation, desktop sessions as visible owners, and custom sidebar groups. The Astra preset does not apply on Claude hosts. Other hosts can use the core principles, but visible-chat and sidebar support must be established on that host. A model name or effort label does not grant tools, permissions, or extra capacity.

## Install and read

Copy the complete folder to a skill location supported by your host. Current Codex documentation lists `~/.agents/skills/orchestrate-task-force` for user skills and `.agents/skills/orchestrate-task-force` for repository skills. Keep an existing recognized installation in place rather than creating a duplicate. See the [official installation guidance](https://learn.chatgpt.com/docs/build-skills#where-codex-loads-local-skills). Current Claude Code documentation lists `~/.claude/skills/orchestrate-task-force` for personal skills and `.claude/skills/orchestrate-task-force` for project skills; see the [Claude Code skills documentation](https://code.claude.com/docs/en/skills).

- [SKILL.md](SKILL.md): English normative core.
- [Codex adapter](references/codex-profile.md): read only for Codex visible-task operations.
- [Claude adapter](references/claude-profile.md): read on Claude Code hosts before dispatching helpers or sessions, grouping, messaging, or changing configuration.
- [Optional Astra preset](references/astra-effort-preset.md): read only after explicit selection.
- [Decision guide](references/decision-guide.md): read when a decision is unclear.
- [Review scenarios](evals/behavior-cases.md): maintenance examples, not runtime performance results.

The Chinese README translates this guide. References and translations do not override the core or higher-priority instructions. Keep private project data, credentials, and runtime IDs out of reusable files and public examples.

## License

MIT
