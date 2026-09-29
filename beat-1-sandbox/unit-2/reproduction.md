# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

---

## Your identity upstream

**GitHub username**

MalikSCole

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/37#issuecomment-5896813926

~~~~text
Hi, I am going to investigate this issue.
I will compare docs/API.md against the backend definitions for POST /profiles and POST /reviews, especially the POST /profiles multipart form-data fields called out in the issue. I will report back with the exact files/fields I checked and whether the API docs are missing request-body details as described.
~~~~

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/37#issuecomment-5897594343

~~~~text
I reproduced this by comparing the checked-in API reference against the backend route and schema definitions.

Environment:
- Repository: `codepath/pathreview-ai301-fa26-s3`
- Commit checked: `2f4e82f52efbcfcc57d65b3fa5348672163ca088`
- OS: macOS 26.6.2
- Python: 3.14.5

Steps:
1. Cloned the repository and checked out the exact commit used for this reproduction:

```bash
git clone https://github.com/codepath/pathreview-ai301-fa26-s3.git
cd pathreview-ai301-fa26-s3
git checkout 2f4e82f52efbcfcc57d65b3fa5348672163ca088

2. Opened docs/API.md and checked the entries for POST /profiles and POST /reviews.
3. Compared those entries with api/routes/profiles.py, api/routes/reviews.py, api/schemas/profile.py, and api/schemas/review.py.
4. Searched the docs and API code for the relevant request-body field names:
rg -n "POST /profiles|POST /reviews|multipart|github_username|portfolio_url|resume_file|profile_id|request body|request-body" docs api -S

Observed:
- docs/API.md only has one-line summaries for the two endpoints:
  - line 18: ``POST /profiles — Create a profile with resume and GitHub username.
  - line 24: ``POST /reviews — Request a new portfolio review for a profile.
- The POST /profiles backend route defines request inputs that are not documented in docs/API.md:
  - github_username: str = Form(default=None) in api/routes/profiles.py
  - portfolio_url: str = Form(default=None) in api/routes/profiles.py
  - resume_file: UploadFile = File(default=None) in api/routes/profiles.py
- api/schemas/profile.py confirms the profile fields include optional github_username and portfolio_url.
- The POST /reviews backend route accepts data: ReviewCreate, and api/schemas/review.py defines that request body as:
class ReviewCreate(BaseModel):    profile_id: UUID


Expected:
- docs/API.md should include the request body/schema details for POST /profiles and POST /reviews.
- For POST /profiles, the docs should make clear that the request is multipart form data with optional github_username, optional portfolio_url, and optional resume_file, rather than leaving readers to guess JSON.
- For POST /reviews, the docs should show the JSON body with profile_id.
Actual:
- docs/API.md currently lists the endpoints but does not document the request body/schema for either POST /profiles or POST /reviews.
- This matches the issue as described.
~~~~

## Eval iterations

**Run history**

1. Smoke run, 3 packages: `agreement: 3/3 scored items`
2. Full run before saving: `agreement: 20/20 scored items  (bar: 18/20: PASS)`
3. Final saved run in `eval-run.txt`: `agreement: 19/20 scored items  (bar: 18/20: PASS)`

**Package analysis**

`pkg-20` was a reject in both the gold label and my rubric's final run. The gold note says: "excellent repro on every proof check; ghostty's stated AI policy requires disclosing all AI usage and the comments do not disclose (course packages are treated as AI-assisted work); the one-item category the floor exists for". My rubric rejected it through the repo-policy check, which requires AI-use disclosure when the repo policy requires it. That let the package fail even though the reproduction evidence itself was strong.

**Check rationale**

Quoted check from `tools/repro-check/rubric.md`:

~~~~text
| repo-policy-followed | Repo facts for templates/contribution policy/AI-use policy plus both candidate comments, using the Comms section of `references/evidence-guide.md`. | The comments satisfy any repo-stated posting requirements that matter to this package, especially required AI-use disclosure. If the repo has no such policy, this check passes unless the comments violate a stated issue/comment template expectation in a way that blocks review. | required |
~~~~

I made this a required check because the eval set includes a disclosure category where the proof is otherwise good. A rubric that only grades environment, steps, and artifacts would accept that package, so the check has to read repo policy and both comments directly. I kept the pass condition conditional so repos without an AI-use policy are not penalized.

**Trade-offs**

The `environment-recorded` check is strict enough to reject packages with no meaningful environment record, but that creates some judgment variance on static documentation issues and browser-based issues. In my final saved run, `pkg-07` flipped from accept to reject with `failed: environment-recorded`, even though the previous full run accepted it. I accept that trade-off because the final score was still passing, the category floor held, and the stricter environment rule correctly rejected packages like `pkg-06`, where the missing Windows/minikube environment details made the reproduction impossible to place.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
