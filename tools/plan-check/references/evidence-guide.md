# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

Feeds the check cause-grounded.

- Where it lives, eval bundle: the candidate plan's stated cause (usually its diagnosis section or first paragraph); the repro-evidence block, including its numbered steps, outputs, and any control run (the same steps with one thing changed, such as the flag removed or the input swapped). Live mode: the diagnosis in plan.md, read against the student's posted repro comment (or the house repro pack as quoted in the drafts).
- What good looks like: the cause the plan names explains what the repro evidence shows. A control run or isolated output is the strongest evidence: if it shows the named cause already behaves correctly, that cause is ruled out. A plan that blames a component the evidence shows working fails, and so does a plan that names a cause the evidence never points at. A cause labeled as a hypothesis, with a way to check it, passes.

## Scope

Feeds the check scope-bounded.

- Where it lives, eval bundle: the plan's in-scope statement, its not-in-scope line, its approach, and the files or areas it lists, read against the issue body. Live mode: the same sections of plan.md, read against the issue on GitHub.
- What good looks like: one bounded change that fixes the issue as reported. Every item in the approach is needed for that fix. Compare drive-by work to the issue: refactors, migrations to a new library, new options or settings, UI rework, retry frameworks, or restructured modules the issue never asked for are scope creep, even when the core fix inside is correct. A short, named not-in-scope line, or an honest deferral of part of the work with a reason, is bounded.

## Executability

Feeds the check buildable.

- Where it lives, eval bundle: the plan's files-to-touch list and its approach. Live mode: the same sections of plan.md.
- What good looks like: a stranger could start editing from the plan alone. It names the file, function, or code site to change and commits to one approach. It fails if the key decisions are pushed to build time ("somewhere", "whichever is easier", "maybe also", "investigate X") or if no files or sites are named. A terse plan that names the site and the change is executable.

## Test plan

Feeds the check test-observable.

- Where it lives, eval bundle: the plan's test plan, read against the repro-evidence block's steps and outputs. Live mode: the test plan in plan.md, read against the repro comment's steps.
- What good looks like: the test plan re-runs a specific action (normally the repro steps) and names the observable result that proves the fix: an exit code, an output line, or a parse that now succeeds. It maps onto the artifacts in the repro evidence, so "before" and "after" can be compared. A test plan with no outcome tied to this fix ("should feel fast", "nothing else should break", "run the full test suite") fails.

## Honesty

Feeds the check unknowns-honest.

- Where it lives, eval bundle: the plan's risks and unknowns section, and any statement of uncertainty in the plan comment. Live mode: the same sections, plus the Deviations section of plan.md after the build.
- What good looks like: uncertainty is stated as uncertainty. Open questions are named as things to check, not asserted as facts. A deviation from the posted plan is recorded in plan.md under Deviations with what changed and why; a deviation that exists only in the diff is not honest work.

## Comms

Feeds the checks thread-engaged and repo-conventions.

- Where it lives, eval bundle: the plan comment, read against the thread highlights (maintainer direction, located culprits, posted patches, requested tests, linked or prior PRs) and against the repo-facts block's stated contribution policy and AI-use policy. Live mode: the draft comment against the issue thread on GitHub; the repo's CONTRIBUTING.md and any AI-use section.
- What good looks like: if a maintainer gave explicit direction in the thread, or a prior PR attempts the same fix, the comment follows it or says why it departs. A comment that ignores the thread's direction fails, however good the plan is. For conventions: if the policy requires disclosing AI assistance, the comment must disclose it (treat every package as AI-assisted work for this rule only); if it requires human-written comments, a first-person comment with its own specifics passes and generic text fails; a permissive or silent policy passes.