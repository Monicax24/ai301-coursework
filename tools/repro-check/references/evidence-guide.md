# Evidence guide: where proof lives in a reproduction package

## Environment

Feeds the checks env-recorded and faithful-target.

- Where it lives, eval bundle: the first lines of the candidate repro report (OS, tool version, shell, driver, build profile); the repo-facts block for what the repo's bug template asks for; the issue body and thread highlights for the target the reporter and maintainers name (versions confirmed on latest or main, the OS or shell involved, maintainer notes on what triggers it).
- Where it lives, live mode: the top of the student's repro draft; the issue body and comments on GitHub; the repo's .github/ISSUE_TEMPLATE/ folder.
- What good looks like: the report names the OS, the tool's version, and any setting the issue says changes the outcome, in a line or two. The version and setup tested match what the issue targets, or the report names each difference (older version, different OS, changed input) and does not present the result as proof about the reported bug. A report with no environment record fails, even when its log excerpt looks right.

## Steps

Feeds the check steps-rerunnable.

- Where it lives, eval bundle: the numbered or listed steps and commands in the candidate repro report. Live mode: the same section of the student's draft, read as a stranger would read the posted comment.
- What good looks like: a stranger can run it from a clean machine. The commands are shown. Each input is shown, taken verbatim from the issue body (the report says so), or described precisely enough to recreate, saying what it contains and which part triggers the behavior. Nothing depends on a private repo, file, or config the reader cannot get, and the step that triggers the behavior is included, so there is no jump from "set up the project" to the result. A small input described in words that pin down the trigger passes. A reproduction that lives in a private setup fails.

## Behavior shown

Feeds the check shows-issue-behavior.

- Where it lives, eval bundle: the pasted output, logs, or transcripts in the candidate repro report, read against the behavior described in the issue body (the exact error text, exit code, or symptom). Live mode: the output pasted in the draft, read against the issue body on GitHub.
- What good looks like: the artifact itself shows the reported behavior: the same error, the same exit code, the same symptom. Fail it when the output is an adjacent behavior: a graceful error where the issue reports a crash, a different error caused by an input the author modified, output that only proves the tool runs (a version banner, a session list), or the old behavior of a different version. In an honest cannot-reproduce, the artifact shows a real attempt and what it produced instead.

## Honesty

Feeds the check honest-outcome.

- Where it lives, eval bundle: the stated outcome in the repro report and in the claim comment, set side by side with the artifacts the comments actually show. Live mode: the same, in the drafts.
- What good looks like: every claim has an artifact behind it. "Reproduced" has output that shows the behavior; a root cause is labeled a hypothesis unless evidence supports it; a cannot-reproduce says what was tried and what differed, and passes. Fail a confident claim with no artifact ("I verified this race condition", "guaranteed reproducible"), and fail a claim that goes beyond what the artifact shows, such as a narrated crash over a graceful error.

## Comms

Feeds the checks claim-specific and repo-conventions.

- Where it lives, eval bundle: the candidate claim comment read against the issue (is anything in it specific to this issue?); the repo-facts block for the stated contribution policy, including any AI-use policy; both comments read against that policy. Live mode: the student's claim draft against the issue on GitHub; the repo's CONTRIBUTING.md and any AI-use section.
- What good looks like: the claim names something only this issue has (the command, function, error, or behavior) and promises only an investigation and a report, with no fix promised, no date, and no guarantee. Boilerplate "assign me" text that fits any issue fails, and so does a +1. For conventions: if the policy requires disclosing AI assistance, the comments disclose it (treat course packages as AI-assisted work for this rule only); if it requires comments to be written by a human in their own words, a first-person comment with its own specifics passes and only generic or templated text fails; a permissive or silent policy passes.

## Live mode on GitHub (where to look)

- Issue body and comments: gh issue view <number> --repo <org/repo> --comments
- Contribution policy: the repo's CONTRIBUTING.md and any AI-use section
- Bug template: .github/ISSUE_TEMPLATE/
- The drafts are the candidate side: grade only what they contain and quote, since a stranger reads only the posted comments.