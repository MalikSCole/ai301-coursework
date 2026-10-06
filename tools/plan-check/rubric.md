# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis | The candidate plan's stated cause and target behavior, read against the issue context and the repro-evidence steps, controls, expected result, and actual result. | Pass if the plan's diagnosis explains the reproduced behavior without contradicting the repro evidence or ignoring a control that rules the diagnosis out. Fail if it blames a cause the repro evidence disproves, treats a symptom as the cause, or cannot name what behavior the fix is meant to change. | required |
| scope | The candidate plan's scope, files/areas, in-scope and not-in-scope claims, and approach, read against the issue, thread highlights, and repo facts. | Pass if the plan is one bounded change that addresses the reproduced issue and explicitly leaves unrelated refactors, redesigns, migrations, options, and nice-to-have cleanup out. Fail if the issue fix is bundled with drive-by work or a broader rewrite that the issue and thread do not require. | required |
| executability | The candidate plan's files/areas, approach, ordered steps, and named implementation decisions, read with the repo facts and thread highlights. | Pass if a stranger could start the implementation from the plan because it names the likely code area, chosen approach, and first concrete edits. Fail if the plan mainly says to investigate, optimize, fix whatever is found, or choose among major approaches later. | required |
| test_plan | The candidate plan's test plan, read against the repro-evidence commands, controls, expected/actual outputs, and any repo test conventions in repo facts or the thread. | Pass if the test plan names an observable before/after result that would prove the reproduced issue changed, plus relevant regression or existing tests when appropriate. Fail if it only says to run broad suites, check that things feel better, or verify no unrelated breakage without tying back to the repro. | required |
| honesty | The candidate plan's risks, unknowns, deferrals, deviations, and certainty claims, read against the issue, thread highlights, and repro evidence. | Pass if material uncertainty is named honestly and bounded without blocking the core fix. Fail if the plan presents unresolved choices as settled, hides a known limitation, or ignores evidence that should make the plan conditional. | required |
| comms | The candidate plan comment, read against thread highlights, repo facts, contribution policy, AI-use policy, and the plan itself. | Pass if the comment accurately summarizes the grounded plan, responds to explicit maintainer direction or repo policy, and includes any required disclosure. Fail if it ignores a maintainer's requested direction, promises a plan different from the draft, overpromises timing, or omits a required AI-use disclosure. | required |

## Verdict rule

Accept only if every required check is `pass`. Reject if any required
check is `fail` or `unclear`. Treat `unclear` as a fail because a plan
that cannot be verified from the package is not ready to post or build
from. Preferred checks, if any are added later, may be reported but
never change the verdict.
