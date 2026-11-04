# Coverage HTTP search/read test plan

## Analysis

Issue #12343 invites one-resource API-test contributions. My claimed scope is GET /fhir/Coverage and GET /fhir/Coverage/:uuid only. At commit 33050754bd9248137f2eef0db00c4b2d4847c73c, routes exist at apis/routes/_rest_routes_fhir_r4_us_core_3_1_0.inc.php:312-332 and call FhirCoverageRestController::getAll/getOne. CoverageFhirWriteApiTest calls only POST/PUT; ApiTestClient scope declarations do not execute GETs. Thus the contribution gap is missing dedicated HTTP regression tests, not a diagnosed product defect. The Unit 6 full reproduction package accepted all six required checks.

Before evidence (real Docker/database/OAuth run):

```text
Coverage Fhir Write Api
  Post creates coverage
  Put updates coverage
  Post without beneficiary returns error
OK (3 tests, 55 assertions)
```

The source cross-check found only CoverageFhirWriteApiTest's /apis/default/fhir/Coverage constant and ApiTestClient's Coverage.read/write scope declarations. PHPUnit --list-tests printed only the three write methods, then exited 70 on the extension's missing shutdown event; that inventory is not claimed as a passing test. No measured line/branch coverage percentage is asserted. The full rerunnable report is ~/ai301-unit6-starter/repro-draft.md; this plan quotes the decisive evidence rather than relying on an unseen file.

## Proposed Solution

Add one file: tests/Tests/Api/CoverageFhirApiTest.php. Use real HTTP via ApiTestClient and synthetic fixtures, following CoverageFhirWriteApiTest's working setup/defensive cleanup and ConditionFhirApiTest's read/search matrix, with PatientFhirApiTest as a second reference. Use strict_types=1, native types and the current AGENTS.md standards rather than copying legacy untyped patterns.

Decided fixture strategy: in setUp, create an authenticated ApiTestClient using setAuthTokenOrFail, install patient fixtures and capture the patient's UUID, install an insurance company fixture, normalize that synthetic insurer to a free positive ID if the helper inserted ID 0, load coverage.json[0], substitute beneficiary and payor references, remove id, POST through the existing write route and assert 201 before capturing its returned UUID. For positive-ID normalization, query COALESCE(MAX(id), 0) + 1, assert that result is numeric, and update only the newly created insurer UUID where id = 0 before POSTing Coverage. This reflects the read path's nonempty-provider precondition without changing product code or FixtureManager. Use typed properties for the client, FixtureManager and captured UUIDs. POST is setup only; no new write-feature assertions or production changes are part of this PR. Existing write baseline already verifies that path.

Teardown handles partially initialized setup, removes Coverage before patient/insurer, and uses try/finally so OAuth client removal still runs if token revocation throws. Reuse current FixtureManager helpers; do not change fixture infrastructure. Run tests serially because existing cleanup uses shared synthetic prefixes. New helper methods in the test narrow decoded JSON with assertions, centralize canonical resource-reference checks and OAuth-denial assertions, and avoid unreviewed casts or suppression annotations.

Scope boundaries: exactly the two GET operations, on the default authorized user path plus unauthenticated denial. No patient-compartment isolation matrix, extra search-parameter matrix, product/controller/service fixes, schema changes, other resources, inventory refresh, or broad refactor. If a product defect blocks a planned case, capture it and record a plan deviation before deciding how to proceed; do not silently change production code or weaken assertions to hide it.

## Implementation Plan

