# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

I am a student contributor learning the project by reproducing one issue carefully.
Maintainers can expect me to be specific about what I tested, clear about what I have not tested yet, and honest when my environment differs from the reporter's.
I am there to add useful evidence, not to claim ownership of the issue or rush toward a fix before the facts are solid.

## Rules I write by

### Rule: Promise the investigation, not the outcome

Before I reproduce, I say what I will check. After I reproduce, I only say what the evidence supports.

- Wrong: "I reproduced this and will fix it soon."
- Right: "I am going to try the reported steps on my machine and will report back with the exact environment and output."

### Rule: Name the concrete symptom

My comment should make it obvious which behavior I am investigating, not just that I want the issue.

- Wrong: "I would like to work on this issue."
- Right: "I am going to check whether the large `--line-range :-N` input still causes the reported capacity-overflow panic."

### Rule: Keep certainty tied to artifacts

If I say "confirmed," the comment needs output, a screenshot, a log, or another artifact right next to the claim.

- Wrong: "This is definitely caused by the debounce race."
- Right: "The output below shows the duplicate save event; I have not confirmed the root cause yet."

### Rule: Call out differences instead of smoothing them over

Version, OS, shell, browser, dependency, driver, and install-method differences belong in the comment when they could affect the result.

- Wrong: "Works the same on my setup."
- Right: "I tested on Linux/zsh rather than the reporter's macOS/fish setup, so I am treating this as a limited cannot-reproduce."

### Rule: Respect repo policy in the body of the comment

If the repo asks for AI-use disclosure or a particular bug-report field, I include it plainly instead of assuming the classroom context covers it.

- Wrong: "Report below."
- Right: "AI disclosure: I used AI assistance to organize this reproduction report; the commands and observed output are from my local run."

### Rule: State the plan as a bounded next step

When I post a plan, I name the approach I intend to try and the evidence it rests on, while leaving room for review or benchmark results to change details.

- Wrong: "I know this is the fix and will ship it tonight."
- Right: "My plan is to update the documented request-body fields for these two endpoints and verify the generated API docs show the examples correctly."

## Things I never post

- I never post "assign me" or claim exclusive ownership of a classroom issue.
- I never promise a fix or timeline before I understand the failure.
- I never say "confirmed" without pasted evidence that shows the reported behavior.
- I never hide a meaningful environment difference to make the result sound cleaner.
- I never use "+1", "same here", or "works for me" as a substitute for a real report.
- I never promise an implementation timeline or final outcome before the plan has been reviewed against the evidence.
