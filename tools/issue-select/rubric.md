# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| unclaimed | Repo-facts block: assignees and linked PRs; comment thread | No assignee and no open linked PR (a closed linked PR does not count), and no comment dated within the 90 days before the snapshot date in which someone says they are working on it or asks to take it. A claim comment older than 90 days with no assignee and no open PR is stale and does not count. | required |
| maintainer-responsive | Repo-facts block: maintainer first-response sample and last 5 default-branch commits | At least one issue in the sample has a maintainer first response within 60 days, OR the last 5 default-branch commits include a commit within 14 days of the snapshot date. Issues opened within 7 days of the snapshot date are ignored in the sample, because they haven't had time to get a reply. | required |
| repo-active | Repo-facts block: release recency and commit activity | At least one commit to the default branch within the last 90 days, or a release within the last 12 months | required |
| policy-allows | Repo-facts block: contribution policy line | Fail if the policy forbids or does not accept AI-generated or AI-assisted code or documentation, forbids outside contributions, or requires approval or assignment first that has not been given. A policy that is silent, or that welcomes AI tools with review or disclosure requirements, passes. | required |
| scope-fits | Issue body and comment thread | The issue describes one bounded problem or change (a single bug, or a docs or feature change with a named target) that a newcomer could work on without private access or special hardware. A terse description, no comments, or an unknown root cause does not fail this check. Fail only if the work clearly spans a redesign, many components, or an open-ended research task. Also fail if the issue itself marks a required input or decision as TBD, undecided, or unknown (for example "asset TBD"), so the work cannot be started from the issue alone. | required |
| clear-description | Issue body | States the expected behavior and how to reproduce it, or exactly what to change | preferred |
| good-first-label | Issue labels | Labeled good first issue, help wanted, or similar | preferred |


## Verdict rule

Accept if every required check passes. Reject if any required check fails. Preferred checks never change the verdict; they only rank accepted issues. Treat unclear as fail.
