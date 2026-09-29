# Rubric: is this reproduction package ready to post?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| claim-specific-intent | Claim comment, read against the issue context and the Comms section of `references/evidence-guide.md`. | The claim comment names the issue or its concrete symptom, says what the student will investigate next, and does not claim completed reproduction unless a full repro report is being graded with matching evidence. Boilerplate "assign me", "+1", guaranteed-fix, or ownership language fails. | required |
| environment-recorded | Repro report's environment record, read against the issue's stated target and repo-facts bug-report asks using the Environment section of `references/evidence-guide.md`. | The package records the product/version under test plus the OS/runtime/install details needed for this issue, and any meaningful difference from the issue's target/latest version is named instead of hidden. | required |
| steps-rerunnable | Repro report's commands or actions, setup notes, fixtures, and starting state, read with the Steps section of `references/evidence-guide.md`. | A stranger could rerun the attempt from the report alone, including the trigger input/configuration. Private-only projects, missing fixtures, vague setup, or steps that skip the issue's trigger fail. | required |
| artifact-matches-issue | Repro report's output excerpts, logs, screenshots, measurements, or other artifacts, read against the issue's described current behavior using the Behavior shown section of `references/evidence-guide.md`. | The shown artifact demonstrates the same behavior the issue reports, or demonstrates a well-supported cannot-reproduce attempt against the same trigger. Artifacts showing only that the program ran, a graceful unrelated error, a different symptom, or no artifact fail. | required |
| conclusion-honest | Claim comment and repro report conclusion, compared with the artifacts, environment differences, controls, and thread/repo facts using the Honesty section of `references/evidence-guide.md`. | The outcome stated by the student is no stronger than the evidence: confirmed, partial, version-specific, or cannot-reproduce are all acceptable when backed. Wrong-target certainty, invented root cause, hidden environment deviation, or broad generalization fails. | required |
| repo-policy-followed | Repo facts for templates/contribution policy/AI-use policy plus both candidate comments, using the Comms section of `references/evidence-guide.md`. | The comments satisfy any repo-stated posting requirements that matter to this package, especially required AI-use disclosure. If the repo has no such policy, this check passes unless the comments violate a stated issue/comment template expectation in a way that blocks review. | required |

## Verdict rule

Accept if every required check that is applicable to the package state passes. Reject if any applicable required check fails or is unclear.

In claim-only live mode, checks that require the repro report are not applicable and should be reported as `unclear` with `not yet applicable: claim-only draft`; leave those checks out of the verdict. In eval mode and full-package live mode, all checks are applicable. Preferred checks never change the verdict.
