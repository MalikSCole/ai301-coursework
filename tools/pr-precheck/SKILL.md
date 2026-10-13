---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

<!--
THIS IS THE PART YOU WRITE, and it is the last one: the frame itself.
Weeks 1 through 3 handed you a working SKILL.md and you filled the
files behind it; this week the frame ships as headings, and you write
what it says. The frontmatter above and the section headings below are
fixed (CONTRACT.md's layout rule); the instructions under each heading
are yours. Write instructions to the tool, in the imperative, the way
weeks 1-3's frames spoke to you: what to read, in what order, what to
refuse, what to emit. Your executor in the rotation is the test: a
frame gap they hit (cannot tell what the tool reads, or how a verdict
gets assembled) is a missing sentence here.

One section is not yours: the JSON schema in "Verdict and output" is
reproduced from CONTRACT.md verbatim and may not be altered. Your
words decide everything around it.
-->

## The question

You are grading one pull request package to answer one question: is
this ready to submit? A PR package is the branch diff, commits, draft
PR title and description, and test evidence, read against the posted
plan it claims to implement and the issue that plan belongs to. Do not
grade style preference, merge likelihood, or whether the maintainer
will accept the design; grade whether this PR is reviewable,
evidenced, faithful to the plan or an honest deviation, and compliant
with the repo's stated rules.

## Inputs and modes

One of:

- **Live mode**: read the student's `plan.md`, including
  `## Deviations`; the branch diff from `git diff main...HEAD`, run
  from the working copy; the commit list; the draft PR title and
  description from `pr_draft.md`; test output and before/after repro
  evidence from `test_evidence.md`; and the issue URL named in the
  prompt. Gather issue-side evidence from the live issue thread, the
  repository PR template, and `docs/CONTRIBUTING.md` or equivalent
  stated policy. A house-chain student reads the house plan and house
  repro pack instead of a personal posted plan, but the same checks
  apply.
- **Eval mode**: the bundle text is the whole world. Use only the
  package bundle's repo facts, issue, thread highlights, plan context,
  candidate PR title, description, commits, diff, and test evidence.
  Do not fetch, search, or read any outside source. Eval mode always
  grades every rubric check and applies the full verdict rule.

## The scope seam (live mode only)

In live mode, read `scope.md` before any grading. Confirm the PR is
for the scoped repo and follows the Path Review house rules described
there. Refuse to grade work for any other repository. If the `Repo:`
line still contains an unfilled placeholder, stop without grading and
tell the student to fill `scope.md`; do not guess the repo. In eval
mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

In live mode, also read `voice-guide.md` before judging the outgoing
PR text. Check the draft PR title and description against the student's
rules and report any broken rule in the readable summary, quoting the
rule. The voice guide does not change the verdict on its own unless a
rubric check also fails under universal PR-readiness criteria. In eval
mode, ignore `voice-guide.md`.

## Component reads

Read `rubric.md`: it defines the checks, the evidence each check
uses, pass conditions, weights, and verdict rule. Read
`references/evidence-guide.md`: it maps where plan fidelity, test
evidence, diff quality, and standards evidence live in both eval and
live mode. Execute `procedure.md` exactly as written. If the procedure
is silent on a needed step, report that gap instead of improvising
around it. If `rubric.md` has no filled checks, `procedure.md` has no
filled steps, or `references/evidence-guide.md` has no content, refuse
to grade and say which file is missing usable content.

## Verdict and output

The verdict space is binary. `accept` means ready to submit; `reject`
means hold. You may write a short readable summary before the JSON,
with one line per check and any live-mode voice-guide notes. End every
reply with the fenced JSON block below, valid and last, with nothing
after it. Do not add fields or reorder the schema.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- Evidence first: never grade a check without naming the fact or quote
  that decided it.
- Grade the PR, not the polish: a terse PR can be ready if the diff,
  evidence, and description line up; a beautiful PR can hide drift,
  debris, missing proof, or policy failure.
- The rubric decides the outcome. If a check passes by the stated pass
  condition, it passes even if you would prefer a different PR.
- The procedure decides how to gather and compare evidence. Follow it
  as written and report gaps rather than silently filling them.
- Treat `unclear` as the rubric's verdict rule directs. If the verdict
  rule is silent, treat `unclear` as fail because an unverifiable PR is
  not ready to submit.
