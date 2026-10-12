# Unit 1 — Issue Selection
 
Path: `beat-1-sandbox/unit-1/selection.md`
 
Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.
 
Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.
 
---
 
## Selected issue
 
**Issue link**
 
https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72
 
**Verdict output**
 
**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.
 
```
claude "issue-select: grade these candidate first issues: https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73 https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72 https://github.com/codepath/pathreview-ai301-fa26-s3/issues/71"
 
I graded all three against your rubric, and the rubric accepts all three. Two things to know before you trust that result, though.
 
1. Every issue already has open pull requests from classmates. No issue has an assignee, but each has open PRs from students: #73 has 9 (#85, #112, #137, #150, #157, #160, #163, #166, #169), #72 has #78, and #71 has #86. Your unclaimed check says "no open linked PR". The Path Review house rule in scope.md says to "ignore the usual claim signals" from classmates because "a shared issue costs nobody anything." I read that as covering classmates' PRs as well as their comments, so unclaimed passes. If you read the house rule as covering comments only, unclaimed fails and all three are rejected. Change the wording in scope.md or rubric.md so it gives one answer.
 
2. maintainer-responsive passes, but only on a technicality. The only maintainer comments in the whole repo are on #43 and #52, both posted on 2026-09-16. They are the maintainer closing issues they opened themselves. That meets your "first response within 60 days" condition. But no maintainer has answered any student comment or PR, and the last commit was 26 days ago, which misses your 14-day option. If you want "responds to contributors," the rubric has to say so.
 
Ranking. Your fit profile in scope.md is still the placeholder "(Write a few sentences here.)", so I couldn't rank by fit. I ranked by your preferred checks instead, and where they tied I used how crowded the issue is. That tiebreak is my call, not your rubric's.
 
1. #72 verify_password raises on malformed hashes. It has the good-first-issue label, a clear expected behavior (return False), and an existing xfail test to turn green. It's a small code change plus a test, with one competing PR.
2. #73 README and .env.example disagree. It has the label and a clear target, but it's a docs-only change with nine competing PRs already open.
3. #71 Indented heading fixture. Bounded and clear, but it has no good-first-issue label and is tagged tier-2.
 
Shared repo facts. The repo isn't archived. The last commit was on 2026-09-16, within your 90-day window. docs/CONTRIBUTING.md says nothing about AI use and only asks you to comment on the issue before working on it, which isn't an approval gate.
 
[
{
"item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72",
"checks": [
{"name": "unclaimed", "grade": "pass", "evidence": "No assignee; open PR #78 and ~20 claim comments are all by classmates (author_association NONE), which the house rule says not to count"},
{"name": "maintainer-responsive", "grade": "pass", "evidence": "Maintainer Aburke225 commented on #43 and #52 on 2026-09-16, 6 days after they were opened (both are the maintainer's own issues)"},
{"name": "repo-active", "grade": "pass", "evidence": "Last default-branch commit 2026-09-16 (26 days ago, within 90)"},
{"name": "policy-allows", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and the PR template say nothing about AI use; contributors only need to comment on the issue, no approval gate"},
{"name": "scope-fits", "grade": "pass", "evidence": "One function in core/security.py should return False instead of raising, plus removing the xfail marker in tests/unit/test_security.py"},
{"name": "clear-description", "grade": "pass", "evidence": "\"Verification against a malformed hash should fail closed (return False), not raise.\""},
{"name": "good-first-label", "grade": "pass", "evidence": "Labels: bug, good first issue, api, tier-1"}
],
"verdict": "accept"
},
{
"item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73",
"checks": [
{"name": "unclaimed", "grade": "pass", "evidence": "No assignee; 9 open PRs (#85-#169) and many claim comments, all by classmates (NONE), which the house rule says not to count"},
{"name": "maintainer-responsive", "grade": "pass", "evidence": "Maintainer Aburke225 commented on #43 and #52 on 2026-09-16, 6 days after they were opened (both are the maintainer's own issues)"},
{"name": "repo-active", "grade": "pass", "evidence": "Last default-branch commit 2026-09-16 (26 days ago, within 90)"},
{"name": "policy-allows", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and the PR template say nothing about AI use; no approval gate"},
{"name": "scope-fits", "grade": "pass", "evidence": "Make README.md and .env.example agree on the LLM key; two named files"},
{"name": "clear-description", "grade": "pass", "evidence": "\"README.md tells you to add OPENROUTER_API_KEY ... .env.example doesn't list that variable ... Make the two files agree.\""},
{"name": "good-first-label", "grade": "pass", "evidence": "Labels: bug, good first issue, docs, tier-1"}
],
"verdict": "accept"
},
{
"item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/71",
"checks": [
{"name": "unclaimed", "grade": "pass", "evidence": "No assignee; open PR #86 and the claim comments are by a classmate (nancyAfycodes, NONE), which the house rule says not to count"},
{"name": "maintainer-responsive", "grade": "pass", "evidence": "Maintainer Aburke225 commented on #43 and #52 on 2026-09-16, 6 days after they were opened (both are the maintainer's own issues)"},
{"name": "repo-active", "grade": "pass", "evidence": "Last default-branch commit 2026-09-16 (26 days ago, within 90)"},
{"name": "policy-allows", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and the PR template say nothing about AI use; no approval gate"},
{"name": "scope-fits", "grade": "pass", "evidence": "Remove the 8-space indent from one test fixture and drop the xfail marker in tests/unit/test_readme_parser.py"},
{"name": "clear-description", "grade": "pass", "evidence": "\"builds its markdown from lines indented by eight spaces ... Remove the indentation.\""},
{"name": "good-first-label", "grade": "fail", "evidence": "Labels: bug, ingestion, tier-2; no good-first-issue or help-wanted label"}
],
"verdict": "accept"
}
]
 
```
 
