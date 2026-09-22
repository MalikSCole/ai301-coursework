# Rubric: is this a good first issue?

<!--

THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md).
   - Pass condition: a condition someone else could apply and get your
     answer.
   - Weight: `required` or `preferred`.

2. A verdict rule below the table.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it.

-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Maintainer activity | Repo-facts block: last 5 default-branch commits and maintainer first-response sample. In live mode, use the default-branch commit history and recent issue responses described in `references/evidence-guide.md`. | Pass if there is at least one non-bot default-branch commit within the last 365 days or at least one Owner, Member, or Collaborator response in the response sample within 90 days. A bot merge of a human PR may count as activity when the underlying contribution is clearly human-authored. | required |
| Repository activity | Repo-facts block: archived flag, last push to any branch, and latest release. In live mode, check the repository archived banner, latest push/commit date, and Releases section. | Pass only if the repository is not archived and either the last push to any branch or the latest release occurred within the last 365 days. A repository with no releases can still pass based on recent pushes. | required |
| Bounded and settled scope | Issue body and comment thread. Look for whether the issue asks for one concrete outcome, whether it is an umbrella/tracking issue, whether contributors must choose among multiple unrelated tasks, and whether a maintainer has left a required product/design decision unresolved. | Pass if the issue asks for one identifiable change or one bug/behavior to fix, even if the body is short, several files may be touched, or the implementation may be technically difficult. Fail if the issue is explicitly an umbrella/tracking/megaissue, asks contributors to select from multiple independent subprojects, or cannot be implemented until a required product/design choice is made. A maintainer-filed bug with a concrete observed behavior or named cause passes even if the exact implementation is not specified. | required |
| Work is available | Repo-facts block for this issue: assignees and linked PRs; issue comment thread for statements that somebody is actively working on it. | Pass if there is no current assignee, no open linked PR, and no recent comment showing another contributor is actively implementing the issue. Closed or merged PRs do not by themselves fail the check. A stale claim does not fail if there is no active PR/assignee and a later maintainer message invites new contributors or otherwise makes the issue available again. | required |
| Contribution policy permits the workflow | Repo-facts contribution-policy entry and the contribution-policy location named in `references/evidence-guide.md`. | Pass if there is no stated restriction that prevents this course workflow, or if AI/assistive tools are allowed when the contributor reviews, understands, tests, and takes responsibility for the work. Fail if the repository explicitly refuses AI-generated code or documentation. A policy that merely discourages generative AI or requires meaningful human review does not automatically fail. | required |
| Newcomer guidance | Issue labels, issue body, and comment thread. | Pass this preferred check if at least one of these is present: a `good first issue` or equivalent newcomer label, explicit acceptance criteria, named files/components or a "where to start" pointer, a concrete reproduction, or a maintainer statement indicating the issue is suitable for contributors. | preferred |

## Verdict rule

Accept an issue only when every required check passes.

A failed required check produces a `reject` verdict.

For required checks, treat `unclear` as a failure unless the check's pass condition explicitly states that absence of a signal is acceptable.

For example, having no stated AI policy does not fail the contribution-policy check, but being unable to determine whether an issue has an active assignee or open linked pull request is `unclear` and therefore fails the availability check.

Preferred checks never change an `accept` or `reject` verdict. Use them only to rank issues that already passed every required check.