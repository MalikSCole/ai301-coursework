# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

1. In live mode only, read `scope.md` first and confirm the issue URL
   belongs to the scoped Path Review repo. If the repo line is still a
   placeholder or the issue is outside scope, stop without grading.
2. Read the repo facts. Note bug-report asks, contribution rules, AI-use
   disclosure rules, and any repo-specific testing or comment
   expectations.
3. Read the issue context and thread highlights. Note the reported
   behavior, expected behavior, labels, maintainer directions, rejected
   approaches, requested tests, and any existing workaround or prior art.
4. Read the repro evidence before the candidate plan. Record the exact
   reproduced command or steps, actual output, expected output, controls,
   and what cause those controls rule in or out.
5. Read the candidate plan. Mark the stated diagnosis, scope, files or
   areas, approach, test plan, risks, unknowns, and deviations.
6. Read the candidate plan comment last. Compare it to the plan, thread,
   and repo rules as a maintainer would see it.

## Evidence gathering

1. For `diagnosis`, copy the plan's cause claim and the smallest repro
   facts that support or disprove it, especially controls that isolate a
   subsystem or rule one out.
2. For `scope`, list the plan's in-scope work, not-in-scope work, named
   files or areas, and any extra work implied by the approach or comment.
3. For `executability`, list the concrete implementation decisions the
   plan has already made: files, functions, modules, algorithm choice,
   ordering, and what the first edit would be.
4. For `test_plan`, list each proposed test or verification command and
   the observable outcome it expects. Match each test to the repro step,
   control, or repo convention it proves.
5. For `honesty`, list risks, unknowns, deferrals, and deviations. Also
   record any place the plan states certainty where the issue or repro
   evidence is still ambiguous.
6. For `comms`, list maintainer directions, repo contribution or AI
   policy requirements, and the concrete promises in the candidate
   comment.

## Check execution

1. Grade checks in this order: diagnosis, scope, executability,
   test_plan, honesty, comms. Do not let a later well-written section
   rescue an earlier check that fails on evidence.
2. For each check, compare only the gathered facts named by the rubric
   and evidence guide. Grade the check, then write one evidence line
   naming the fact or short quote that decided it.
3. Grade `pass` when the pass condition is clearly satisfied from the
   package. Grade `fail` when the package clearly violates the pass
   condition.
4. Grade `unclear` when the needed evidence is absent, ambiguous, or
   internally inconsistent and the check cannot be verified from the
   package. Do not fill gaps with likely repo knowledge, assumptions, or
   live web results in eval mode.
5. A terse plan can pass if it makes the needed decisions. A polished or
   long plan must fail if it chooses the wrong cause, grows beyond the
   issue, leaves the build decisions to later, lacks a decisive test, or
   ignores thread or repo rules.

## Verdict assembly

1. Apply the rubric verdict rule exactly: accept only when every
   required check is `pass`; reject when any required check is `fail` or
   `unclear`.
2. In the readable summary, put each check on its own line with its
   grade and the deciding evidence. For rejects, make the first failing
   or unclear required check easy to find.
3. In the final JSON, include every rubric check with `name`, `grade`,
   and one-line `evidence`. The JSON verdict must be `accept` or
   `reject` and must match the rule above.
4. If live mode voice-guide notes exist, report them before the JSON.
   Voice-guide notes do not change the verdict unless the comms check
   also fails under the rubric.
