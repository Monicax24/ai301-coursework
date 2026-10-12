# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

Feeds the checks plan-fidelity and description-honest.

- Where it lives, eval bundle: the plan-context block (the plan's in-scope and not-in-scope lines, its files-to-touch, its promised deliverables, any Deviations note); the candidate PR's diff and commit list; the candidate PR's description, read claim by claim. Live mode: plan.md and its Deviations section; the branch's diff from `git diff main...HEAD`; the draft description in pr_draft.md.
- What good looks like: every changed file and hunk falls inside the plan's stated boundary or a Deviations note, and every deliverable the plan promises (code, a test, a docs update) is in the diff or recorded as deferred. Silent drift goes in both directions: the diff does more than the plan (a new option or flag, a rewrite, a renaming pass, an unrelated file) with no note, or less than the plan (a promised docs update missing) with no note. A deferral the plan states, and the description repeats, is an honest shortfall and passes. The description is read against the diff: a claim of "exactly as planned" or "no changes outside X" that the diff contradicts, or a claim that docs were updated when the diff has none, is drift too.

## Test evidence (harness category: not-tested)

Feeds the checks decisive-evidence and repo-checks.

- Where it lives, eval bundle: the candidate PR's test-evidence section, read against the plan-context block's test plan and repro steps; the repo-facts block for the repo's stated check commands. Live mode: test_evidence.md read against the test plan in plan.md and the repo's PR template.
- What good looks like: the plan's repro is re-run on the path the fix changes, with an observable before and after (an exit code, an output line, a diff, a table) and the commands shown. Every failure mode the plan's test plan names is exercised, or the description says it was not. The repo's own checks (the commands the template or contributing guide names) are shown with their results; a failing check reported honestly with the reason counts as evidence. Not decisive: "tests pass" with nothing named, "works on my machine", output from the unchanged path or a control run (for example a GET when the bug is a POST), or a repro the plan names that is never re-run.

## Diff quality (harness category: unreviewable)

Feeds the check diff-clean.

- Where it lives, eval bundle: the candidate PR's unified diff and its commit list. Live mode: the output of `git diff main...HEAD` and `git diff main...HEAD --stat`, plus `git log main..HEAD --oneline`.
- What good looks like: the fix is visible and nothing unrelated rides along. Debris tells: debug prints or logging left from debugging, commented-out code, dead code (an added function or variable that nothing uses, or code hidden behind an allow-dead-code attribute), formatting-only or import-reordering hunks, leftover TODO or WIP notes, and edits to unrelated files. Judge the diff lines themselves; commit messages like "wip" or "misc cleanups" are a hint to look closer, not the evidence.

## Standards and comms (harness category: standards-wall)

Feeds the checks template-asks, ai-disclosure, and title-clear.

- Where it lives, eval bundle: the repo-facts block (the PR template's required sections, any required artifact such as a changelog or whatsnew entry, and the stated AI-use policy); the candidate PR's description and title; the diff, for whether a required artifact is present. Live mode: .github/PULL_REQUEST_TEMPLATE.md and docs/CONTRIBUTING.md in the repo; the draft title (first line) and description in pr_draft.md.
- What good looks like: every section the template requires has real content (Summary, Issue with Closes #, Changes, Testing with the boxes that are true ticked, Notes for Reviewers), no section is left as placeholder text, and every artifact the repo says it requires with a change is in the diff. If the stated policy requires disclosing AI use, the description says how AI was used in the author's own words; if it requires human-written text, a first-person description with its own specifics passes; a permissive or silent policy passes. Treat every package as AI-assisted work for the disclosure rule only. The title names the change and the area. (Whether the description's claims match the diff belongs to plan fidelity, above.)