# Procedure: how this skill grades a plan package

## Read order

1. Read the issue context first: the title, the body, and the behavior the reporter describes. Note the exact symptom in one line.
2. Read the repro-evidence block next. Note every numbered step, every output, and every control run (the same steps with one thing changed). Write down what each control run rules in or out. This comes before the plan so the plan is judged against the evidence and not the other way round.
3. Read the thread highlights. Note any explicit maintainer direction (a located culprit, a requested test, a posted patch, a settled design) and any linked or prior PR that attempts the same fix.
4. Read the repo-facts block. Note the stated contribution policy and any AI-use policy, and whether it requires disclosure or human-written comments.
5. Read the candidate plan: its cause, in-scope and not-in-scope statements, files, approach, test plan, and risks.
6. Read the candidate plan comment last, against the thread notes and the policy notes from steps 3 and 4.
7. Do not grade anything until all six reads are done.

## Evidence gathering

1. cause-grounded: quote the plan's stated cause. Then quote the repro-evidence line or control run that bears on it. Record whether the evidence supports the cause, rules it out, or never points at it.
2. scope-bounded: list every change the plan proposes, one per line. For each, mark whether the issue as reported requires it. Record any not-in-scope line and any deferral with its reason.
3. buildable: record the files or code sites the plan names and the one approach it commits to. Record any decision the plan defers to build time, quoting the words used ("somewhere", "whichever is easier", "maybe also", "investigate").
4. test-observable: quote the plan's test plan. Record the action it re-runs and the observable result it names (exit code, output line, parse success). Record whether that action matches a step in the repro evidence.
5. thread-engaged: from step 3 of the read order, list the maintainer directions and prior PRs. Then quote the line in the plan comment that follows or answers each one, or record that none does. If the thread has no direction, record "no direction".
6. repo-conventions: quote the policy line from the repo-facts block. Then record whether the plan comment contains an AI-use disclosure, and whether it reads as first-person with its own specifics or as generic text.
7. unknowns-honest: quote the plan's risks and unknowns section, and mark each item as stated uncertainty or asserted fact.
8. Use only the package text in eval mode. In live mode, gather issue-side evidence from the locations named in references/evidence-guide.md, and read the drafts as the candidate side.

## Check execution

1. Run the checks in this order: cause-grounded, scope-bounded, buildable, test-observable, thread-engaged, repo-conventions, unknowns-honest.
2. Grade each check pass, fail, or unclear by applying the pass condition in rubric.md to the evidence recorded in the gathering stage. Name the fact or quote that decided it.
3. If the evidence a check needs is genuinely absent from the package, grade it unclear and say what is missing. Do not guess, and do not carry a grade over from another check.
4. A check may be graded from the notes already recorded; do not re-read the whole package for each check. Re-read only the specific lines the check names.
5. If a control run or isolated output in the repro evidence rules out the plan's named cause, cause-grounded fails, however well the rest of the plan is written.
6. If the plan includes work the issue never asked for, scope-bounded fails, even when the core fix inside it is correct.
7. If the thread contains explicit maintainer direction that the plan comment does not engage, thread-engaged fails.
8. If the policy requires AI-use disclosure and the plan comment has none, repo-conventions fails. Treat every package as AI-assisted work for this rule only.
9. Grade the checks independently. Do not let a strong plan raise a weak check, and do not let one failed check lower the others.
10. If this procedure is silent on a case, say so in the summary instead of inventing a step.

## Verdict assembly

1. Apply the verdict rule in rubric.md: accept if every required check passes; reject if any required check fails; preferred checks never change the verdict.
2. Treat unclear on a required check as fail, as the rubric states.
3. If the verdict is reject, name the first failed required check in execution order as the deciding check, and quote its evidence line in the summary.
4. If the verdict is accept, state that every required check passed, and quote the evidence line for one of them.
5. Emit the JSON block with one entry per check, in rubric order, and the verdict last. The block must be valid and must be the final thing in the output.
