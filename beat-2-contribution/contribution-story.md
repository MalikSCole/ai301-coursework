# Contribution: Disable or hide “Use via API” when no agents are present

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Malik Cole
**GitHub Username:** MalikSCole
**Issue:** https://github.com/mckinsey/agents-at-scale-ark/issues/2871
**Pull Request:** [GitHub PR link, once opened]

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

**Unit 6: Installed the voice guard and checked the real-repository workflow**

2026-11-03: I consolidated the newest voice rules into one canonical guide, added concrete claims/questions/pings rules with wrong/right pairs, installed the global PreToolUse hook, and linked all three checker skills to the guide. The wiring test blocked a body-less comment command; the claim later passed the guard and posted after a claim-only repro-check accept. I replaced both classroom checker scopes, patched the scout, installed Ark’s pre-commit hook, and created a local memory file from scoped orientation. The main shortcoming was the scout’s missed parent visibility gate: the component attempt could not reproduce the settled-empty symptom, so I saved the accepted full repro-check package and the corrected scout rejection instead of inventing a fix.

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

I compared two candidates from my existing shortlist, Ark #2871 and clearlydefined/service#830, using my issue scout after its broad TypeScript/Python scan. The initial rubric accepted #2871 and rejected #830 over its unresolved API response design. After the Unit 6 scope-feasible patch, both passed: #2871 was rated straightforward, while #830 was ambitious because a maintainer still needs to settle how invalid batch entries should be represented. I chose #2871 because its React/TypeScript empty-state behavior matches my frontend experience and has a clear observable outcome: hide or disable “Use via API” when there are no agents. I want to learn how this unfamiliar dashboard handles agent availability and test the behavior without expanding into a backend change.

The scout was useful because it compared concrete evidence, including comments, assignees, linked work, and contribution policy. Its broad scan also exposed weaknesses: language metadata did not ensure component fit, the ranking favored very new issues, and the original availability check accepted an issue already fixed by a merged PR. I tightened availability to reject completed work, installed scope-feasible and its difficulty notes, and aligned the installed evidence guide with the patch. GitHub checks found #2871 open, unassigned, without claim comments or linked PRs; the initial source check incorrectly inferred visible behavior from the unconditional action prop, without tracing its parent gate. My selection-site check reported #2871 unclaimed; selection changes and unclaiming any other picks have not been independently verified by the automation. Claim: [Claim posted 2026-11-03](https://github.com/mckinsey/agents-at-scale-ark/issues/2871#issuecomment-6614608081), after claim-only repro-check accepted the draft and the voice guard passed it. After posting, scoped orientation and runtime probes found the action already hidden for a settled empty list at commit `63d31cc`. The post-reproduction scout re-grade now **rejects #2871** on Work is available: the originally requested outcome is already delivered, and no maintainer has identified remaining work. I am not silently proceeding against that verdict: implementation is on hold pending clarification of a current deployed-version symptom or the loading/error edge, or selection of another issue. The full-package repro-check accepts my explicitly limited cannot-reproduce report.

**Toolkit**

- Tool: issue-scout with my preserved Unit 1 rubric and evidence guide, a TypeScript/Python search strategy, direct finalist grading, and the Unit 6 scope-feasible patch.
- What it produced: a saved five-issue scan, original grades for both finalists, patched grades accepting #2871 (straightforward) and #830 (ambitious), followed by a post-reproduction correction rejecting #2871 because the settled-empty outcome already occurs.
- Difficulties: language-only search surfaced environment-heavy or mismatched tasks; a merged fix slipped through the availability rule; the old scope guidance conflicted with the new rubric.
- What changed: tightened completed-work availability, replaced Bounded and settled scope with scope-feasible, added difficulty notes, and aligned the installed evidence guide. Full before/after readouts, the later corrected verdict, and dated notes are saved in the installed scout directory. Future source checks must follow parent visibility gates instead of inferring visibility from a child prop.

---

## Understanding the Issue

**Problem Description**

The Agents page offers “Use via API” even when there are no installed agents. The issue reports that clicking it then does nothing. This describes the reporter’s observation. My component attempt at commit `63d31cc` did not reproduce it once the empty list settled.

**Expected Behavior**

