# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue


**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/37


**Verdict output**


```
issue-select verdict — live mode
item: https://github.com/codepath/pathreview-ai301-fa26-s3/issues/37
title: API reference doc is missing the `POST /profiles` request body schema
graded: 2026-09-22 (recency measured against today, not a capture date)
scope: in scope — repo matches skill/scope.md; Path Review house rule noted, not triggered (no comments)

Checks
- Maintainer activity        pass  Human collaborator Aburke225 pushed three commits to main on 2026-09-16 (6 days ago).
- Repository activity        pass  archived: false; last push to any branch 2026-09-16. No releases, which the pass condition allows on recent pushes.
- Bounded and settled scope  pass  One outcome: add request bodies for POST /profiles and POST /reviews to docs/API.md. Not an umbrella issue; the multipart-vs-JSON question is already settled in the body.
- Work is available          pass  assignees: []; timeline has only label events, no linked PRs; 0 comments; PR search for "37" returns none.
- Contribution policy        pass  docs/CONTRIBUTING.md states no AI/assistive-tool restriction; no AI_POLICY.md or AGENTS.md in the repo. Silence passes.
- Newcomer guidance (pref.)  pass  Labels 'good first issue' and 'tier-1'; body names docs/API.md, api/routes/profiles.py, api/schemas/review.py and estimates 2-3 hours.

Fit: Python/FastAPI docs task with the relevant files named up front and a stated expected outcome — matches the fit profile's preference for clear expected behavior and an obvious starting point. Documentation rather than backend logic.

Verdict: accept. Claim it in a comment regardless of other students' claims (house rule).

```json
{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/37",
  "checks": [
    {"name": "Maintainer activity", "grade": "pass",
     "evidence": "Human collaborator Aburke225 pushed default-branch commits on 2026-09-16, within 365 days."},
    {"name": "Repository activity", "grade": "pass",
     "evidence": "archived: false; last push to any branch 2026-09-16 (no releases, allowed by the condition)."},
    {"name": "Bounded and settled scope", "grade": "pass",
     "evidence": "Body asks for one change: add request bodies for POST /profiles and POST /reviews to docs/API.md; no umbrella list, no open design decision."},
    {"name": "Work is available", "grade": "pass",
     "evidence": "assignees: []; timeline has only label events, no linked PRs; 0 comments; PR search for '37' returns none."},
    {"name": "Contribution policy permits the workflow", "grade": "pass",
     "evidence": "docs/CONTRIBUTING.md states no AI/assistive-tool restriction and no AI_POLICY.md exists; silence passes."},
    {"name": "Newcomer guidance", "grade": "pass",
     "evidence": "Labels include 'good first issue' and 'tier-1'; body names docs/API.md, api/routes/profiles.py, api/schemas/review.py."}
  ],
  "verdict": "accept"
}
```

---



## Eval iterations

**Run history**

First full run:

> agreement: 17/20 scored items  (bar: 18/20: below the bar)

Targeted rerun on issue-01, issue-04, and issue-19:

> agreement: 3/3 scored items

Final full run:

> agreement: 19/20 scored items  (bar: 18/20: PASS)

**Issue analysis**

I analyzed `issue-15`.

My final run recorded:

> issue-15  reject  accept   NO     graded accept

The gold label describes the issue as:

> years of design debate and two abandoned PRs behind a friendly label

My rubric accepted the issue because my final scope check emphasized whether there was one identifiable change and whether a required product or design decision was still unresolved. The issue was not an umbrella or tracking issue, so the model treated it as sufficiently bounded.

The gold label instead treated the long history of design discussion and abandoned implementation attempts as evidence that the issue was not a good first contribution.

**Check rationale**

My final rubric contains this check:

> | Bounded and settled scope | Issue body and comment thread. Look for whether the issue asks for one concrete outcome, whether it is an umbrella/tracking issue, whether contributors must choose among multiple unrelated tasks, and whether a maintainer has left a required product/design decision unresolved. | Pass if the issue asks for one identifiable change or one bug/behavior to fix, even if the body is short, several files may be touched, or the implementation may be technically difficult. Fail if the issue is explicitly an umbrella/tracking/megaissue, asks contributors to select from multiple independent subprojects, or cannot be implemented until a required product/design choice is made. A maintainer-filed bug with a concrete observed behavior or named cause passes even if the exact implementation is not specified. | required |

I changed this check because my first full run incorrectly rejected issue-01, issue-04, and issue-19. The original version placed too much weight on how much implementation detail the issue contained. I revised it so a short or technically difficult issue can still pass when it has one clear requested outcome.

**Trade-offs**

The targeted rerun showed:

> issue-01  accept  accept   yes  
> issue-04  accept  accept   yes  
> issue-19  accept  accept   yes

So the revised scope check fixed all three false rejects.

The trade-off appeared in the final run:

> issue-15  reject  accept   NO     graded accept

Making the check more permissive helped correctly accept bounded issues that did not provide detailed implementation instructions, but it also made the rubric less sensitive to a long history of design debate and abandoned attempts.

I accepted that trade-off because the final run improved the clear-accept category from:

> clear-accept 5/8

to:

> clear-accept 8/8

and the final agreement reached:

> agreement: 19/20 scored items  (bar: 18/20: PASS)

**Selection rationale**


1. This issue fits me well because I have experience with Python, FastAPI, and backend APIs. It also seems realistic to finish in the available time because the task is documentation-focused, the relevant files are already named, and the expected work is limited in scope.

2. The verdict correctly identified that the issue is bounded, available, and has clear newcomer guidance. Beyond the rubric, I also considered that I am already comfortable reading API routes and schemas, so I should be able to understand the existing behavior without spending too much time learning a completely unfamiliar area.

3. I do not expect much difficulty claiming it. There are no assignees, linked pull requests, or comments, and the Path Review house rule means another student's claim would not block me anyway.
---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
