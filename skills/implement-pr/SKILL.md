---
name: implement-pr
description: Implement a change and deliver a green, review-ready pull request with explicit scope and evidence.
disable-model-invocation: true
---

# Implement PR

Own the change through a green, review-ready PR. Completion is the merge-ready PR, not the finished code.

## 1. Take ownership of linked work

For every linked ticket or work item, record ownership before implementation: Use the tracker's assignee field to assign the item to the currently authenticated user. If assignment is unavailable, use the tracker's explicit ownership or in-progress mechanism.

## 2. Establish the contract

Read the request, linked tickets or spec, repository instructions, and relevant code before editing. Write a short working contract and a task checklist to a git-ignored file (`.claude/tasks.md` when `git check-ignore -q .claude/tasks.md`, run as its own command, exits 0). Tick items off and add new ones as you find them; after compaction, re-read the file instead of the summary. The contract has five parts:

- **Outcome:** observable behavior that must exist.
- **Preserve:** behavior and interfaces that must stay unchanged.
- **Scope:** files, packages, and systems the request permits changing.
- **Evidence:** focused checks that prove the outcome and preserved behavior.
- **Stop:** the PR, required CI, and requested review state that define completion.

Resolve repository facts by inspection. Choose defaults for internal, reversible decisions that follow existing patterns and are cheap to change. Ask the user only when a choice changes product behavior, visible UX, data meaning, permissions, security, cost, compatibility, is destructive or expensive to reverse, requires authority or credentials, or needs information only the user has. Include a recommended default and the boundary reason with every question.

## 3. Implement the smallest complete change

Use the `$ponytail ultra` skill. Follow repository conventions and reuse established seams. Add only behavior required by the contract. Keep types precise from the lowest changed boundary to the highest consumer.

Read what the contract's open questions need, then edit. Once a read stops changing the plan, the reading is done: start implementing.

Add focused tests at the stable behavioral seam. Skip tests that only memorialize deleted behavior, duplicate type checks, or restate implementation details.

For visual or interactive work, use the browser, Android emulator or iOS simulator to check the affected states and responsive behavior. Capture evidence needed by the PR.

## 4. Verify

Before review, run the affected package's complete test, typecheck, lint, and build commands that the repository documents. Record commands and results for the PR.

## 5. Review cold

Review spend scales with the diff. Every reviewer gets the diff command, the contract file path, and only what its axis needs.

**Base.** Run `git fetch origin <base-branch>` and diff against `origin/<base-branch>`. A worktree's local base branch lags the remote and pulls unrelated commits into the diff. The review diff is `git diff origin/<base-branch>...HEAD`.

**Depth.** Size the diff with `git diff --shortstat origin/<base-branch>...HEAD`:

- **Light:** under about 50 changed lines that delete, rename, or adjust config, copy or docs without adding behavior. Run `$bug-review` alone.
- **Full:** everything else, and any diff touching auth, permissions, money, persisted data or migrations, concurrency, or a public interface, whatever its size. Run `$bug-review`, `$ponytail-review` and `$code-review`.

**Standards.** For a full review, select the standards files once. Read the repo's standards index, take the files it marks as always applying plus the domain files whose scope matches a touched path, and write the list into the contract file. With no index, select by each file's stated scope. This list is the complete standards set for every round; `$bug-review` and `$ponytail-review` get none.

**Dispatch.** Start `$bug-review` and `$ponytail-review` as background subagents. Then run `$code-review` yourself, with `origin/<base-branch>` as its fixed point, the contract file as its spec, and the selected list as its standards sources; its own Standards and Spec subagents are the cold readers. Each subagent's completion notification is your wake signal, so schedule no timers or wakeups for them.

Treat findings as hypotheses:

1. Verify each finding against the contract and current code.
2. Fix every valid, in-scope finding.
3. Record false positives and out-of-scope findings, leaving the change as it stands.
4. Re-run the checks your fixes touched.
5. Re-dispatch only the reviewers whose findings drove a fix. Hand each the fix hunks (`git diff <reviewed-sha>..HEAD`, or that SHA as `$code-review`'s fixed point) and its prior findings with your verdicts. Repeat until a round raises nothing new.

A finding that would widen the contract is an escalation under step 2's boundary, carrying a recommended default and the boundary reason.

Completion: every finding has a recorded verdict (fixed, false positive, or out of scope) in the contract file.

## 6. File and babysit the PR

Commit the complete change, push it, and use the `$file-pr` skill to open the PR.

Use the `$babysit-pr` skill until required CI and review automation are green. It addresses review feedback; re-run the evidence each fix affects.

Finish only when the PR is merge-ready or an external blocker remains. Report under these headings, in order, leaving out empty ones: **Blocked on you** (the exact blocker or decision), **Changed** (PR URL, verified checks, review state), **Found** (out-of-scope findings).
