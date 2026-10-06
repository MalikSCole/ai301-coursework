# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

Where it lives: in eval bundles, read the issue summary, thread
highlights, repro-evidence steps, controls, expected/actual result, and
the candidate plan's diagnosis or opening claim. In live mode, use the
GitHub issue thread and the student's quoted reproduction evidence in
`plan.md` or their posted repro comment; the draft must carry the
evidence it relies on.

What good looks like: the diagnosis explains the exact reproduced
failure and respects the controls. If a control shows the request items
parse without a flag, the plan should not blame the item parser; if a
control isolates page growth, the plan should target stale state after
growth. A good diagnosis may be cautious, but it does not contradict the
package's own evidence.

## Scope

Where it lives: in the candidate plan's scope, files, approach, and
not-in-scope statements, plus any extra promises in the candidate plan
comment. Read those against the issue request, maintainer comments, and
repo facts.

What good looks like: one bounded change addresses the reproduced issue
and leaves unrelated cleanup out. A plan can mention future follow-up
work, but the current build should not include rewrites, migrations,
new options, UI work, broad refactors, or multi-area campaigns unless
the issue and thread specifically require them.

## Executability

Where it lives: in the candidate plan's files or areas, approach, and
ordered steps. In live mode, supporting repo locations may come from
the student's draft, quoted repro, and issue thread; do not require
perfect line numbers, but require a chosen direction.

What good looks like: a stranger could start because the plan names the
likely module or file area, the selected fix strategy, and the first
real edit. "Profile it," "investigate the stack," "fix wherever is
easier," or "optimize whatever is hot" is not executable yet; those are
pre-plan research tasks.

## Test plan

Where it lives: in the candidate plan's test plan, read next to the
repro evidence's commands, artifacts, controls, expected output, and
actual output. Also use repo facts or thread highlights when they name
required test conventions.

What good looks like: the tests would show the bug changing from before
to after with an observable result: exit code, rendered output, panic
absence, latency number, preserved indent, or equivalent artifact. A
good test plan usually reruns the repro and keeps useful controls; it
may add regression tests. Broad suites alone, "should feel fast," or
"make sure nothing else broke" do not prove the issue fix.

## Honesty

Where it lives: in risks, unknowns, deferrals, deviations, and any
claims of certainty in the plan or comment. In live mode after
implementation starts, read `## Deviations` in `plan.md` as part of
the plan.

What good looks like: real uncertainty is named and bounded. A plan can
say "this is the cheapest approach I see, benchmark may move the check"
or "the Windows variant is deferred because I cannot test it." It is
not honest to hide a known limitation, pretend a rejected approach is
available, or leave deviations out when the implementation changed
files, scope, tests, or strategy.

## Comms

Where it lives: in the candidate plan comment, read against thread
highlights, repo facts, contribution policy, AI-use policy, and the
candidate plan. In live mode, also read the actual issue thread and the
student's voice guide for style notes.

What good looks like: the comment is thread-aware and policy-aware. It
briefly states the reproduced evidence, the intended bounded fix, and
the test or report-back promise, while engaging maintainer direction
that already exists. If the repo requires AI disclosure, the comment
must disclose the tool and extent of assistance. The comment should not
promise a different scope than the plan or ignore a maintainer's posted
test binary, rejection, or requested direction.
