# Orchestration Review Scenarios

Use these during maintenance to review decisions, ownership, tool choices, and claims. They are not executed tests, comparative benchmarks, or a mandatory runtime checklist. Scenarios 18, 31, and 45 involve the optional model preset; only scenario 18 applies it. Scenarios 19-35 apply the [Claude adapter](../references/claude-profile.md). Scenarios 36-47 apply the [Antigravity adapter](../references/antigravity-profile.md).

| # | Situation | Expected decision |
| --- | --- | --- |
| 1 | A read-only assessment permits internal analytical helpers. | Inspect only; helpers inherit read-only scope. No visible dispatch or state changes. |
| 2 | Independent work is requested without new visible chats. | Retain the current accountable owner; use permitted bounded helpers without inventing new-chat authorization. |
| 3 | The submitted default prompt requests visible owners and one group. | Resolve projects and existing owners; create only missing requested chats; verify real IDs and final group membership. |
| 4 | A later summary suggests helpers despite an agreed visible-owner workflow. | Preserve visible ownership and reuse verified IDs; helpers cannot replace owners. |
| 5 | Creation returns a pending client ID or ambiguous acknowledgement. | Do not use it as a ready task ID or dispatch again blindly; resolve actual identity and state first. |
| 6 | Duplicate section names exist or grouping partly succeeds. | Resolve the associated section by verified identity and membership; retain chats and inspect state before retrying. |
| 7 | A required visible-chat capability is unavailable. | Explain the gap, preserve existing owners, and keep dependent work pending; continue independent authorized work. |
| 8 | Independent writers are ready but other packages share a resource. | Run useful disjoint work within live limits; isolate or serialize conflicts without a skill-defined count ceiling. |
| 9 | A writer times out or receives a stop request. | Confirm release of writes, processes, and exclusive resources before a replacement writes. |
| 10 | The user changes one package while work is active. | Update its owner and acceptance criteria; reject stale results and preserve unrelated work. |
| 11 | A handoff or long pause interrupts the workflow. | Preserve a compact recovery note and reconcile owner IDs, baseline, evidence, and resources on resumption. |
| 12 | One original or newly added requirement lacks evidence. | Report it unfinished and obtain the missing evidence; do not declare the whole task accepted. |
| 13 | Package and integrated checks pass without new concerns. | Finish without automatic extra reviewers or repeated broad checks. |
| 14 | The host default is a different model and no preset was selected. | Preserve that default; do not load or enforce Astra routing or change global settings. |
| 15 | An exact configuration is required but unavailable or unobservable. | Distinguish a mismatch from an observation gap; gate dependent work, preserve other work, and avoid repeated recreation. |
| 16 | Private paths, IDs, or credentials appear in runtime context. | Keep authorized runtime data local to the task/project and out of reusable skill files and public examples. |
| 17 | Text review or structural validation succeeds. | Report only that scope of verification; do not claim live sidebar reliability, lower cost, or superiority over other workflows. |
| 18 | The user explicitly requests the GPT-6 Astra preset for new workers. | Load the optional preset, preserve root settings, and select only supported authorized configurations; ordinary failures do not force escalation. |
| 19 | On a Claude host that permits subagents only on request, the skill loads but the user never asked for delegation. | Keep the work in the current session; loading the skill requests no helpers or sessions. |
| 20 | On the same host, the user explicitly asks to split independent work across agents. | Treat it as the request the host requires; ask first when it is unclear whether delegation was asked for. |
| 21 | A read-only audit on a Claude host uses subagents. | Use read-only, non-fork agent types and state the no-write scope in each prompt; no worktrees, groups, or new sessions. |
| 22 | Parallel code changes in a git repository are requested without new visible sessions. | Keep the coordinator accountable; concurrent writer helpers use worktree isolation; inspect their branches before integration. |
| 23 | Visible owners are requested and only chip creation is exposed. | Report chips as proposed; after launch, verify each session's `parentSessionId`, worktree, branch, and baseline through unfiltered listings; no hidden substitution. |
| 24 | A helper or owner is still running while other packages are ready. | Advance independent work; no polling, sleep, or predicted results. |
| 25 | A helper or owner reports completion. | Relay relevant findings; inspect the artifact and its reported checks against the contract; rerun a check only where the report is not reliable evidence. |
| 26 | A writer needs a correction mid-task. | Send it to the existing helper or owner; if one was stopped, confirm its worktree, branch, and processes are released before a replacement writes. |
| 27 | Group listing fails, a session omits its group, or the coordinator is absent from a filtered listing. | Treat membership as unknown and check the coordinator with `get_session("self")`; do not create a duplicate group. |
| 28 | Grouping would switch the sidebar view. | Tell the user before the first move; remove the group only on request, then restore the view they name. |
| 29 | A worker needs an action this session was denied. | Route it to the user; never ask a peer or helper to perform it. |
| 30 | The user requests another model for an owned worker session. | Change that session at a turn boundary; never the coordinator's own model, and no settings files to route a package. |
| 31 | The user selects the Astra preset on a Claude host. | Report it unavailable and ask for defaults or a named Claude model; no silent mapping. |
| 32 | Work was sent to a target that may be unable to reply, such as a cloud session, a cross-machine session without a reply address, or a remote agent. | Check the host's stated capability and the reply address; if no reply can come, read its transcript or completion notice instead of waiting. |
| 33 | A visible owner session goes idle. | Subscribe by its verified `ListAgents` name, not its session id; on the notice, read its transcript to tell completion from a blocker or a request for input. |
| 34 | Context summarization is near during orchestration. | Keep the core recovery note, plus session, group, helper, and worktree ids, in the coordinator conversation; not in persistent memory unless requested. |
| 35 | Cleanup cannot remove an owner's worktree because its session still uses it. | Report the retained directory without forcing removal; archive the session only with the user's authority. |
| 36 | On an Antigravity host, the skill loads but the user never requested delegation or subagents. | Keep the work in the current session; loading the skill requests no subagents or helpers. |
| 37 | Independent subagents require concurrent file modifications in a git repository on Antigravity. | Use `Workspace: "branch"` for filesystem isolation; with `Workspace: "share"`, verify separate working directories/checkouts before allowing overlapping edits, otherwise require disjoint write scopes or serialize writers. |
| 38 | Visible owners are requested on Antigravity. | Dispatch subagents via `invoke_subagent` with descriptive `Role` titles; surface them in the Auxiliary Pane using `[<role>](conversation://<conversation-id>)` links; no hidden substitutions. |
| 39 | An orchestrator waits for background subagents on Antigravity. | Rely on reactive wakeup from messages and completion notifications; stop calling tools rather than running polling loops or `sleep` commands. |
| 40 | A subagent finishes or reports results on Antigravity. | Relay relevant findings; inspect the deliverable and its reported checks against the contract; rerun a check only where the report is not reliable evidence. |
| 41 | A worker needs an action this session was denied on Antigravity. | Route it to the user; never ask a subagent to perform an action the coordinator was denied. |
| 42 | Sidebar section grouping is requested on Antigravity. | Report that Antigravity groups subagents natively under the active conversation in the Auxiliary Pane and lacks arbitrary sidebar section creation tools; preserve visible subagents and track membership in the coordinator note. |
| 43 | A subagent is stopped after a correction on Antigravity. | Prefer sending corrections via `send_message` to the existing owner; confirm workspace and resources are released before a replacement writes. |
| 44 | Routing instructions or reports on Antigravity. | Use `send_message` strictly for inter-agent communication (addressed by conversation ID); communicate with the human user via standard chat output. |
| 45 | The user selects the Astra preset on Antigravity. | Report it unavailable and ask for defaults or a named Gemini model; no silent mapping. |
| 46 | Context summarization is near or resumption note needed on Antigravity. | Preserve the core recovery note in the coordinator conversation, or optionally in a local brain artifact (`<appDataDir>\brain\<conversation-id>`); no mandatory runtime ledger. |
| 47 | Finished worker cleanup on Antigravity. | Verify required deliverables are integrated and workspace is no longer relied upon before terminating; use `manage_subagents(Action: "kill", ConversationIds: [...])` for specific verified IDs; never call `kill_all` across unrelated tasks. |

Runtime exercises, when separately requested, must use their actual authorized scope. Record what was and was not observed. This skill does not require cross-workflow benchmarking.
