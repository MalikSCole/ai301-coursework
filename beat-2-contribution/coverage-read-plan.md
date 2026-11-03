# Initial Unit 7 plan: Coverage HTTP search/read tests

2026-11-03. Planning draft only; not yet graded by plan-check. No implementation authorized by this document alone.
Issue: https://github.com/openemr/openemr/issues/12343
Claim: https://github.com/openemr/openemr/issues/12343#issuecomment-6615689727
Scope: GET /fhir/Coverage and GET /fhir/Coverage/:uuid only.
Base: 33050754bd9248137f2eef0db00c4b2d4847c73c (OpenEMR 8.6.0-dev).
Branch: test/fhir-coverage-read; managed worktree openemr-wt-test-fhir-coverage-read.

## Evidence and diagnosis

Unit 6 full-package repro-check accepted all six checks. The existing Coverage write API baseline passed (3 tests, 55 assertions). Source inspection confirms POST/PUT-only tests and a distinct legacy controller path for the two GETs. This is a test gap, not a diagnosed product defect. The --list-tests inventory printed only the write cases but exited 70 at the PHPUnit extension's shutdown check; it is not counted as a test pass.

## Proposed scope and first edit

After plan review, create `tests/Tests/Api/CoverageFhirApiTest.php`. Use strict_types=1, native types, the current file header/license conventions, and current AGENTS.md standards. Do not alter application controllers, services, routes, schema, other resources or the stale issue inventory as part of this task. If a product bug prevents an intended case, capture its evidence and decide the next step separately.

Use `CoverageFhirWriteApiTest` for synthetic setup and defensive cleanup, `ConditionFhirApiTest` for search/read cases, and `PatientFhirApiTest` as a second reference. Do not duplicate legacy typing or fragile teardown just because a template contains it.

## Fixture and lifecycle decision

Proposed default: reuse the working Coverage write setup and seed a fresh Coverage via the existing HTTP POST route, capturing the returned UUID. Install synthetic patient and insurer fixtures, fill beneficiary/payor in coverage.json, then use that seeded UUID in GET assertions. The write baseline already validates that seeding path; setup POST is a prerequisite, not extra write-feature scope.

Use ApiTestClient::setAuthTokenOrFail so setup cannot silently continue without authentication. Record the seeded patient, insurer and Coverage UUIDs in typed properties. Teardown must handle partial setup, remove Coverage before patient/insurer, and clean up the OAuth client even if token revoke throws. Inspect the existing shared-prefix cleanup behavior; run these fixture tests serially and avoid a broad fixture-framework rewrite.

Planning checkpoint: verify that reuse is sufficient without adding a new fixture helper. If it is not, describe the minimal helper and isolation requirement before editing it.

## Proposed case matrix

| Case | HTTP trigger | Intended observable proof |
|---|---|---|
| Search by patient | GET Coverage?patient=<seeded patient UUID> | 200; Bundle includes the seeded Coverage; beneficiary equals Patient/<seeded UUID>. |
| Search by id | GET Coverage?_id=<seeded Coverage UUID> | 200; matching resource id and type; deterministic membership without depending on unrelated rows. |
| Read one | GET Coverage/<seeded Coverage UUID> | 200; Coverage resource identity and stable fixture-backed beneficiary/payor references. |
| Empty search | GET Coverage?_id=<well-formed absent UUID> | Successful empty Bundle; verify actual Bundle shape at this version before pinning it. |
| Unknown read | GET Coverage/<well-formed absent UUID> | Route documentation/pattern suggests 404; verify the Coverage-specific body rather than assuming OperationOutcome. |
| Malformed read | GET Coverage/not-a-uuid | Route documentation/pattern suggests 400; verify actual validation body before assertion. |
| Unauthenticated access | Both GET routes without bearer credentials | 401/denial response through HTTP middleware; confirm exact current contract. |

Expected status/body details in error rows are hypotheses from source and sibling tests, not observations from new GET probes. Confirm them during the planning checkpoint using the existing synthetic environment before implementing assertions. Do not silently change product behavior to make tests match assumptions.

Keep payor/status search matrices, new patient-token isolation infrastructure, and exhaustive FHIR conformance out of the first slice. The routes have separate patient-context binding; decide during plan-check whether a minimal existing-pattern patient-context case is necessary for this claim, rather than expanding that scope implicitly.

## Verification commands and outcomes

From the primary clone, use the managed worktree wrapper so commands hit its container:

```bash
openemr-cmd worktree exec test/fhir-coverage-read e 'cd /var/www/localhost/htdocs/openemr && vendor/bin/phpunit --testsuite api --filter CoverageFhirApiTest --testdox'
openemr-cmd worktree exec test/fhir-coverage-read e 'cd /var/www/localhost/htdocs/openemr && vendor/bin/phpunit --testsuite api --filter CoverageFhirWriteApiTest --testdox'
openemr-cmd worktree exec test/fhir-coverage-read api-test
```

These are planned checks: the new class does not exist yet. Require the new cases to be discovered (not zero tests or silently skipped), meaningful assertions to pass, write baseline to stay green, and no leaked fixtures/OAuth clients across repeated serial runs. If the full suite fails, distinguish a baseline failure from a changed-test regression with evidence.

Use installed hooks and documented code-quality checks before any future commit/PR. PHPStan is run with full-codebase context per AGENTS.md. Feature changes stay on this branch; Conventional Commit-style PR/commit messages and accurate Generated-By/Assisted-By trailers apply. Do not bypass hooks. No commit, push or PR is part of this planning draft.

## Next gate

Read this plan against the accepted Unit 6 claim/repro package with plan-check. Resolve fixture strategy, Coverage-specific error contracts and minimal patient-context depth before new test or product code is written. Unit 7 ship-gate installation/manifest work has not been completed or represented as completed here.
