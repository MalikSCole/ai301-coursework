# Evidence guide: where proof lives in a reproduction package

## Environment

Where it lives: In eval bundles, look in the candidate repro report first, then compare it with the issue context and repo-facts bug-report template asks. In live mode, look in the draft repro comment, the issue body/thread, and the repo's bug-report template or contributing docs when available.

What good looks like: A sufficient environment names the software and version tested plus the OS and runtime/install details needed for the reported failure mode. If the issue targets a latest release, a platform-specific shell, a browser, a package manager, a driver, a terminal, or a particular dependency, the report either matches that target or plainly calls out the difference and limits the conclusion.

## Steps

Where it lives: In eval bundles, use the candidate repro report's commands/actions, setup notes, test data, config snippets, fixture descriptions, and any controls. In live mode, use only what the student plans to post in the claim/repro drafts, plus public issue context for the original trigger.

What good looks like: Steps are followable when a stranger can get from a clear starting state to the trigger without guessing hidden files, private repos, missing config, or unstated options. The steps must preserve the issue's meaningful syntax, input shape, platform, and order of operations; a neat command that changes the trigger is not a reproduction.

## Behavior shown

Where it lives: In eval bundles, inspect the candidate repro report's terminal output, logs, screenshots, measurements, stack traces, before/after controls, and explicit expected/actual comparison. In live mode, inspect the artifacts pasted into the draft comment; do not give credit for artifacts only said to exist elsewhere unless the draft links or quotes them clearly.

What good looks like: The artifact shows the same externally observable behavior the issue describes: same error class, missing value, crash mode, rendering defect, measurement direction, or other reported symptom. A valid cannot-reproduce package still shows the attempted trigger and observed non-failure, then explains the likely limiting difference. Artifacts that only show installation, version output, a running app, or a different validation error do not prove the issue.

## Honesty

Where it lives: Compare the claim comment, repro report conclusion, expected/actual text, controls, environment differences, and any issue-thread maintainer notes. In eval mode, the bundle is the complete record; in live mode, also consider the live issue thread when it changes what a careful claim should say.

What good looks like: The conclusion matches the proof. "Confirmed" needs an artifact for the reported behavior; "cannot reproduce" needs a real attempt at the right trigger plus a candid account of differences; "partial" or "version-specific" needs the boundary named. Overconfident language, unsupported root-cause claims, "guaranteed" promises, or presenting an adjacent failure as the reported bug are honesty failures even if the report is polished.

## Comms

Where it lives: In eval bundles, read repo facts for bug-report templates, contribution rules, and AI-use policy; then read the candidate claim comment and repro report as comments on that issue. In live mode, read `scope.md`, the issue thread, repo docs/templates, and the student's draft files.

What good looks like: A good claim comment is modest, specific to the issue, and future-facing when posted before reproduction: it promises an investigation, not a result. A good repro comment gives maintainers enough context to judge and rerun the attempt, follows stated repo policies, and includes AI-use disclosure when the repo requires it. Boilerplate assignment claims, "+1" comments, piggybacking on someone else's work, or missing required disclosure fail.
