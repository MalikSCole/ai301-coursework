# Evidence guide: where evidence lives in a PR package

<!--
THIS IS THE PART YOU WRITE (third week running: the map stays in your
hands). Your tool uses this guide as its map: for every kind of
evidence a rubric check names, this file says WHERE to find it in a PR
package and WHAT GOOD LOOKS LIKE when you do.

The four families below are the harness's failure categories under
the names the eval README uses: plan fidelity = silent-drift, test
evidence = not-tested, diff quality = unreviewable, standards and
comms = standards-wall. A package that fails none of them is a
clear-accept. Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the plan-context block's scope pair and test
  plan, the candidate PR's diff, commits, description, or
  test-evidence section, the repo-facts block's template asks and
  stated policy). In live mode (where in your working copy and on
  GitHub: your plan.md and its deviation notes, your branch's diff,
  your draft title and description, your captured test output, the
  repo's PR template and CONTRIBUTING.md).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("every changed file falls inside the
  plan's stated boundary or a deviation note") over adjectives ("the
  diff is clean").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts three ways: your
procedure says WHEN to gather each family, this guide says WHERE, and
your SKILL.md says the tool reads both. Write the map you wish your
executor had.
-->

## Plan fidelity (harness category: silent-drift)

Where it lives: in eval bundles, read the Plan context for scope,
not-in-scope items, files, test plan, and deviations; read Candidate PR
title, description, commits, and diff for what actually changed and
what the PR claims. In live mode, read `plan.md` including
`## Deviations`, `git diff main...HEAD`, commit history, and
`pr_draft.md`.

What good looks like: every meaningful diff hunk is inside the plan or
an explicit deviation note, and the PR description accurately describes
what the diff delivers. Silent drift includes extra features, config
surface, refactors, unrelated docs, or less-than-plan work that the
description claims was completed.

## Test evidence (harness category: not-tested)

Where it lives: in eval bundles, read Candidate PR Test evidence
against the Plan context's test plan and repro evidence; also read repo
facts for expected checks. In live mode, read `test_evidence.md`, the
plan's test plan in `plan.md`, and the captured outputs for `make
test-unit`, `make test-integration`, `make lint`, `make typecheck`,
plus before/after repro evidence.

What good looks like: the evidence names commands and outcomes and
shows an observable behavior changing from before to after. It also
reports relevant repo checks honestly, including failures or expected
"no tests ran" output. Vague "tested locally," evidence for only a
control path, or omitting the planned decisive repro is not enough.

## Diff quality (harness category: unreviewable)

Where it lives: in eval bundles, read Candidate PR Diff and Commits.
In live mode, read `git diff main...HEAD --stat`, `git diff
main...HEAD`, and the branch commit list.

What good looks like: the diff is small enough to review for the issue,
the changed files are relevant, and there are no debug prints, dead
helpers, commented-out attempts, TODO imports, pure reformatting churn,
or unrelated hunks. The core fix can be correct and still fail if
reviewers must dig through debris to find it.

## Standards and comms (harness category: standards-wall)

Where it lives: in eval bundles, read Repo facts for PR template,
contribution policy, changelog/checklist asks, and AI-use policy; read
thread highlights for maintainer direction; read Candidate PR title and
description for compliance. In live mode, read the repo's PR template,
`docs/CONTRIBUTING.md` or equivalent policy files, the issue thread,
and `pr_draft.md`.

What good looks like: required template sections are filled with real
content, the issue is linked or closed when asked, required checklists
or changelog entries are addressed, and required AI-use disclosure is
present in the PR text. Boilerplate left empty, missing `Closes #...`,
or omitted AI disclosure when the repo requires it is a standards wall.
