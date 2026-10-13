# Unit 4 — Pull Request

Path: `beat-1-sandbox/unit-4/pull-request.md`

---

## Pull request

**PR URL**

https://github.com/codepath/pathreview-ai301-fa26-s3/pull/189

**Branch**

fix/37-api-request-body-docs

## Eval iterations

**Run history**

1. Final saved run: `agreement: 20/20 scored items  (bar: 18/20: PASS)`.

**Package analysis**

`pkg-20` was a reject in both the gold label and my rubric's final run. The package had a bounded, well-evidenced Ghostty fix, but the repo facts said Ghostty has a strict AI policy requiring disclosure of all AI usage. The candidate PR description omitted that disclosure, so my `standards_comms` check rejected it even though the implementation itself was otherwise ready.

**Check rationale**

Quoted check from `tools/pr-precheck/rubric.md`:

~~~~text
| standards_comms | Repo facts for PR template asks, contribution policy, AI-use policy, and maintainer directions, read against the candidate PR title and description. | Pass if the title and description satisfy required template sections, link or close the issue when asked, include required changelog/checklist/disclosure items, and engage explicit maintainer direction. Fail if a visible repo requirement is ignored, boilerplate is left empty, or required AI-use disclosure is missing. | required |
~~~~

I made this required because a PR can be technically correct but still not ready to submit when it ignores the repo's template, issue-linking rule, or disclosure policy. The eval set includes standards-wall packages where the code is good but the PR is not submit-ready.

**Trade-offs**

The `standards_comms` check can reject a PR whose diff and tests are otherwise strong. I accept that strictness because repository policies and required disclosure are part of upstream review, not optional polish. The check is conditional on visible repo requirements so it does not penalize projects that do not ask for a checklist, changelog, or AI disclosure.