1. After plan-check accepts, create CoverageFhirApiTest.php with the project header, strict types, namespace, typed properties, fixture/auth setup and defensive teardown described above. No other code file is planned.
2. Add eight tests: patient-filtered search, _id-filtered search, read-one, empty search, malformed read UUID, absent read UUID, unauthenticated search and unauthenticated read.
3. Success assertions: HTTP 200, Bundle/collection shape for search, membership of the captured Coverage UUID, exact resourceType/id, beneficiary.reference == Patient/<captured patient UUID>, payor[0].reference == Organization/<captured insurer UUID>, and fixture subscriberId. _id search must return exactly one matching entry. Do not depend on arbitrary DB row order.
4. Empty search uses a valid absent UUID: expect HTTP 200 with Bundle/collection, total 0, no entries. Malformed read expects 400 with validationErrors. Valid absent read expects 404 and empty JSON array. These error contracts are grounded in the route annotations, shared RestControllerHelper and Condition/Patient tests; verify Coverage-specific behavior during the first focused run and record any difference rather than claiming it is already observed.
5. Unauthenticated clients deliberately skip token setup. Both GETs must return 401 with an OAuth error/message denial body (not a FHIR resource, 404 route miss or 500).
6. Run the new class alone first, then both Coverage classes to prove existing writes remain green and cleanup permits serial reuse. Inspect the before/after source inventory: the new GET/getOne calls must now be present and discovered, with no skipped/zero-test success.
7. Run every must-pass ship-manifest command, record exact outputs, and investigate any failure. An unchanged-code baseline failure is documented separately only after matching evidence; changed-test failures are fixed.
8. Review the single-file diff and local-file exclusions. Use Conventional Commit title and accurate Generated-By/Assisted-By trailers for actual tools. Draft the upstream template, use Refs #12343 to avoid closing the umbrella, and explain that relationship choice in course notes. Commit only the test file, run ship-gate on the committed branch and exact PR text, then push/open the upstream PR after PASS.

## Test Plan

- Decisive before/after: previously only 3 Coverage write tests/55 assertions; afterward a discovered, passing CoverageFhirApiTest with eight GET cases plus green write regression tests and visible GET call sites. The change adds coverage, not a product behavior change.
- Focused new class: openemr-cmd e 'cd /var/www/localhost/htdocs/openemr && vendor/bin/phpunit --testsuite api --filter CoverageFhirApiTest --testdox'. Require all new cases discovered and passing without skips.
- Existing-plus-new Coverage cases, style, full static analysis and API regression commands are sourced and recorded in ship-manifest.md. Full PHPStan uses full-codebase context, as AGENTS.md requires.
- Controls include nonempty seeded search/read versus absent-id search/read, malformed versus valid absent UUID, and authenticated versus unauthenticated requests. Assert response bodies so success or denial cannot be confused with routing/server failures.
- test_evidence.md will contain before artifacts, new test output, combined regression output, and every repository check result. Full matrix/runtime combinations not executed are stated honestly. Existing baseline outputs and hook logs remain recorded.

## Risks and Unknowns

PHP/FHIR are new to the contributor; all code must be understood and reviewed. The existing cleanup helpers use shared synthetic prefixes, so avoid parallel fixture runs and infrastructure scope creep. The initial Coverage error-shape hypotheses are now confirmed by the focused run: all 8 cases pass with 234 assertions, including the planned 400/404/401 bodies. The static-analysis baseline passed. The untouched full API baseline reported 1 OAuth failure, 1 warning and 4 skips, now documented in the manifest with dated evidence. QueryUtils is the DB helper for the fixture-ID normalization. This is one named slice of a shared issue; other resources' PRs do not complete or block this slice.

## Deviations

2026-11-03 — Verification adjustment: the untouched full API suite reports one OAuth client-grant failure, one warning and four skips, but openemr-cmd api-test returns exit 0. Keep this documented as a pre-existing failure in the manifest, and run the equivalent underlying PHPUnit full suite via openemr-cmd e after implementation to retain its exit status. The test scope and implementation approach are unchanged. This limitation and command adjustment will be stated in the PR and story.

2026-11-03 — Fixture deviation, recorded before correction: first focused run had 3 success-case failures while 5 error/auth cases passed. A diagnostic executed through the normal PHPUnit safety extension showed the POST-created insurance_data row linked to insurer_id/provider 0, search returned empty Bundles, and read returned 404. FhirCoverageService::searchForOpenEMRRecords filters empty provider values, including 0. The helper's default zero insurer ID is unsuitable for a readable seed. Add only test-local positive-ID normalization before POST, preserving existing fixture helper and product behavior. This fixture adjustment will be disclosed in the PR. A standalone diagnostic was refused by the safety bootstrap and was not bypassed; the successful diagnostic used the normal runner.
