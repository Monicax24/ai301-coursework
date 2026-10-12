# Unit 2 — Claim and Reproduce
 
Path: `beat-1-sandbox/unit-2/reproduction.md`
 
Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.
 
Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.
 
---
 
## Your identity upstream
 
**GitHub username**
 
Monicax24
 
---
 
## Posted upstream
 
**Claim comment**
 
(Not posted, TF walkthrough)
 
Below is the draft I wrote for issue #72 (https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72). I graded it in live mode with my installed repro-check skill, and the verdict was `accept` (claim-specific: pass, repo-conventions: pass; the repro checks reported "not yet applicable: claim-only draft").
 
Draft, not posted:
 
> Hi, I'd like to claim this one. I'll try to reproduce the bug in `verify_password` in `core/security.py` by passing it a malformed hash and checking whether it raises instead of returning `False`, starting from the existing `xfail` test in `tests/unit/test_security.py`. I'll post a repro report here with my environment and the output I get.
 
**Reproduction comment**
 
(Not posted, TF walkthrough)
 
---
 
## Eval iterations
 
Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.
 
**Run history**
 
1. Full run: "agreement: 17/20 scored items  (bar: 18/20: below the bar)" (misses: pkg-03, pkg-05, pkg-12)
2. Partial `--only` run (pkg-03, pkg-05, pkg-12, pkg-20, pkg-07, pkg-06, pkg-18), not a scored run: "agreement: 7/7 scored items"
3. Final full run, saved with `--save-run eval-run.txt`: "agreement: 19/20 scored items  (bar: 18/20: PASS)" (miss: pkg-03)
The last score, 19/20, matches the agreement line in the `eval-run.txt` I committed.
 
**Package analysis**
 
pkg-05 (conda/conda#16543, "EnvironmentSectionNotValid message breaking json output").
 
- Gold label: accept. The gold note reads "minimal env.yml repro with a json.tool parse failure as the artifact; conda's stated generative-AI policy is permissive-with-responsibility, no disclosure requirement".
- My rubric's decision in run 1: reject ("failed: steps-rerunnable, next-step-concrete"). `next-step-concrete` is preferred, so it could not cause the reject; `steps-rerunnable` did.
- Why my rubric read it that way: the first version of `steps-rerunnable` said "exact commands or inputs are shown". The repro report says it "wrote a minimal `env.yml` containing a valid `dependencies:` list plus a `category:` section" but never pastes the file, so the grader failed the check. But the commands are all shown (`conda env update --quiet --json -f env.yml 2>/dev/null | python3 -m json.tool`), the output is shown, and the input is described precisely enough to recreate: a valid dependencies list plus the unrecognized `category:` section that the issue names. A stranger can re-run it, and my wording was stricter than that.
- Fix: I changed the check so an input counts if it is shown, taken verbatim from the issue, or "described precisely enough to recreate". In the final run pkg-05 is accept, matching gold.
**Check rationale**
 
```
| steps-rerunnable | Repro report's steps and commands | A stranger could run the steps as written: the commands are shown, and each input is either shown, taken verbatim from the issue body, or described precisely enough to recreate (what it contains and which part triggers the behavior). A small input described in words that pin down the trigger passes; do not fail a step only because a file's contents are not pasted in full. Fails if the reproduction depends on a private file, repo, or config the reader cannot get, or if the step that triggers the behavior is missing or skipped. | required |
```
 
I first wrote this check as "exact commands or inputs are shown, nothing depends on private files". That wording failed pkg-05 and pkg-12, both clear accepts, because their reports describe an input file (or point at the issue's script) without pasting it. I rejected two options: dropping the check, because pkg-06 and pkg-18 need it to stay rejected, and keeping it strict, because it made good packages fail. The current wording keeps the real failures (private setup, skipped trigger step) and stops failing a report just for not pasting a small file.
 
**Trade-offs**
 
The check now passes a report whose input is only described in words, so a vague description could slip through. I accept that, because the wording requires the description to pin down what the input contains and which part triggers the behavior.
 
I checked that loosening it did not flip packages that were already right by re-running canaries with `--only`: pkg-06 (no environment record, driver omitted) and pkg-18 (reproduction in a private monorepo) both stayed reject, pkg-20 (the disclosure package) stayed reject, and pkg-07 stayed accept. The result was "agreement: 7/7 scored items".
 
One case I accept: pkg-03 passed in that partial run but failed in the final full run (on `honest-outcome`), so it is a borderline package where the grader varies between runs. I did not change the rubric to chase it, because the final run was already 19/20 and over the bar.
 
---
 
Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