---
 
## Eval iterations
 
Quote source text directly in each field below. Paraphrase does not satisfy them.
 
**Run history**
 
1. Smoke run with `--limit 3` (partial, not scored): "agreement: 2/3 scored items"
2. Full run: "agreement: 17/20 scored items" (misses: issue-09, issue-11, issue-19)
3. Full run: "agreement: 17/20 scored items" (misses: issue-12, issue-19, issue-20)
4. Final full run, saved with `--save-run eval-run.txt`: "agreement: 19/20 scored items"
The last score, 19/20, matches the agreement line in the `eval-run.txt` I committed.
 
**Issue analysis**
 
issue-12 (bookwyrm-social/bookwyrm#1133, "Include in-progress books in the reading-goal progress-bar").
 
- Gold label: reject.
- My rubric's decision in run 3: accept ("issue-12  reject  accept   NO     graded accept").
- Why my rubric accepted it: the bundle's contribution policy line reads "We do not accept AI-generated code or documentation." My `policy-allows` check at that point said the policy must not "forbid outside contributions, require prior approval or assignment that has not been given, or ban the kind of work this issue needs". An AI ban is none of those three things, so the check passed. The other checks also passed: the last commit was 2026-08-12, the issue has the "good first issue" label, and the 2024 claim comment from jrings was older than my 90-day stale-claim window, so `unclaimed` no longer caught it either. The policy was the only signal left, and my rubric had no wording for it.
- Fix: I rewrote `policy-allows` to name AI bans explicitly. The final run rejects it.
**Check rationale**
 
```
| policy-allows | Repo-facts block: contribution policy line | Fail if the policy forbids or does not accept AI-generated or AI-assisted code or documentation, forbids outside contributions, or requires approval or assignment first that has not been given. A policy that is silent, or that welcomes AI tools with review or disclosure requirements, passes. | required |
```
 
The first clause ("forbids or does not accept AI-generated or AI-assisted code or documentation") is there because of issue-12, whose policy says "We do not accept AI-generated code or documentation." The last sentence is there to avoid over-rejecting. The conda issues (issue-01, issue-09) have a policy that says "generative AI tools welcome," and the bundles for zxlive and excalidraw say "no statement on AI or contribution tooling." Those should still pass, so silent and AI-welcoming policies pass.
 
**Trade-offs**
 
This check gives up two things. First, it rejects every issue in a repo that bans AI-generated code, even though a contributor who writes the code by hand could still contribute. I accept that, because the maintainers stated the rule and a newcomer's first PR is a bad place to test it. Second, it passes a repo whose policy is silent, so a repo with an unwritten anti-AI norm gets through. The check can only read what is written in the policy line of the bundle. A separate case I accept missing is issue-19 (zxlive#517), a scope call where my rubric rejects and gold accepts.
 
---
 
## Selection rationale
 
**Selection rationale**
 
1. **Fit and time.** Issue #72 is a small Python bug fix: one function in `core/security.py` should return `False` for a malformed hash instead of raising, and an existing `xfail` test in `tests/unit/test_security.py` should turn green. That is a few hours of work, which fits the time I have, and I'd rather start with a small, testable backend change than a large one. (Edit this line to say what actually interests you.)
2. **What the verdict got right, and what it couldn't weigh.** The verdict correctly found a bounded problem with clear expected behavior (return `False`, remove the `xfail` marker), the "good first issue" label, and no AI policy or approval gate in `docs/CONTRIBUTING.md`. What the rubric could not weigh: my fit profile in `scope.md` is still the placeholder "(Write a few sentences here.)", so it could not rank by my interests. It also could not decide whether classmates' open PRs count as claims. It passed `unclaimed` only by reading the house rule as covering PRs as well as comments, and it flagged that as a wording problem in my rubric. Finally, `maintainer-responsive` passed on a technicality, because the only maintainer comments are on the maintainer's own issues.
3. **Anticipated difficulty in claiming it.** PR #78 is already open on #72, and there are about 20 claim comments from classmates, so this is a shared issue and I won't be first. The maintainer (Aburke225) has not answered any student comment or PR that I can see, so I shouldn't expect a quick reply. My claim comment should be specific and short, and I should start from the existing `xfail` test so my change is easy to compare with #78.
---
 
Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
