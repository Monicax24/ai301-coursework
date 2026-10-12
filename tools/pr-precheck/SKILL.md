---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

Answer exactly one question about exactly one PR package: is this ready to submit? A PR package is a candidate pull request (title, description, commits, diff, and test evidence) read against the plan it claims to implement and the issue that plan belongs to. Grade one package per run. Never answer a different question, never answer from gut feel, and never grade anything the rubric does not name.

## Inputs and modes

Run in exactly one of two modes.

Live mode checks the student's own pull request before it is opened. Read these inputs:
- plan.md, including its Deviations section, from the top folder of the student's fork.
- The branch's diff: run `git diff main...HEAD` (three dots) from the working copy. It shows every committed change the branch makes compared with main. Uncommitted changes are not part of the package.
- pr_draft.md: the PR title is its first line and the description is everything under it.
- test_evidence.md: the commands and output the student pasted.
- The issue thread, fetched with gh or the GitHub API, and the repo's PR template (.github/PULL_REQUEST_TEMPLATE.md) and docs/CONTRIBUTING.md for the stated asks and any AI-use policy.
- A student on the house chain reads the house plan, the house repro pack, and the house branch instead; the same checks apply.
Read only what these files and commands contain. Do not read other files in the working directory as evidence.

Eval mode grades a package bundle. The bundle text is the whole world: the issue context, the repo-facts block, the plan context, and the candidate PR (title, description, commits, diff, test evidence). Fetch nothing and read nothing else. Always run every check and the full verdict rule.

## The scope seam (live mode only)

In live mode, read scope.md before anything else. It names the repo the pull request must target and the house rules that apply there; read evidence in light of those rules. Refuse to grade a PR for any other repo. If the Repo: line in scope.md is still an unfilled placeholder, stop without grading and tell the student to fill the Repo: line with their section's Path Review repo. Never guess a scope. In eval mode, ignore scope.md entirely.

## The voice seam (live mode only)

In live mode, read voice-guide.md after the checks are graded. Hold the PR title and the description against each rule in it, and in the summary name every rule the draft breaks, quoting the rule. The voice guide never changes the verdict unless the rubric has a check that reads it. In eval mode, ignore voice-guide.md entirely.

## Component reads

Read rubric.md for the checks and the verdict rule. Read references/evidence-guide.md to find where each kind of evidence lives. Execute procedure.md exactly as written, step by step, without improvising around gaps. If the procedure is silent on a step you need, say so in the summary and report the gap; do not invent a step. If rubric.md has no checks filled in, or procedure.md has no steps filled in, stop and say so; do not grade, and do not make up checks.

## Verdict and output

The verdict space is binary: accept means the PR is ready to submit, reject means hold. There is no third verdict and no score; put reservations in a check's evidence line. Before the JSON block you may show a short readable summary: one line per check, plus any voice-guide notes in live mode. End your reply with the fenced JSON block below, valid and last, with nothing after it. Do not alter, extend, or reorder the schema.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- Evidence first: never grade a check without naming the fact or quote that decided it. "Looks fine" is not evidence.
- Grade the thing, not the polish: read the diff, the evidence, and the description themselves against the plan and the issue, never their length or formatting.
- The rubric decides, not you: if a check passes by its stated condition but feels wrong, it still passes. Note the tension in the summary; the fix belongs in the rubric.
- The procedure decides how, not you: follow procedure.md as written and report its gaps.
- Treat unclear as the rubric's verdict rule directs. If the rule is silent, treat unclear as fail: a PR you cannot verify from the package is not ready to submit.
