# Rubric: is this pull request ready to submit?

<!--
THIS IS THE PART YOU WRITE (fourth week running; this is the rubric's
final form in the sandbox). Your frame in SKILL.md executes whatever
checks you define here, via your procedure.md. It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the diff read against the plan's scope, the test
     evidence read against the plan's test plan, the description read
     against the diff, the repo-facts block's template asks) or a
     location from your references/evidence-guide.md. "The PR" is not
     a source; "the diff's changed files read against the plan's
     stated boundary" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself
     (does the diff fall inside the plan plus its deviation notes? is
     the claimed evidence observable?), never the write-up's shape
     (how long the description is, how many commits there are).
     Structure-shaped checks are what make graders disagree with
     themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (submit) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. State the `unclear`
   treatment explicitly: the frame here is YOUR SKILL.md, so a rubric
   that stays silent is only covered if your frame's grading
   discipline says what happens (the contract's own default is that
   an unverifiable claim fails).

Cover what actually gets bad PRs submitted. The failure families the
lecture named ARE the harness's scoring categories, same names as the
eval README: silent drift (the diff silently does more or less than
the posted plan, or the description claims fidelity the diff
contradicts), not tested (the evidence proves nothing observable, or
the repo's own checks were never run), unreviewable (debris or
unrelated hunks bury the change), and standards wall (the repo's
stated template and disclosure asks are ignored). Your evidence
guide's four headings map onto these one to one (plan fidelity =
silent drift, test evidence = not tested, diff quality =
unreviewable, standards and comms = standards wall), and the category
floor is scored on exactly these names plus clear accept. A rubric
that ignores a category will fail the eval packages built around
that category. And remember the honest-outcome
rule, fourth week running: a PR that honestly discloses a shortfall
can be ready; a rubric that equates "less than everything" with
"hold" fails the set.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| plan_fidelity | Plan context scope, not-in-scope items, files, test plan, and deviation notes read against the candidate PR diff, commits, title, and description. | Pass if every meaningful changed file and behavior is inside the posted plan or an explicit honest deviation, and the PR description does not claim work the diff lacks or hide work the plan scoped out. Fail if the diff silently does more, does less, or says it followed the plan while contradicting it. | required |
| test_evidence | Candidate test evidence read against the plan's test plan, the reproduction's before/after behavior, and the repo checks or test commands named by repo facts or the PR template. | Pass if the PR shows observable before/after evidence for the reproduced issue and reports relevant repo checks with commands and outcomes, including honest failures or expected no-test cases. Fail if evidence is vague, exercises an unchanged path, omits the plan's decisive repro, or never shows the repo checks were run. | required |
| diff_quality | Candidate PR unified diff and commit list, read against the issue and plan scope. | Pass if the diff is reviewable: the fix is visible, changed files are related, and there are no debug leftovers, dead code, commented-out experiments, formatting churn, or drive-by edits that obscure review. Fail if unrelated hunks or debris make the PR harder to review even when the core fix is right. | required |
| standards_comms | Repo facts for PR template asks, contribution policy, AI-use policy, and maintainer directions, read against the candidate PR title and description. | Pass if the title and description satisfy required template sections, link or close the issue when asked, include required changelog/checklist/disclosure items, and engage explicit maintainer direction. Fail if a visible repo requirement is ignored, boilerplate is left empty, or required AI-use disclosure is missing. | required |

## Verdict rule

Accept only if every required check is `pass`. Reject if any required
check is `fail` or `unclear`. Treat `unclear` as fail because a PR that
cannot be verified from the package is not ready to submit. Preferred
checks, if added later, may be reported but never change the verdict.
