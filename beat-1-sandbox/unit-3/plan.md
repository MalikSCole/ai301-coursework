# Plan for issue #37

## Diagnosis

The API reference is missing request-body details for the two endpoints named in issue #37. My Unit 2 reproduction compared `docs/API.md` with the backend route and schema definitions and found that the docs only contain one-line endpoint summaries:

> `docs/API.md` only has one-line summaries for the two endpoints: line 18: `POST /profiles` and line 24: `POST /reviews`.

The backend shows more specific request inputs that the docs do not explain. For `POST /profiles`, the route uses multipart form data:

> `github_username: str = Form(default=None)`, `portfolio_url: str = Form(default=None)`, and `resume_file: UploadFile = File(default=None)` in `api/routes/profiles.py`.

For `POST /reviews`, the route accepts a JSON body using `ReviewCreate`:

> `class ReviewCreate(BaseModel): profile_id: UUID`

So the fix is documentation-only: add request-body sections and examples for `POST /profiles` and `POST /reviews` in `docs/API.md`.

## Scope

In scope:
- Update `docs/API.md` so `POST /profiles` documents `multipart/form-data`, each accepted field, and an example request.
- Update `docs/API.md` so `POST /reviews` documents its JSON body, `profile_id`, and an example request.
- Keep the existing endpoint list and interactive-docs references intact.

Not in scope:
- Changing backend route behavior, schemas, validation, authentication, or tests.
- Adding docs for unrelated endpoints.

## Files you will change

- `docs/API.md`

## Approach

1. Expand the `POST /profiles` entry under Profiles into a short endpoint subsection.
2. Add a request body table for `github_username`, `portfolio_url`, and `resume_file`, noting that all three are optional and that `resume_file` accepts PDF, Markdown, or plain text based on the route validation.
3. Add a `curl` example that uses `multipart/form-data` with `-F` fields.
4. Expand the `POST /reviews` entry under Reviews into a short endpoint subsection.
5. Add a JSON request body table for `profile_id` and a JSON example.

## Test plan

Because this is a docs-only change, I will verify it by comparing the updated docs against the backend definitions:

```bash
rg -n "POST /profiles|POST /reviews|multipart/form-data|github_username|portfolio_url|resume_file|profile_id" docs/API.md api/routes/profiles.py api/routes/reviews.py api/schemas/review.py api/schemas/profile.py
```

Expected after the change:
- `docs/API.md` contains `multipart/form-data`, `github_username`, `portfolio_url`, and `resume_file` for `POST /profiles`.
- `docs/API.md` contains `profile_id` and a JSON example for `POST /reviews`.
- The backend route/schema references still show the same field names, so the docs match the implementation.

## Risks and unknowns

The main risk is documenting a field type incorrectly. I will avoid that by using the exact FastAPI route parameters and Pydantic schema as the source of truth. I am not changing generated OpenAPI output or backend code.

## Deviations

The implementation followed the plan as written. I did not need to change the scope, files, or test approach.
