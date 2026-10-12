# Unit 4 - Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

NOT OPENED. I am a teaching assistant working through this assignment as a walkthrough, so I did not open a pull request on the shared Path Review repo and there is no link to give.

The change is built and committed on the branch below, and its title and description are in a local `pr_draft.md`. I graded that draft in live mode with my installed pr-precheck skill, and the verdict was `accept`: all seven required checks and the preferred title check passed. The PR title is "fix(api): return False for a malformed hash in verify_password" and its description says "Closes #72".

**Branch**

fix/72-verify-password-malformed-hash

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Full run, saved with `--save-run eval-run.txt`: "agreement: 18/20 scored items  (bar: 18/20: PASS)" (misses: pkg-02 and pkg-08)

This was my only full run, so the last score, 18/20, is also the agreement line in the `eval-run.txt` I committed.

**Package analysis**

pkg-03 (starship/starship#7648).

- Gold label: reject. The gold note reads "the one-line fallback fix arrives with an unrequested truncate() rewrite and a new resolve_symlinks config option while the description claims 'implements the posted plan exactly' and the plan scopes out any config change".
- My rubric's decision: reject, so it agreed with gold.
- Why my rubric read it that way: this is the silent-drift case. By my rubric's wording, `plan-fidelity` fails a diff that "adds an unplanned change (a new option or flag, a rewrite, a rename pass, an unrelated file) with no deviation note". The truncate() rewrite and the new config option are exactly that, and the plan scopes out any config change. `description-honest` also fails a description that "claims fidelity the diff contradicts", and "implements the posted plan exactly" is that claim. The fix itself is right, so my rubric rejects it for the drift and for the description, not for the quality of the one-line change.

**Check rationale**

| plan-fidelity | The diff's changed files and hunks read against the plan's scope, files-to-touch, and Deviations section | Every changed file and hunk is named in the plan or recorded in its Deviations, and every deliverable the plan promises (code, test, docs) is in the diff or recorded as deferred. Fail if the diff adds an unplanned change (a new option or flag, a rewrite, a rename pass, an unrelated file) with no deviation note, or leaves out a planned deliverable without saying so. A change the plan itself defers, with the description saying so, passes. | required |

I wrote it to read the diff against the plan in both directions, because the silent-drift packages go both ways. pkg-03, pkg-06, and pkg-09 do more than the plan, and the gold note for pkg-17 says "the plan promises a dev warning AND a docs update; the diff contains only the warning while the description claims the docs 'now document the limitation'", which does less than the plan. The last sentence, "A change the plan itself defers, with the description saying so, passes", is there because pkg-13 and pkg-16 are accepts that honestly disclose a shortfall, and a check that treated "less than everything" as a failure would reject them. I rejected a simpler version that only looked for extra files in the diff, because it would miss pkg-17.

**Trade-offs**

This check only compares the diff to the plan, so it gives up judging the plan itself: a PR that does exactly what an oversized plan said would pass it. I accept that, because the plan was already graded in the previous unit.

I did not revise this check after my first full run, so I did not re-run any canaries with `--only`. The reason nothing changed around it: it did not cause either of my two misses. The run's notes show pkg-02 failed on "template-asks" and pkg-08 on "repo-checks, template-asks", both clear accepts that my rubric rejected for the template and repo-check wording, not for plan fidelity. All four silent-drift packages (pkg-03, pkg-06, pkg-09, pkg-17) matched gold in the run ("silent-drift 4/4"), including pkg-09, which the gold note calls arguable.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.