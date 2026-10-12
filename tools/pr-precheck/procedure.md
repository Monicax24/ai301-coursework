# Procedure: how this tool grades a PR package

## Read order

1. Read the issue context first. Note the exact symptom the issue reports in one line.
2. Read the plan context (eval) or plan.md (live) next. Write down: the files and code sites the plan names, its in-scope and not-in-scope lines, every deliverable it promises (code, tests, docs), its test plan (the exact repro and the observable result it expects), and anything in its Deviations section. Read the plan before the diff so the diff is judged against the plan and not the other way round.
3. Read the repo-facts block (eval) or the PR template and docs/CONTRIBUTING.md (live). Note the required template sections, any required artifact (changelog entry), the stated check commands, and the AI-use policy.
4. Read the diff. List every changed file and, for each file, what its hunks do. Mark any hunk that is a debug line, commented-out code, a dead function, formatting or import churn, or unrelated to the issue.
5. Read the commit list (eval) or the branch's commits (live), and note whether they match the diff.
6. Read the test evidence. Note each command run, its output, and which path it exercises.
7. Read the PR title and description last, against the diff and evidence. List every claim the description makes.
8. Do not grade anything until all eight reads are done.

## Evidence gathering

1. plan-fidelity: put the diff's file list beside the plan's named files. Record each file in the diff that the plan or its Deviations does not name, each hunk that does something the plan did not ask for, and each deliverable the plan promises that the diff lacks.
2. description-honest: for each claim in the description, find the diff lines or evidence that make it true or false. Record each claim that the diff or evidence contradicts, and each claim of fidelity or completeness.
3. decisive-evidence: place the plan's test plan beside the test evidence. Record whether the plan's repro was re-run, on which path (the changed path or an unchanged one), whether a before and an after both appear, whether the output is observable, and which failure modes the plan names that the evidence never exercises.
4. repo-checks: from the repo-facts block or template, list the check commands. Record, for each, whether the evidence shows the command and a result, or states why it could not run.
5. diff-clean: from the diff-reading notes, quote each debris line or churn hunk. Record "none" if there is nothing.
6. template-asks: for each section the template requires, record whether the description fills it with real content. Record whether the Closes # line is present and whether any required artifact (such as a changelog entry) is in the diff.
7. ai-disclosure: quote the policy line from the repo-facts block, or record that it is silent. Then quote the part of the description that discloses AI use, or record that there is none, and record whether the description reads as the author's own first-person words.
8. title-clear: quote the title.
9. Use only the package text in eval mode. In live mode, take issue-side facts from the thread, the PR template, and docs/CONTRIBUTING.md, and take the candidate side from plan.md, the diff on the branch, pr_draft.md, and test_evidence.md.

## Check execution

1. Run the checks in this order: plan-fidelity, description-honest, decisive-evidence, repo-checks, diff-clean, template-asks, ai-disclosure, title-clear.
2. Grade each check pass, fail, or unclear by applying its pass condition in rubric.md to the evidence recorded for it. Name the quote or fact that decided it.
3. If the evidence a check needs is genuinely absent from the package, grade it unclear and say what is missing. Do not guess, and do not carry a grade over from another check.
4. Grade from the notes already made. Re-read only the specific lines a check names.
5. A shortfall that the plan or the description states plainly is not a failure of plan-fidelity or description-honest. A shortfall that exists only in the diff, with no note, is.
6. A claim in the description that the diff contradicts fails description-honest, however good the diff is.
7. Grade the checks independently. A clean diff does not raise a failed evidence check, and one failed check does not lower the others.
8. If this procedure is silent on a case, say so in the summary and do not invent a step.

## Verdict assembly

1. Apply the verdict rule in rubric.md: accept if every required check passes; reject if any required check fails; preferred checks never change the verdict.
2. Treat unclear on a required check as fail.
3. If the verdict is reject, the deciding check is the first failing required check in rubric order. Quote its evidence line in the summary.
4. If the verdict is accept, say that every required check passed and quote one evidence line.
5. Emit the JSON block with one entry per check in rubric order and the verdict last. It must be valid and must be the final thing in the output.