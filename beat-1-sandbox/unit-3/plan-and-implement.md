# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

---

## Posted upstream

**GitHub username**

MalikSCole

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/37#issuecomment-6020285677

Exact posted text:

~~~~text
I reproduced this by comparing `docs/API.md` with the backend definitions for the two endpoints named in the issue. The docs currently only list one-line summaries for `POST /profiles` and `POST /reviews`, while the backend shows the missing request-body details:

- `POST /profiles` uses multipart form data in `api/routes/profiles.py`: `github_username`, `portfolio_url`, and `resume_file`.
- `POST /reviews` accepts a JSON body defined by `ReviewCreate` in `api/schemas/review.py`: `profile_id`.

My plan is a docs-only update to `docs/API.md`: add request body tables and examples for both endpoints, explicitly noting that `POST /profiles` is `multipart/form-data` rather than JSON. I will verify the change by re-running the same `rg` comparison against `docs/API.md`, the route files, and the schema files so the documented fields match the implementation.
~~~~

## Your branch

**Branch**

docs/37-api-request-body-docs

**Evidence**

Before evidence from Unit 2:

~~~~text
Command:
rg -n "POST /profiles|POST /reviews|multipart|github_username|portfolio_url|resume_file|profile_id|request body|request-body" docs api -S

Observed:
- docs/API.md only has one-line summaries for the two endpoints:
  - line 18: `POST /profiles` — Create a profile with resume and GitHub username.
  - line 24: `POST /reviews` — Request a new portfolio review for a profile.
- The POST /profiles backend route defines request inputs that are not documented in docs/API.md:
  - github_username: str = Form(default=None) in api/routes/profiles.py
  - portfolio_url: str = Form(default=None) in api/routes/profiles.py
  - resume_file: UploadFile = File(default=None) in api/routes/profiles.py
- api/schemas/profile.py confirms the profile fields include optional github_username and portfolio_url.
- The POST /reviews backend route accepts data: ReviewCreate, and api/schemas/review.py defines that request body as:
class ReviewCreate(BaseModel): profile_id: UUID
~~~~

After evidence from the implementation branch:

~~~~text
Command:
rg -n "POST /profiles|POST /reviews|multipart/form-data|github_username|portfolio_url|resume_file|profile_id" docs/API.md api/routes/profiles.py api/routes/reviews.py api/schemas/review.py api/schemas/profile.py

Output excerpt:
docs/API.md:18:`POST /profiles` — Create a profile with resume and GitHub username.
docs/API.md:20:Request body: `multipart/form-data`
docs/API.md:24:| `github_username` | string | No | GitHub username to associate with the profile. | `octocat` |
docs/API.md:25:| `portfolio_url` | string | No | Portfolio or personal website URL for the profile. | `https://octocat.dev` |
docs/API.md:26:| `resume_file` | file | No | Resume upload. Accepted file types are PDF, Markdown, or plain text. | `resume.pdf` |
docs/API.md:43:`POST /reviews` — Request a new portfolio review for a profile.
docs/API.md:49:| `profile_id` | UUID string | Yes | ID of the profile to review. | `8d1f3d3d-7b1f-4d8f-9f2b-1c2a3b4c5d6e` |
docs/API.md:55:  "profile_id": "8d1f3d3d-7b1f-4d8f-9f2b-1c2a3b4c5d6e"
api/routes/profiles.py:25:    github_username: str = Form(default=None),
api/routes/profiles.py:26:    portfolio_url: str = Form(default=None),
api/routes/profiles.py:27:    resume_file: UploadFile = File(default=None),
api/schemas/review.py:15:    profile_id: UUID
~~~~

## Eval iterations

**Run history**

1. First full run failed because the sandboxed shell could not access the Claude CLI login state: all packages returned `claude exited 1`.
2. Final saved run, run outside the sandbox with the authenticated Claude CLI: `agreement: 20/20 scored items  (bar: 18/20: PASS)`.

**Package analysis**

`pkg-20` was a reject in both the gold label and my rubric's final run. The package had a bounded implementation plan, but the repo facts said Ghostty has a strict AI policy requiring all AI usage to be disclosed. The candidate plan comment did not include that disclosure, so my `comms` check rejected it for omitting a required repo-policy item.

**Check rationale**

Quoted check from `tools/plan-check/rubric.md`:

~~~~text
| comms | The candidate plan comment, read against thread highlights, repo facts, contribution policy, AI-use policy, and the plan itself. | Pass if the comment accurately summarizes the grounded plan, responds to explicit maintainer direction or repo policy, and includes any required disclosure. Fail if it ignores a maintainer's requested direction, promises a plan different from the draft, overpromises timing, or omits a required AI-use disclosure. | required |
~~~~

I made this required because the Unit 3 eval set includes thread and convention failures where a plan can be technically bounded but still not ready to post, such as ignoring maintainer direction or omitting a required AI-use disclosure.

**Trade-offs**

The `comms` check can reject a plan whose implementation approach is otherwise good. I accept that trade-off because posting a plan that violates explicit repo policy or maintainer direction is not ready for upstream collaboration.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