When no agents are present, the button should be hidden or disabled, as the issue permits either behavior.

**Current Behavior**

The reporter says the button remains available but does nothing with no agents installed. At tested commit `63d31cc`, my component-level attempt instead showed the button absent once the empty result loaded; see Reproduction Process for the limits and evidence.

**Affected Components**

The Ark dashboard (Next.js/React/TypeScript), especially the Agents section and its API access dialog. The relevant files are `components/sections/agents-section.tsx`, `components/sections/resource-list-section.tsx`, `components/dialogs/agents-api-access.tsx`, and `components/dialogs/agents-api-dialog.tsx`. The shared section, not just the action prop, controls visible empty-state behavior.

**Toolkit**

- Tool: a scoped dashboard orientation run and direct source inspection, followed by Testing Library probes.
- What it produced: a trace from AgentsSection through ResourceListSection to the API action/dialog, identifying the real visibility gate.
- Difficulties: the scout's first source check stopped at the action prop and missed the parent gate.
- What changed: checked rendered behavior with settled-empty/nonempty/loading controls; no product fix is claimed.

---

## Reproduction Process

**Environment Setup**

2026-11-03: macOS 26.6.2 (25G83), arm64; Node v24.15.0, npm 11.12.1. I cloned [my Ark fork](https://github.com/MalikSCole/agents-at-scale-ark) at `63d31cc5d7aba00b09cc8c32a00da967f72d4e05`, then ran `npm ci` in `services/ark-dashboard/ark-dashboard`. The locked install uses Next.js 16.4.1, React 19.2.7, Vitest 4.1.11, and jsdom 25.0.1; installation succeeded. npm reported 26 dependency vulnerabilities (2 low, 23 moderate, 1 high); I did not change dependencies. The default production build failed first on a sandboxed Google Fonts fetch and then, with network access, on a Turbopack worker port restriction; `npm run build -- --webpack` succeeded with warnings (middleware deprecation and Edge Runtime API warnings). This build check is not a browser reproduction. I installed the required pre-commit hook and kept CLAUDE.local.md and the temporary probe out of the PR with `.git/info/exclude`.

This is a component-level attempt using the repository’s existing namespace/router mocks and a mocked agent-query hook. I did not run a browser, Next.js server, Kubernetes cluster, or real API; the reporter did not specify an environment or version. This result does not establish behavior in a deployed system, older version, or every loading/error race. AI assisted this investigation and report; the commands and artifacts below were executed and checked locally.

**Steps to Reproduce**

1. Clone the public fork and pin the tested source:

   ```bash
   git clone https://github.com/MalikSCole/agents-at-scale-ark.git
   cd agents-at-scale-ark
   git checkout 63d31cc5d7aba00b09cc8c32a00da967f72d4e05
   cd services/ark-dashboard/ark-dashboard
   npm ci
   npm test -- __tests__/unit/components/sections/agents-section.test.tsx __tests__/unit/components/dialogs/agents-api-dialog.test.tsx
   cp __tests__/unit/components/sections/agents-section.test.tsx __tests__/unit/components/sections/issue-2871-repro.test.tsx
   ```

2. Append the full block below to the copied `issue-2871-repro.test.tsx`. It reuses the original test’s imports, mocks, sampleAgents, and mockQueryResult; no private fixtures are needed.

<details>
<summary>Complete reproduction probe to append</summary>

```tsx
describe('issue 2871 reproduction on current main', () => {
  beforeEach(() => {
    vi.clearAllMocks();
    mockReadOnly.value = false;
  });

  it('settled empty agents hide Use via API', async () => {
    mockUseGetAllAgents.mockReturnValue(mockQueryResult({ data: [] }));
    render(<AgentsSection />);
    expect(await screen.findByText('No agents yet')).toBeInTheDocument();
    expect(screen.queryByRole('button', { name: 'Use via API' })).not.toBeInTheDocument();
    console.log('2871: settled empty list -> No agents yet visible; Use via API absent');
  });

  it('nonempty control retains an enabled Use via API action', async () => {
    mockUseGetAllAgents.mockReturnValue(mockQueryResult({ data: sampleAgents }));
    render(<AgentsSection />);
    await screen.findByTestId('agents-table');
    expect(screen.getByRole('button', { name: 'Use via API' })).toBeEnabled();
    console.log('2871: nonempty control -> Use via API present and enabled');
  });

  it('loading action disappears when the list resolves empty', async () => {
    mockUseGetAllAgents.mockReturnValue(mockQueryResult({ isPending: true }));
    const view = render(<AgentsSection />);
    expect(screen.getByRole('button', { name: 'Use via API' })).toBeEnabled();
    mockUseGetAllAgents.mockReturnValue(mockQueryResult({ data: [] }));
    view.rerender(<AgentsSection />);
    expect(await screen.findByText('No agents yet')).toBeInTheDocument();
    expect(screen.queryByRole('button', { name: 'Use via API' })).not.toBeInTheDocument();
    console.log('2871: loading -> action enabled; resolved empty -> action absent (related transient edge)');
  });
});
```

</details>

3. Run the probe:

   ```bash
   npm test -- __tests__/unit/components/sections/issue-2871-repro.test.tsx --reporter=verbose
   ```

4. Observe the settled-empty case (data=[], isPending=false, error=null), the nonempty control, and the pending-to-empty transition. The issue expects the action hidden or disabled when no agents exist. In the settled-empty case “No agents yet” is visible and the action is already absent. With agents present it is enabled. During loading it is briefly enabled, then disappears when the empty result resolves.

**Reproduction Evidence**

- **Commit showing reproduction:** no product-change commit was created in the fork. The tested source is [63d31cc in my fork](https://github.com/MalikSCole/agents-at-scale-ark/commit/63d31cc5d7aba00b09cc8c32a00da967f72d4e05); the runnable probe and observed output are recorded in this coursework story. The fork working tree remains clean because the local probe and memory file are excluded; no application changes were committed or pushed to the fork.
- **Screenshots/logs:** no browser screenshot; this was a jsdom component run. The baseline existing tests passed (2 files, 24 tests, exit 0). The copied probe file passed (10 tests: 7 copied baseline cases and 3 focused probes, exit 0). The complete probe run is below.
- **My findings:** cannot reproduce the reported settled-empty symptom at this component boundary at commit `63d31cc`. ResourceListSection computes `isEmpty = !loading && !hasError && items.length === 0` and renders header actions only when `!isEmpty`; its empty-state actions contain Create and Learn more, not Use via API. The loading-state observation is an adjacent edge, not proof of the original report. No root cause for the reporter’s environment or product fix is claimed. A maintainer/version check is needed before proposing remaining work.

<details>
<summary>Observed reproduction output</summary>

```text
> ark-dashboard@0.1.0 test
> vitest run __tests__/unit/components/sections/issue-2871-repro.test.tsx --reporter=verbose

(!) Your Vite config uses features that are unsupported by `configLoader: 'native'`, which is planned to become the default in a future major version of Vite:
  - `__dirname` (vitest.config.ts:32:25). Use `import.meta.dirname` instead
Set `VITE_CONFIG_NATIVE_IGNORE_WARNING=true` to suppress this warning.

 RUN  v4.1.11 /Users/admin/ai301-coursework/agents-at-scale-ark/services/ark-dashboard/ark-dashboard

 ✓ __tests__/unit/components/sections/issue-2871-repro.test.tsx > AgentsSection > shows Loading... while data is pending 19ms
 ✓ __tests__/unit/components/sections/issue-2871-repro.test.tsx > AgentsSection > shows the empty state when there are no agents 27ms
 ✓ __tests__/unit/components/sections/issue-2871-repro.test.tsx > AgentsSection > renders AgentsTable with returned agents 15ms
 ✓ __tests__/unit/components/sections/issue-2871-repro.test.tsx > AgentsSection > filters by search term (case-insensitive) 32ms
stdout | __tests__/unit/components/sections/issue-2871-repro.test.tsx > issue 2871 reproduction on current main > settled empty agents hide Use via API
2871: settled empty list -> No agents yet visible; Use via API absent

stdout | __tests__/unit/components/sections/issue-2871-repro.test.tsx > issue 2871 reproduction on current main > nonempty control retains an enabled Use via API action
2871: nonempty control -> Use via API present and enabled

stdout | __tests__/unit/components/sections/issue-2871-repro.test.tsx > issue 2871 reproduction on current main > loading action disappears when the list resolves empty
2871: loading -> action enabled; resolved empty -> action absent (related transient edge)

 ✓ __tests__/unit/components/sections/issue-2871-repro.test.tsx > AgentsSection > disables Create Agent button in readOnly mode 10ms
 ✓ __tests__/unit/components/sections/issue-2871-repro.test.tsx > AgentsSection > renders Create Agent link when not readOnly 8ms
 ✓ __tests__/unit/components/sections/issue-2871-repro.test.tsx > AgentsSection > surfaces a load error via toast instead of a silent empty state 4ms
 ✓ __tests__/unit/components/sections/issue-2871-repro.test.tsx > issue 2871 reproduction on current main > settled empty agents hide Use via API 4ms
 ✓ __tests__/unit/components/sections/issue-2871-repro.test.tsx > issue 2871 reproduction on current main > nonempty control retains an enabled Use via API action 8ms
 ✓ __tests__/unit/components/sections/issue-2871-repro.test.tsx > issue 2871 reproduction on current main > loading action disappears when the list resolves empty 6ms

 Test Files  1 passed (1)
      Tests  10 passed (10)
   Start at  15:30:03
   Duration  944ms (transform 226ms, setup 91ms, import 396ms, tests 134ms, environment 248ms)
```

</details>

**Toolkit**

- Tool: repro-check in full-package live mode, plus scoped dashboard orientation and Vitest/Testing Library/jsdom probes.
- What it produced: a complete claim/reproduction draft with pinned source, environment, runnable fixture, output, nonempty/loading controls, and a limited cannot-reproduce conclusion. Full-package repro-check accepted all six required checks, with no voice-guide violations; it accepted an evidenced cannot-reproduce result, not a confirmed bug.
- Difficulties: the earlier scout read an unconditional headerActions prop as proof of visible behavior and missed the parent gate. A full browser/cluster run was not performed, so I cannot generalize beyond the component boundary.
- What changed: traced the complete render path, checked runtime behavior, recorded the environment difference explicitly, and requested a post-reproduction scout re-grade. I did not turn the loading edge into an unverified reproduction claim or implement an unrelated fix. The post-reproduction scout rejects #2871 as originally reported; a maintainer follow-up draft is prepared locally and has not been posted.

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

**2026-11-03**

Completed Unit 5 scout setup, broad scan, review notes, two finalist grades, and the Unit 6 scope/voice-guard upgrades. Posted the accepted claim through Claude Code after the guard passed, forked/cloned Ark, installed its pre-commit hook, and created local repository memory from scoped orientation. No application code has changed. The baseline component tests passed (24/24); the local copied probe passed (10/10, including 3 added controls) and did not reproduce the settled-empty issue at the tested commit. Repro-check accepted the complete cannot-reproduce package; the scout's updated availability verdict rejects the issue as originally described. I prepared a follow-up question rather than inventing a fix or expanding into the loading/error edge without maintainer direction.

**Toolkit**

- Tool: issue-scout, voice guard, repro-check, scoped repository memory, and Vitest.
- What it produced: a traceable setup/claim/reproduction trail and a corrected issue-selection decision.
- Difficulties: a source-only scout inference missed shared parent rendering; the runtime attempt corrected it.
- What changed: held implementation, saved the superseding rejection and bounded cannot-reproduce evidence, and drafted a maintainer clarification.

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Ark contribution rules](https://github.com/mckinsey/agents-at-scale-ark/blob/main/CONTRIBUTING.md): ticket scope, conventional PR titles, pre-commit hooks, and DCO sign-off.
- [Ark repository instructions](https://github.com/mckinsey/agents-at-scale-ark/blob/main/CLAUDE.md): local lint/test gates before pushing.
- [Unit 5 starter](https://github.com/codepath/ai301-unit5-starter): scout setup and search strategy.
- [Unit 6 starter](https://github.com/codepath/ai301-unit6-starter): voice guard, wild scopes, scope-feasible patch, and local memory template.
- [Issue #2871](https://github.com/mckinsey/agents-at-scale-ark/issues/2871): reported symptom, screenshot, and expected empty-state behavior.
