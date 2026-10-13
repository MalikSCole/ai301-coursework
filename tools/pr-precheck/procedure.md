# Procedure: how this tool grades a PR package

<!--
THIS IS THE PART YOU WRITE (second week running for the procedure).
Week 3 you wrote these steps for a plan package; this week the graded
object is a PR package, and the read that matters most is a
side-by-side: the diff against the plan, the evidence against the test
plan, the description against both. Your week-3 procedure is the
pattern; do not paste it unchanged, because its read order was built
for a different object.

Your rotation is the design brief again, and this week friction routes
three ways: a stall on WHAT to decide is a rubric gap, a stall on
WHERE to look is a procedure gap (this file), and a stall on what the
tool even reads or outputs is a frame gap (your SKILL.md). A complete
procedure lets someone who has never seen a PR package before grade
one exactly the way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
plan's scope pair before opening the diff, and list the files the plan
names" is a step; "understand the change" is a wish.
-->

## Read order

1. In live mode only, read `scope.md` first and confirm the PR target
   belongs to the scoped Path Review repo. Stop if the repo is out of
   scope or the scope line is still a placeholder.
2. Read repo facts or live repo rules next: PR template asks,
   contribution policy, AI-use policy, required checklist, changelog,
   test, and issue-link conventions.
3. Read the issue and thread highlights. Note maintainer directions,
   rejected approaches, and the behavior the plan promised to fix.
4. Read the plan context before the diff. Record diagnosis, scope,
   not-in-scope items, named files, test plan, and deviation notes.
5. Read the candidate PR diff and commit list. Record changed files,
   meaningful behavior/doc changes, suspicious debris, and any work
   beyond or short of the plan.
6. Read the candidate PR title and description. Record what the PR
   claims changed, issue links, template sections, disclosures, and
   testing claims.
7. Read test evidence last so it can be matched to both the plan's test
   plan and the actual diff.

## Evidence gathering

1. For `plan_fidelity`, make a side-by-side list of plan promises and
   diff reality: files planned, files changed, work excluded, work
   delivered, deviations stated, and description claims.
2. For `test_evidence`, list each planned verification and each repo
   check, then match it to a command/output in the evidence. Mark
   whether the evidence demonstrates the before/after behavior or only
   a control/unchanged path.
3. For `diff_quality`, scan the unified diff and commits for unrelated
   files, debug prints, TODO/debug comments, dead code, commented-out
   experiments, formatting-only churn, and vague WIP commits.
4. For `standards_comms`, compare repo template/policy requirements to
   the PR title and description. Record missing issue links, empty
   sections, unchecked required checklist items, missing changelog
   entries, and missing AI-use disclosure where policy requires it.

## Check execution

1. Grade checks in this order: plan_fidelity, test_evidence,
   diff_quality, standards_comms. Do not let a later polished section
   rescue an earlier evidence failure.
2. Grade `pass` when the package clearly satisfies the rubric pass
   condition. Grade `fail` when the package clearly violates it.
3. Grade `unclear` when the needed evidence is absent, ambiguous, or
   internally inconsistent. In eval mode, do not fetch outside facts to
   clarify an unclear package.
4. Honest disclosure matters: a known shortfall or deferral can still
   pass plan_fidelity when it is stated in the plan/deviation note and
   repeated accurately in the PR description. Silent mismatch fails.
5. For each check, write one evidence line naming the specific fact,
   quote, file, or command output that decided the grade.

## Verdict assembly

1. Apply the rubric verdict rule exactly: accept only if every required
   check passes; reject if any required check fails or is unclear.
2. In the readable summary, show every check with its grade and
   deciding evidence. For rejects, put the first failing or unclear
   required check in rubric order first in the summary.
3. In the final JSON, include every rubric check with `name`, `grade`,
   and one-line `evidence`; set `verdict` to `accept` or `reject`.
4. In live mode, include voice-guide notes before the JSON. Voice notes
   do not alter the verdict unless a rubric check also fails.
