# Orchestration Review Scenarios

Use these during maintenance to review decisions, ownership, tool choices, and claims. They are not executed tests, comparative benchmarks, or a mandatory runtime checklist. Only scenario 18 selects the optional model preset. Scenarios 19-33 apply the [Claude adapter](../references/claude-profile.md).

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
| 20 | Parallel code changes in a git repository are requested without new visible sessions. | Keep the coordinator accountable; concurrent writer helpers use worktree isolation; inspect and check their branches before integration. |
| 21 | Visible owners are requested and only chip creation is exposed. | Report chips as proposed; after launch, resolve sessions through unfiltered listings and `parentSessionId`; no hidden substitution. |
| 22 | A helper or owner is still running while other packages are ready. | Advance independent work; no polling, sleep, or predicted results. |
| 23 | A helper or owner reports completion. | Relay relevant findings; inspect the artifact and rerun package checks before acceptance. |
| 24 | A writer is stopped after a correction. | Prefer correcting the existing owner; otherwise confirm its worktree, branch, and processes are released before a replacement writes. |
| 25 | Group listing fails or a session omits its group. | Treat membership as unknown; do not create a duplicate group. |
| 26 | Moving sessions into a group switched the sidebar view. | Tell the user; after the group is removed, restore the view they name. |
| 27 | A worker needs an action this session was denied. | Route it to the user; never ask a peer or helper to perform it. |
| 28 | The user requests another model for an owned worker session. | Change that session at a turn boundary; never the coordinator's own model or settings files. |
| 29 | The user selects the Astra preset on a Claude host. | Report it unavailable and ask for defaults or a named Claude model; no silent mapping. |
| 30 | Work was sent to a cloud session or remote agent. | Read its transcript or completion notice; do not wait for a reply it cannot send. |
| 31 | One completion notice is needed from a visible owner. | Subscribe by its `ListAgents` name; if an id address is rejected, retry once by name instead of polling. |
| 32 | Context summarization is near during orchestration. | Keep the recovery note in the coordinator conversation, not in persistent memory unless requested. |
| 33 | Cleanup cannot remove an owner's worktree because its session still uses it. | Report the retained directory; archive the session only with the user's authority. |

Runtime exercises, when separately requested, must use their actual authorized scope. Record what was and was not observed. This skill does not require cross-workflow benchmarking.
