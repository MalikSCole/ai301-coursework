# Contribution: FHIR Coverage HTTP search/read API tests

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Malik Cole
**GitHub Username:** MalikSCole
**Issue:** https://github.com/openemr/openemr/issues/12343
**Claimed slice:** `GET /fhir/Coverage` and `GET /fhir/Coverage/:uuid` only.
**Pull Request:** https://github.com/openemr/openemr/pull/15022

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Installed issue-scout and tested a two-language search**

2026-11-03: I installed the Unit 5 scout using my preserved Unit 1 rubric, evidence guide, and fit profile. My TypeScript and Python good-first-issue queries produced 200 unique results; filtering out assigned issues left 195, and the scout graded the top five by fewest comments, then latest update. All five passed the original rubric, but one (cvs-health/flag-controller#25) already had its requested change delivered by merged PR #26, exposing an availability-check gap; the search also surfaced environment-heavy work and a Rust lockfile task despite my frontend/backend profile. I saved the full readout and review notes locally and identified a rubric correction: completed work must make an issue unavailable even if GitHub still shows it as open.

**Unit 6: Guarded the claim and prepared OpenEMR memory and reproduction evidence**

2026-11-03: I installed the voice guard, canonical claims/questions/pings rules, real-repository scopes, and the scope-feasible rubric patch; the wiring block and actual claim passes are logged. After Ark #2871's component attempt could not reproduce the settled-empty issue, I investigated alternatives and claimed only OpenEMR #12343's two Coverage GET endpoints after the scout accepted the slice as moderate. I created my fork, configured origin/upstream, used the project's managed Docker worktree and hooks, and filled an ignored CLAUDE.local.md under 60 lines from scoped orientation. Repro-check accepted all six checks for the coverage-gap report; I recorded the listing command's shutdown error honestly and corrected a stale Path Review-only step in plan-check's procedure before starting planning.

**Unit 7: Shipped the scoped Coverage GET tests through the manifest and gate**

2026-11-03: I installed ship-gate, verified both hook stops, and wrote a manifest with three sourced must-pass checks plus the dated unrelated full-API baseline failure. Plan-check accepted both the initial plan and its recorded fixture adjustment; the final single-file commit b0b0ca4 passed repository hooks, all active manifest checks, and all four pr-precheck criteria, and [PR #15022](https://github.com/openemr/openemr/pull/15022) is open upstream. The main obstacles were the installer's .git-directory assumption, an insurer fixture with ID 0, and a helper returning 0 despite suite failures; I resolved local excludes through Git, normalized only the test insurer, and preserved the real full-suite outcomes without production changes. The manifest kept targeted tests/style/full static analysis decisive while making the existing OAuth failure visible; I used Refs #12343 following prior PRs so the umbrella remains open, and the hook reran fresh because its issue inference does not recognize Refs for the manual-pass cache.

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

I first used a broad TypeScript/Python scout scan and compared Ark #2871 and clearlydefined/service#830. The scope-feasible patch kept #830's unresolved API design as an ambitious difficulty note; Ark initially looked straightforward, but scoped component evidence showed its settled-empty outcome already implemented, and the updated scout rejected it. I posted the [Ark findings and clarification](https://github.com/mckinsey/agents-at-scale-ark/issues/2871#issuecomment-6614854554), then investigated alternatives including OpenChoreo #4592, whose Go/generated-code and integration-test scope was larger than its label suggested. I chose OpenEMR #12343 specifically for **GET /fhir/Coverage and GET /fhir/Coverage/:uuid**, not its entire tracking checklist. The scout accepted this exact slice as **moderate**, while rejecting the whole umbrella separately; the issue expressly permits one resource/method at a time and maintainers have accepted that approach. Although PHP/FHIR are new to me, this is bounded API testing with existing patterns, which builds on my backend/API/testing experience. I want to learn real OAuth-backed HTTP tests, deterministic fixtures, and careful cleanup in an unfamiliar project.

The scout helped compare scope, availability, and policy, but I learned not to trust labels, stale checklists, or shallow source checks. Its first broad scan accepted an issue already fixed by a merged PR, so I tightened completed-work availability; the Ark attempt also showed why parent rendering matters. For OpenEMR I checked the full thread, current source and PR overlap for the named slice, rather than treating other contributors' unrelated resources as taking the entire issue. I verified that the existing Coverage tests only exercise POST/PUT, got the Docker/OAuth/database baseline running (3 tests, 55 assertions), and saved the accepted claim-plus-reproduction package. My [Coverage GET claim](https://github.com/openemr/openemr/issues/12343#issuecomment-6615689727) posted on 2026-11-03 after claim-only repro-check accepted it and the voice guard logged a pass. The AI301 selection-site change from the earlier candidate has not been independently verified.

**Toolkit**

- Tool: my issue-scout, written search strategy and fit profile, scope-feasible/difficulty patch, and direct per-slice grading.
- What it produced: a saved five-issue scan, before/after finalist grades, a corrected Ark rejection, and an accepted OpenEMR Coverage GET slice rated moderate.
- Difficulties: language metadata and fewest-comment ranking surfaced mismatched/environment-heavy tasks; merged work slipped through availability; parent versus shared-issue slice required explicit distinction.
- What changed: tightened completed-work checks, aligned stale scope guidance, traced code rather than trusting labels/checklists, and graded the exact two-endpoint item separately from the umbrella. Earlier outputs and dated notes remain saved instead of being rewritten as if they were always correct.

---

## Understanding the Issue

**Problem Description**

OpenEMR's HTTP API test suite leaves resources/methods untested. For my selected slice, both Coverage GET routes exist, but source review and test inventory show no dedicated Coverage HTTP search/read cases. This is missing regression coverage, not a claim that the endpoints are broken.

**Expected Behavior**

ApiTestClient tests should exercise `GET /apis/default/fhir/Coverage` and `GET /apis/default/fhir/Coverage/<uuid>` through real OAuth and HTTP, asserting useful success/error responses against synthetic fixtures. New work stays within those two read routes.

**Current Behavior**

At commit `33050754bd9248137f2eef0db00c4b2d4847c73c` (8.6.0-dev), CoverageFhirWriteApiTest contains POST creation, PUT update, and invalid-POST cases. All three pass locally (55 assertions), but none calls GET/getOne. ApiTestClient already declares Coverage read scopes; scope declarations alone do not execute read tests. I have not measured line/branch coverage or demonstrated a product defect.

**Affected Components**

`tests/Tests/Api/CoverageFhirWriteApiTest.php`, `PatientFhirApiTest.php`, `ConditionFhirApiTest.php`, `ApiTestClient.php`, and `tests/Tests/Fixtures/FixtureManager.php` provide the patterns. The GET routes in `apis/routes/_rest_routes_fhir_r4_us_core_3_1_0.inc.php:312-332` call `FhirCoverageRestController` and `FhirCoverageService`; the write routes use a separate generic controller, explaining why passing writes do not test GET response construction.

**Toolkit**

- Tool: scoped orientation and source/test-discovery inspection.
- What it produced: a comparison of Coverage write fixtures/auth, Patient read patterns, and Condition's recent search/read/error matrix.
- Difficulties: the issue checklist is stale, and existing templates contain legacy patterns that must not override current AGENTS.md standards.
- What changed: used actual source and runtime baseline evidence, distinguished the GET controller path from writes, and recorded future status/body expectations as planning hypotheses.

---

## Reproduction Process

**Environment Setup**

2026-11-03: macOS 26.6.2 arm64, Docker Desktop engine 29.4.3, OpenEMR 8.6.0-dev at `33050754bd9248137f2eef0db00c4b2d4847c73c`, PHP 8.5.12, PHPUnit 11.5.57, and MariaDB 12.3.3. My [fork](https://github.com/MalikSCole/openemr) is origin; openemr/openemr is upstream. I created `test/fhir-coverage-read` using `openemr-cmd worktree add ... -b --start`, which manages the sibling worktree and isolated easy Docker stack (offset 1; http://localhost:8301). The database and OAuth readiness checks pass. Container-backed Git hooks are installed; CLAUDE.local.md is ignored through the shared `.git/info/exclude`. The complete public, pinned setup instructions and image digests are embedded below.

Docker was initially stopped and the clone sparse; I started Docker Desktop, fetched the full checkout, installed the official helper, and let first-start setup finish. The helper requires `prek-install` on the host, so I corrected the rejected worktree-exec form. No real patient data is used. The full API/CI matrix has not been run.

**Steps to Reproduce**

1. Clone the public fork, install the pinned official openemr-cmd helper, and create the managed worktree pinned to the source SHA, as detailed below. Wait for application/database/OAuth readiness.
2. From the primary clone, run the existing Coverage HTTP baseline:

   ```bash
   openemr-cmd worktree exec test/fhir-coverage-read e 'cd /var/www/localhost/htdocs/openemr && vendor/bin/phpunit --testsuite api --filter CoverageFhirWriteApiTest --testdox'
   ```

3. List CoverageFhir tests, then inspect the suite's resource references and HTTP calls:

   ```bash
   openemr-cmd worktree exec test/fhir-coverage-read e 'cd /var/www/localhost/htdocs/openemr && vendor/bin/phpunit --testsuite api --filter CoverageFhir --list-tests'
   ```

   From the feature worktree:

   ```bash
   rg -n '(/fhir/Coverage|CoverageFhir|Coverage\.read|Coverage\.write)' tests/Tests/Api
   rg -n 'public function test|testClient->(get|getOne|post|put)' tests/Tests/Api/CoverageFhirWriteApiTest.php
   ```

4. Compare CoverageFhirWriteApiTest, PatientFhirApiTest and ConditionFhirApiTest. Confirm both target GET routes exist, distinguish their controller path from writes, and identify the missing dedicated read/search cases without treating the stale issue checklist as proof.

**Reproduction Evidence**

- **Commit showing reproduction:** [tested source in my fork](https://github.com/MalikSCole/openemr/commit/33050754bd9248137f2eef0db00c4b2d4847c73c). No product/test implementation commit has been made in Unit 6; this coursework story records the commands and observed artifacts.
- **Screenshots/logs:** baseline exit 0, **3 tests / 55 assertions**. Test listing printed only the three write methods but exited **70** on the project's PHPUnit shutdown-event check; that listing is not counted as a passing test run. Source inspection independently shows write-only HTTP calls. Full output is embedded below; no browser screenshot is claimed.
- **My findings:** the two Coverage GET routes have a dedicated HTTP test gap at the pinned commit. This is not a reproduced endpoint malfunction, not a line/branch coverage measurement, and not proof about later commits or every runtime combination. No new test or application code has been written.
- **Checker result:** full-package repro-check **accept**, all six required checks pass. Its optional upstream-posting polish notes do not change the grade; this report is retained as coursework evidence and has not been posted as another issue comment.

<details>
<summary>Complete passing reproduction package, commands, and observed output</summary>


Date: 2026-11-03
Issue: https://github.com/openemr/openemr/issues/12343
Claim: https://github.com/openemr/openemr/issues/12343#issuecomment-6615689727
Scope: **GET /fhir/Coverage** and **GET /fhir/Coverage/:uuid** only.

**Outcome**

Confirmed a source/test-inventory gap for these two GET routes at commit `33050754bd9248137f2eef0db00c4b2d4847c73c`. The existing Coverage HTTP tests exercise writes (POST creation, PUT update, and invalid POST), and all three pass in the local Docker/OAuth/database environment. Source inspection and the per-resource test inventory show no dedicated Coverage search/read tests. This is a missing-test contribution, not a reproduced product failure. I have not yet written new tests, asserted that either GET endpoint is broken, or measured line/branch coverage. The stale issue checklist alone is not evidence of the gap.

**Environment**

- macOS 26.6.2 (25G83), arm64; Docker Desktop engine 29.4.3 (aarch64).
- OpenEMR 8.6.0-dev (`version.php`), commit `33050754bd9248137f2eef0db00c4b2d4847c73c`. This pins the version rather than assuming later master is identical.
- Fork: https://github.com/MalikSCole/openemr; upstream: https://github.com/openemr/openemr.
- Existing full clone: `/Users/admin/ai301-coursework/openemr`; origin points to my fork, upstream to the canonical repository.
- Managed feature worktree: `/Users/admin/ai301-coursework/openemr-wt-test-fhir-coverage-read`; branch `test/fhir-coverage-read`; no product/test edits.
- Official openemr-cmd 1.0.52; easy Docker environment, project `openemr-test-fhir-coverage-read`, offset 1. OpenEMR at http://localhost:8301 and https://localhost:9301. In-container PHP 8.5.12, PHPUnit 11.5.57, MariaDB 12.3.3.
- Pinned app image: `openemr/openemr:flex@sha256:cf6f04e1194e3aa07f4af1a07d4472084729766a2bd41e4b625e3c96fa321e60`; database: `mariadb:12.3.3@sha256:d46e102fa8b9b72bfcdeb56f9dd538742092119dc8b11f31fe662605cd234cd9`. Other image pins come from the checked-in easy compose file at the tested source commit.
- Readiness returned HTTP 200 with installed/database/filesystem/session/oauth_keys/cache all true. The environment was created locally with synthetic fixtures; no private data or external application account is required for these tests.
- The issue targets default-branch coverage, with no reporter OS/runtime. My attempt uses the documented Docker setup and one pinned default-branch commit. I have not run every supported PHP/database combination, full API suite, browser suite, or CI matrix.

**Rerunnable setup**

Prerequisites: Git, running Docker Desktop/Compose, Bash, jq, realpath, curl, and sufficient disk space. Install the official helper (the exact source revision used here is `2b0adb9a2dc77c73ddedc4cc9d25c179459a567a`):

```bash
mkdir -p "$HOME/.local/bin"
curl --fail --location https://raw.githubusercontent.com/openemr/openemr-devops/2b0adb9a2dc77c73ddedc4cc9d25c179459a567a/utilities/openemr-cmd/openemr-cmd -o "$HOME/.local/bin/openemr-cmd"
chmod +x "$HOME/.local/bin/openemr-cmd"
export PATH="$HOME/.local/bin:$PATH"
git clone https://github.com/MalikSCole/openemr.git
cd openemr
git remote add upstream https://github.com/openemr/openemr.git
openemr-cmd worktree add test/fhir-coverage-read -b --base 33050754bd9248137f2eef0db00c4b2d4847c73c --start
```

That creates the sibling worktree and per-worktree Docker environment through the project-supported helper. A fresh clone has no feature branch yet; for the already-created local worktree I used `openemr-cmd worktree add test/fhir-coverage-read -b --start` and verified HEAD equals the SHA above. On a machine with other managed worktrees, the allocated ports may differ; use the URLs printed by the helper rather than assuming offset 1.

Wait for first-start installation and healthy services. Check with `openemr-cmd worktree list`; the readiness endpoint is `/meta/health/readyz` on the printed HTTP URL. My observed readiness response was:

```json
{"status":"ready","checks":{"installed":true,"database":true,"filesystem":true,"session":true,"oauth_keys":true,"cache":true}}
```

Install validation hooks from the host clone/worktree using `openemr-cmd prek-install` (not through worktree exec); this succeeded and installed the shared pre-commit and commit-msg hooks. The stack must run for future hook checks.

**Commands and observed artifacts**

From the primary clone, run the existing Coverage baseline through the managed container:

```bash
openemr-cmd worktree exec test/fhir-coverage-read e 'cd /var/www/localhost/htdocs/openemr && vendor/bin/phpunit --testsuite api --filter CoverageFhirWriteApiTest --testdox'
```

Observed exit 0, 3 tests and 55 assertions:

```text
PHPUnit 11.5.57 by Sebastian Bergmann and contributors.

Runtime:       PHP 8.5.12
Configuration: /var/www/localhost/htdocs/openemr/phpunit.xml

...                                                                 3 / 3 (100%)

Time: 00:02.968, Memory: 59.00 MB

Coverage Fhir Write Api (OpenEMR\Tests\Api\CoverageFhirWriteApi)
 ✔ Post creates coverage
 ✔ Put updates coverage
 ✔ Post without beneficiary returns error

OK (3 tests, 55 assertions)
```

Then inspect the current per-resource inventory without adding tests:

```bash
openemr-cmd worktree exec test/fhir-coverage-read e 'cd /var/www/localhost/htdocs/openemr && vendor/bin/phpunit --testsuite api --filter CoverageFhir --list-tests'
```

Observed output:

```text
PHPUnit 11.5.57 by Sebastian Bergmann and contributors.

Available tests:
 - OpenEMR\Tests\Api\CoverageFhirWriteApiTest::testPostCreatesCoverage
 - OpenEMR\Tests\Api\CoverageFhirWriteApiTest::testPutUpdatesCoverage
 - OpenEMR\Tests\Api\CoverageFhirWriteApiTest::testPostWithoutBeneficiaryReturnsError
CRITICAL ERROR: Exiting without having received PHPUnit shutdown event
```

**Limitation:** listing emitted the three write-test methods, then exited **70** because the project's PHPUnit extension did not receive a shutdown event in listing mode. This is not a successful test run and is not used as proof that tests pass. The actual execution above independently exited 0. A test-name filter alone also cannot prove absence of dynamically named coverage, so I cross-checked source below.

From the feature worktree, search the API suite and inspect the matching file's HTTP calls:

```bash
rg -n '(/fhir/Coverage|CoverageFhir|Coverage\.read|Coverage\.write)' tests/Tests/Api
rg -n 'public function test|testClient->(get|getOne|post|put)' tests/Tests/Api/CoverageFhirWriteApiTest.php
```

The first command produced only the write class/resource constant and client scope declarations:

```text
tests/Tests/Api/CoverageFhirWriteApiTest.php:6: * Drives real HTTP POST/PUT through OAuth against /apis/default/fhir/Coverage
tests/Tests/Api/CoverageFhirWriteApiTest.php:29:class CoverageFhirWriteApiTest extends TestCase
tests/Tests/Api/CoverageFhirWriteApiTest.php:31:    private const RESOURCE_URL = '/apis/default/fhir/Coverage';
tests/Tests/Api/ApiTestClient.php:78:        'patient/Coverage.read',
tests/Tests/Api/ApiTestClient.php:105:        'user/Coverage.read',
tests/Tests/Api/ApiTestClient.php:106:        'user/Coverage.write',
tests/Tests/Api/ApiTestClient.php:210:        'patient/Coverage.read',
```

The second command produced:

```text
106:    public function testPostCreatesCoverage(): void
108:        $response = $this->testClient->post(self::RESOURCE_URL, $this->fhirFixture);
121:    public function testPutUpdatesCoverage(): void
123:        $createResponse = $this->testClient->post(self::RESOURCE_URL, $this->fhirFixture);
138:        $putResponse = $this->testClient->put(self::RESOURCE_URL, $id, $updated);
157:    public function testPostWithoutBeneficiaryReturnsError(): void
161:        $response = $this->testClient->post(self::RESOURCE_URL, $invalid);
```

Reading CoverageFhirWriteApiTest confirms its three test methods call post/put; none calls get/getOne. Client scope declarations authorize access but do not execute endpoint tests. I also inspected the existing API test files for Coverage references rather than relying on class names or the issue's old checkboxes.

**Route and pattern comparison**

The route table `apis/routes/_rest_routes_fhir_r4_us_core_3_1_0.inc.php:312-332` defines both GET routes. Their full HTTP paths are `/apis/default/fhir/Coverage` and `/apis/default/fhir/Coverage/<uuid>`. They call FhirCoverageRestController::getAll/getOne, then FhirCoverageService. The patient-context branch binds a patient UUID; the user-context branch checks admin/super ACL. Write routes go through FhirGenericRestController, so passing POST/PUT tests does not exercise the GET controller's Bundle/read response path.

| Existing file | Setup and behavior inspected | What it contributes to planning |
|---|---|---|
| CoverageFhirWriteApiTest.php | Real OAuth via setAuthTokenOrFail; patient and insurer fixtures; coverage.json; HTTP POST/PUT; defensive teardown | Reuse Coverage-specific fixture/authentication setup; its successful run establishes the baseline environment. |
| PatientFhirApiTest.php | HTTP _id search/read tests and malformed/unknown UUID cases, with patient data seeded through existing helpers | Reference for HTTP calls and assertions, while checking modern typing/cleanup standards instead of copying legacy code blindly. |
| ConditionFhirApiTest.php | Recent read/search class: patient/_id search, Bundle contents, read one, empty/invalid/unknown/unauthenticated cases | Reference matrix for the two claimed GET endpoints; expected Coverage status/body details still need runtime verification during Unit 7. |

FixtureManager already provides patient, insurer, Coverage JSON and cleanup support. Coverage read fields include beneficiary `Patient/<uuid>` and payor `Organization/<uuid>`; these are source-derived candidate assertions, not results from new GET tests. Setup/cleanup uses synthetic fixture rows; review isolation because some existing removers match shared fixture prefixes.

**Expected versus actual**

Expected contribution outcome: focused HTTP-level tests for the two Coverage read/search routes using ApiTestClient, real OAuth, deterministic synthetic fixtures, meaningful response/status assertions, and reliable cleanup.

Actual at the pinned commit: existing Coverage write cases pass, but source/test inventory has no dedicated search/read cases for these two GET routes. The difference is test coverage, not a claimed HTTP failure. This establishes the bounded missing-coverage task without changing product behavior or implementing the tests ahead of Unit 7 planning.

**Scope, policy, and next stage**

The issue explicitly permits incremental per-resource work. The scout accepted this precise slice as moderate and rejected the entire tracking issue separately. Other resources' claims do not claim Coverage; the posted claim names only these two endpoints. Current source and claim/PR review, not the stale issue inventory, informed the selection.

I read CONTRIBUTING.md, AGENTS.md and CLAUDE.md. Conventional Commit titles/messages, strict typing and existing quality hooks apply. AI-created/modified code needs the proper Generated-By/Assisted-By trailer with the actual tool's name. I used AI assistance to investigate and organize this report; commands/artifacts are from the local attempt and were reviewed. No contribution code has been committed. Any later product defect should be documented separately instead of widening this test-only scope.

Next is Unit 7 planning: decide new test class versus extension, fixture seeding strategy and cleanup, exact read/search/error matrix, and test commands before implementation. No new application or test code has been written. This report is for grading/course evidence; it has not been posted upstream.

</details>

**Toolkit**

- Tool: repro-check full-package live mode, managed Docker/OAuth/database baseline, PHPUnit inventory and scoped source comparison.
- What it produced: a passing claim/reproduction package with pinned setup, exact endpoints, successful existing tests, source evidence and explicit limits.
- Difficulties: discovery mode exits 70 after printing tests; a name-filter inventory alone cannot prove all coverage gaps; source patterns and runtime claims must stay distinct.
- What changed: disclosed the listing failure, cross-checked source and route/controller paths, embedded actual outputs, and deferred implementation until Unit 7 planning.

---

## Solution Approach

**Analysis**

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

**Proposed Solution**

Add one file: tests/Tests/Api/CoverageFhirApiTest.php. Use real HTTP via ApiTestClient and synthetic fixtures, following CoverageFhirWriteApiTest's working setup/defensive cleanup and ConditionFhirApiTest's read/search matrix, with PatientFhirApiTest as a second reference. Use strict_types=1, native types and the current AGENTS.md standards rather than copying legacy untyped patterns.

Decided fixture strategy: in setUp, create an authenticated ApiTestClient using setAuthTokenOrFail, install patient fixtures and capture the patient's UUID, install an insurance company fixture, normalize that synthetic insurer to a free positive ID if the helper inserted ID 0, load coverage.json[0], substitute beneficiary and payor references, remove id, POST through the existing write route and assert 201 before capturing its returned UUID. For positive-ID normalization, query COALESCE(MAX(id), 0) + 1, assert that result is numeric, and update only the newly created insurer UUID where id = 0 before POSTing Coverage. This reflects the read path's nonempty-provider precondition without changing product code or FixtureManager. Use typed properties for the client, FixtureManager and captured UUIDs. POST is setup only; no new write-feature assertions or production changes are part of this PR. Existing write baseline already verifies that path.

Teardown handles partially initialized setup, removes Coverage before patient/insurer, and uses try/finally so OAuth client removal still runs if token revocation throws. Reuse current FixtureManager helpers; do not change fixture infrastructure. Run tests serially because existing cleanup uses shared synthetic prefixes. New helper methods in the test narrow decoded JSON with assertions, centralize canonical resource-reference checks and OAuth-denial assertions, and avoid unreviewed casts or suppression annotations.

Scope boundaries: exactly the two GET operations, on the default authorized user path plus unauthenticated denial. No patient-compartment isolation matrix, extra search-parameter matrix, product/controller/service fixes, schema changes, other resources, inventory refresh, or broad refactor. If a product defect blocks a planned case, capture it and record a plan deviation before deciding how to proceed; do not silently change production code or weaken assertions to hide it.

**Implementation Plan**

1. After plan-check accepts, create CoverageFhirApiTest.php with the project header, strict types, namespace, typed properties, fixture/auth setup and defensive teardown described above. No other code file is planned.
2. Add eight tests: patient-filtered search, _id-filtered search, read-one, empty search, malformed read UUID, absent read UUID, unauthenticated search and unauthenticated read.
3. Success assertions: HTTP 200, Bundle/collection shape for search, membership of the captured Coverage UUID, exact resourceType/id, beneficiary.reference == Patient/<captured patient UUID>, payor[0].reference == Organization/<captured insurer UUID>, and fixture subscriberId. _id search must return exactly one matching entry. Do not depend on arbitrary DB row order.
4. Empty search uses a valid absent UUID: expect HTTP 200 with Bundle/collection, total 0, no entries. Malformed read expects 400 with validationErrors. Valid absent read expects 404 and empty JSON array. These error contracts are grounded in the route annotations, shared RestControllerHelper and Condition/Patient tests; verify Coverage-specific behavior during the first focused run and record any difference rather than claiming it is already observed.
5. Unauthenticated clients deliberately skip token setup. Both GETs must return 401 with an OAuth error/message denial body (not a FHIR resource, 404 route miss or 500).
6. Run the new class alone first, then both Coverage classes to prove existing writes remain green and cleanup permits serial reuse. Inspect the before/after source inventory: the new GET/getOne calls must now be present and discovered, with no skipped/zero-test success.
7. Run every must-pass ship-manifest command, record exact outputs, and investigate any failure. An unchanged-code baseline failure is documented separately only after matching evidence; changed-test failures are fixed.
8. Review the single-file diff and local-file exclusions. Use Conventional Commit title and accurate Generated-By/Assisted-By trailers for actual tools. Draft the upstream template, use Refs #12343 to avoid closing the umbrella, and explain that relationship choice in course notes. Commit only the test file, run ship-gate on the committed branch and exact PR text, then push/open the upstream PR after PASS.


**Recorded deviations (2026-11-03)**

- The helper seeded insurer ID 0; Coverage filters an empty provider, so initial success cases failed. A PHPUnit diagnostic confirmed provider 0 and empty/404 reads. The accepted revised plan assigns only that synthetic insurer a free positive ID in the new test, without changing FixtureManager or product code. After correction, all eight cases pass (234 assertions).
- The baseline API helper returned 0 while reporting one pre-existing OAuth failure, a refresh_token warning and four skips. The after-run used underlying PHPUnit for an honest exit code and reproduced the same failure/warning/skip signatures. The manifest preserves this dated exception; it does not claim the full suite green.

**Toolkit**

- Tool: plan-check, sourced ship manifest and scoped fixture diagnostics.
- What it produced: initial and revised plan-check accept results (all six checks), a private plan-comment draft, and an executable one-file plan.
- Difficulties: passing writes did not prove the zero-ID insurer was readable; the broad helper masked the test failure exit; the staff installer assumed .git was a directory.
- What changed: documented the positive-ID fixture adjustment and verification-command change, used the resolved common Git exclude path, and backed up/corrected stale sandbox/default-base instructions without changing rubric criteria. The PR draft discloses both deviations; plan-comment.md remains unposted.

---

## Testing Strategy

The new CoverageFhirApiTest drives real OAuth/HTTP against the two claimed GET routes using a deterministic synthetic Coverage, patient and insurer. It checks patient-filtered and _id search membership, exact read identity and canonical references, subscriber ID, empty search, malformed versus absent UUID, and authenticated versus unauthenticated behavior. These assertions distinguish meaningful API results from route misses, server errors or a body that merely exists; POST is used only to seed the read fixture.

Observed before: only the Coverage write class (3 tests, 55 assertions), with no dedicated GET call sites. Observed after: the new class passes **8 tests / 234 assertions**; a consecutive combined run passes **11 tests / 289 assertions**, including all pre-existing writes, exercising cleanup/reuse. Coverage PHP_CodeSniffer passes, and full-codebase PHPStan with staged final source passes; I confirmed the new file appears in the analysis cache rather than assuming an untracked file was checked.

Full API comparison: untouched base **729 tests / 9765 assertions**, after **737 tests / 10006 assertions**. Both report the same **1 failure, 1 warning, 4 skips**. The failure is ClientGrantTypeEnforcementTest.php:215 (client-credentials request 400 invalid_client vs expected 200); the warning is ApiTestClient.php:315, undefined refresh_token, triggered by 9 public-client/introspection cases. This is explicitly a pre-existing suite problem, not a green full suite, and it is retained with a dated reason in ship-manifest.md. The after-run used direct PHPUnit through the managed helper and exited 1; the baseline api-test helper returned 0 despite FAILURES. Full raw logs are retained locally; test_evidence.md contains before, after and command/result excerpts.

The environment is the pinned Docker/PHP 8.5.12/MariaDB 12.3.3 setup. Other PHP/database/CI combinations, patient-compartment isolation and exhaustive search-parameter matrices are not claimed tested. No production fix, shared fixture change or extra resource was bundled into the test contribution.

**Toolkit**

- Tool: PHPUnit/ApiTestClient, PHP_CodeSniffer, full PHPStan, ship-manifest baselines and before/after test_evidence.md.
- What it produced: passing new and combined Coverage runs, source-level GET coverage evidence, and an honest full-suite baseline comparison.
- Difficulties: initial success cases exposed a zero-ID seed; the suite helper masked exit failure; untracked-file cache inclusion needed explicit verification.
- What changed: corrected only the local fixture setup after re-grading the deviation, ran the underlying full-suite command, confirmed staged-file analysis, and preserved unrelated failures instead of claiming full green or expanding scope.

---

## Implementation Notes

**2026-11-03 — Unit 6 and planning**

Earlier Ark #2871 evidence remains in coursework history through f41ddfa; I posted its limited cannot-reproduce findings and selected the scoped OpenEMR Coverage GET task. The claim, fork/remotes, managed branch/stack, local memory and full repro-check package were completed before implementation. I installed ship-gate, verified both hooks stopped the help command, sourced and baselined the manifest, and pushed the accepted plan checkpoint as 25d0881.

**2026-11-03 — Implementation and observed deviation**

Added only tests/Tests/Api/CoverageFhirApiTest.php with the planned eight HTTP cases. The first run had three success-case failures while five error/auth cases passed. A temporary diagnostic through the normal PHPUnit safety path showed the insurer helper used ID 0, which the Coverage GET service filters as empty; I updated the plan and story and obtained another six-check accept before applying test-local positive-ID normalization. No controller/service/shared-helper fix was made, and temporary diagnostic files were removed. The final new and combined tests, style and definitive staged-file full PHPStan pass. The full API after-run matches the pre-existing OAuth failure/warning/skips. All applicable repository hooks passed; commit b0b0ca4 contains only the new test class with Generated-By: Codex and Assisted-By: Claude Code trailers. Manual ship-gate and the actual PR hook both passed, and PR #15022 is open against openemr/openemr master from my fork. The hook reran checks instead of honoring the manual stamp because Refs does not match its issue-reference inference; the manual run explicitly supplied the issue URL, and no gate was bypassed.

**Toolkit**

- Tool: plan-check, managed Docker tests, scoped diagnostics, local ship-gate and repository hooks.
- What it produced: a single-file implementation aligned with the accepted revised plan and reproducible before/after evidence.
- Difficulties: staff installer worktree path, zero-ID fixture, masked helper exit, and pre-existing unrelated suite failures.
- What changed: completed exclusions via Git's resolved path, recorded/re-graded deviations, used accurate test commands, and kept local working files outside the diff.

---

## Pull Request

**PR Link:** https://github.com/openemr/openemr/pull/15022

**PR Description:** `test(api): add FHIR Coverage read endpoint tests`. Adds one CoverageFhirApiTest with eight real-OAuth HTTP search/read/error/auth cases and defensive cleanup. The description discloses the test-local positive-insurer-ID adjustment, passing new/combined/style/static checks, unchanged full-suite OAuth failure/warning/skips, and AI involvement. It uses `Refs #12343` rather than a closing keyword, matching earlier single-resource PRs and leaving the umbrella inventory open; repository context takes precedence over the course's generic Fixes wording.

<details>
<summary>Submitted PR description</summary>

#### Short description of what this changes or resolves:

This adds HTTP regression tests for `GET /fhir/Coverage` and `GET /fhir/Coverage/:uuid` using the existing real-OAuth API test pattern. The current Coverage API tests already cover writes, so this PR adds search and read coverage without changing any production behavior.

Refs [[#12343](https://github.com/openemr/openemr/issues/12343)]. This only covers the Coverage read portion of that larger issue and leaves the rest of the inventory open, similar to earlier resource test PRs like [[#12808](https://github.com/openemr/openemr/pull/12808)].

#### Changes proposed in this pull request:

- Adds `tests/Tests/Api/CoverageFhirApiTest.php` with eight tests covering patient-filtered search, `_id` search, read by UUID, empty search, malformed and unknown UUID errors, and unauthenticated search/read.
- Checks the returned status codes and response data, including the seeded resource ID, beneficiary/payor references, subscriber ID, and OAuth denial responses.
- Reuses the existing patient, insurer, and Coverage fixtures, with HTTP POST used only for setup.
- Adds cleanup for the created fixtures and OAuth client.

While implementing the tests, I ran into an issue with the existing insurer fixture. In my environment, the helper creates an insurer with ID `0`, and the Coverage GET path filters records with an empty provider. Because of that, the POST setup succeeded but the first read returned `404` and searches came back empty.

To keep this PR limited to tests, the setup only assigns the synthetic insurer a free positive ID when its ID is `0` before creating the Coverage resource. I did not change the shared fixture helper, controllers, services, or route tables.

**Verification**

Environment: OpenEMR 8.6.0-dev at base `33050754`, Docker/PHP 8.5.12, PHPUnit 11.5.57, MariaDB 12.3.3.

- Before: existing Coverage write tests passed with `3 tests, 55 assertions`.
- New Coverage read tests pass with `8 tests, 234 assertions`.
- Both Coverage test classes pass together with `11 tests, 289 assertions`.
- Coverage PHP_CodeSniffer checks pass.
- Full-codebase PHPStan passes.
- Full API suite before: `729 tests, 9765 assertions`.
- Full API suite after: `737 tests, 10006 assertions`.

The full API suite reports the same existing failure, warning, and four skips before and after this change. The failure is in `ClientGrantTypeEnforcementTest.php:215`, where a client-credentials request returns `400 invalid_client` instead of `200`. The warning is in `ApiTestClient.php:315` for an undefined `refresh_token`.

The new Coverage tests pass during the full run, and I did not include any unrelated production fixes in this PR.

Commands used included:

`vendor/bin/phpunit --testsuite api --filter CoverageFhirApiTest --testdox`

`vendor/bin/phpunit --testsuite api --filter CoverageFhir`

`composer phpcs -- tests/Tests/Api/CoverageFhir*ApiTest.php`

and the full-codebase PHPStan check, all inside the documented development container.

One thing I noticed during verification is that the `api-test` helper returned exit code `0` even though the baseline reported failures, so I used the underlying PHPUnit command for the after-run to get the actual failing exit code. I am not claiming the full API suite is green.

#### Was an AI assistant used? Yes / No

Yes. I used Codex to help generate the test class and trace the fixture behavior, and Claude Code for plan and readiness review. I reviewed the changes, ran the commands locally, and verified the results myself. The commit trailers also record the AI assistance.

</details>

**Maintainer Feedback:**

- 2026-11-03: no human maintainer response or submitted review yet. The initial GitHub check snapshot showed only auto-merge skipped; a green remote CI matrix is not claimed. CONTRIBUTING.md says first-time contributors require maintainer approval before CI runs.
- Latest monitoring check: [CodeRabbit automated comment](https://github.com/openemr/openemr/pull/15022#issuecomment-6620296648) reports no actionable review comments, but flags docstring coverage (22.22% versus its 80% threshold) and redundant comments. These are bot warnings, not maintainer approval; they remain to assess during Unit 8. The PR is still OPEN and has no submitted reviews.

**Status:** Awaiting review. Verified OPEN, not draft, upstream base master; head MalikSCole:test/fhir-coverage-read; exactly tests/Tests/Api/CoverageFhirApiTest.php changed.

**Toolkit**

- Tool: ship-gate, sourced local manifest, pr-precheck, voice guard, repository hooks and GitHub CLI.
- What it produced: manual PASS and PR-hook PASS (all three active repo checks and four PR criteria), a clean one-file commit, and upstream PR #15022.
- Difficulties: staff install did not resolve worktree excludes; full suite had an unrelated baseline failure and a masked exit; Refs does not match the gate's closing-keyword issue inference, so it reran rather than using the manual pass cache.
- What changed: used the common Git exclude path, explicitly passed the issue URL to manual gate, kept Refs to protect the umbrella, recorded honest failures with matching before/after proof, and let both hooks run without bypass. Working drafts, manifest, memory and evidence stayed local.

---

## Learnings and Reflections

**Technical Skills Gained**

I learned to drive PHP API tests through real OAuth, seed/read synthetic FHIR Coverage resources, assert canonical Patient/Organization references, and distinguish a zero-ID fixture from a product behavior defect. I also learned to check exit status against reported test outcomes and verify that staged new files are included in static analysis.

**Challenges Overcome**

The documented tools assumed a regular clone in one install step and masked a suite failure in another. Git-resolved exclusions handled the worktree, and underlying PHPUnit preserved the true suite result. A scoped diagnostic and re-graded plan kept the insurer-ID correction test-local instead of widening into product code.

**What I'd Do Differently Next Time**

Establish a readable synthetic fixture, not only a successful write, before settling the test setup. Keep exact public issue URLs in local plans for tooling inference, while retaining non-closing references for umbrella work. Preserve baseline logs before implementation and record deviations before changing the plan.

---

## Resources Used

- [OpenEMR #12343](https://github.com/openemr/openemr/issues/12343): incremental-slice guidance, claims and existing test patterns.
- [OpenEMR contribution guide](https://github.com/openemr/openemr/blob/master/CONTRIBUTING.md): Docker workflow, Conventional Commits, AI trailers and hooks.
- [OpenEMR AGENTS.md](https://github.com/openemr/openemr/blob/master/AGENTS.md): managed worktrees, coding/test standards and feature-branch rules.
- [Coverage write API test](https://github.com/openemr/openemr/blob/master/tests/Tests/Api/CoverageFhirWriteApiTest.php), [Patient API test](https://github.com/openemr/openemr/blob/master/tests/Tests/Api/PatientFhirApiTest.php), and [Condition API test](https://github.com/openemr/openemr/blob/master/tests/Tests/Api/ConditionFhirApiTest.php): fixture/authentication and search/read patterns.
- [Official openemr-cmd](https://github.com/openemr/openemr-devops/tree/master/utilities/openemr-cmd): per-worktree stack and hook commands.
- [Unit 6 starter](https://github.com/codepath/ai301-unit6-starter): voice guard, wild scopes, scope-feasible and local memory template.
- [Earlier Ark follow-up](https://github.com/mckinsey/agents-at-scale-ark/issues/2871#issuecomment-6614854554): evidence that redirected issue selection.

- [Opened Coverage GET PR #15022](https://github.com/openemr/openemr/pull/15022): final submitted test-only contribution and disclosed verification.
