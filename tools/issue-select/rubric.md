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
| maintainer-active | "maintainer first-response sample" under Repo facts | At least one maintainer response in the sample occurred within the last 90 days | required |
| repo-active | "last push to any branch", "latest release", and "archived" under Repo facts | The repository is not archived and has had a push to any branch within the last 90 days | required |
| scope-fits-newcomer | Issue body and comment thread; labels and maintainer comments when present | The issue describes one bounded contribution, is not a usage/support question or umbrella/tracking issue, and does not require broad or architecture-level changes | required |
| not-already-claimed | Assignee field, linked PRs, and issue comment thread | The issue has no assignee, no open linked PR, and no comment indicating that someone has claimed or is actively working on it | required |
| contribution-policy | "contribution policy" under Repo facts | The repository has no stated ban on AI-assisted or AI-generated contributions | required |
| reproducible-context | Issue body and comment thread | The issue provides enough information to begin investigating, such as reproduction steps, an error message, or expected versus actual behavior | preferred |

## Verdict rule

Accept only if every required check passes. A single required check that fails rejects the issue. Unclear (?) on a required check counts as a fail. Preferred checks never affect the verdict; they only help rank issues that are accepted.

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->