# Decision Guide

Use these examples only when a decision is unclear. The core and active tool contracts govern; examples introduce no task-count or model defaults.

| Situation | Decision |
| --- | --- |
| A small task has one coherent outcome | Keep its current owner; no artificial decomposition |
| Independent work is useful but no new visible tasks were requested | Keep the current task accountable; use permitted bounded helpers |
| The user requested visible owners earlier in this workflow | Preserve that contract across continuation; verify real IDs and reuse owners |
| Two packages share an unresolved schema decision | Settle the common contract or sequence the dependent work before parallel writes |
| Disjoint files use the same database, cache, port, or device | Isolate or serialize that resource; file separation alone is insufficient |
| A worker times out, disappears, or receives a stop request | Reconcile live state; do not release its write reservation merely because observation ended |
| A user correction invalidates an in-progress result | Update the affected owner and acceptance contract; reject stale output while preserving unrelated work |
| More tasks are ready than an earlier example allowed | Use current capacity and conflicts, not historical fan-out numbers |
| A difficult decision lacks facts | Retrieve evidence; extra effort cannot supply missing facts or authority |
| Reliable package checks and integrated acceptance have passed | Finish; add checks only for a new change, failure, unresolved risk, or project requirement |

## A compact continuation note

Before a handoff or significant context break, leave enough state to resume without recreating the team:

> Continue the current objective within the agreed scope. Retain the verified owner and group IDs. Check the recorded baseline and validated outputs against live state, resolve the listed blockers and retained resources, then perform the next pending action. Apply all later user corrections before acceptance.

Populate the note with actual facts in the existing task or authorized project context. Do not put private runtime values into this skill, invent missing IDs, or treat the note as proof that a writer stopped.

## Proportional verification

Choose checks that can detect the relevant failure. Worker confidence, a completed status, or a plausible artifact does not establish acceptance. Use targeted package validation and an integrated check; independent review is useful when a concrete uncertainty remains, not merely because another review slot exists.
