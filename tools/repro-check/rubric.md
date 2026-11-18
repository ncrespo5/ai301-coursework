# Rubric: is this reproduction package ready to post?

## Checks

| Check | Evidence | Pass condition | Weight |
| --- | --- | --- | --- |
| Targeted claim | Claim draft against the issue title, body, and thread. | The claim identifies the issue or the specific behavior that will be investigated and makes a bounded commitment. A project-wide or generic claim, or a guarantee of a fix or timeline that the draft cannot support, fails. In live mode, a classmate's claim does not block a PathReview claim. | required |
| Relevant environment | Repro report's environment and setup against the issue's affected versions, platform, configuration, and code state. | The report identifies the revision or release and the runtime, platform, or settings material to the bug. Any material deviation from the reported environment is named and scoped. Incidental versions that cannot affect the behavior are optional. | required |
| Followable steps | Repro report's starting state, fixtures or inputs, command or UI sequence, and trigger. | A maintainer with the stated environment can reproduce the experiment without guessing a prerequisite, value, fixture, or action material to the result. When an upstream issue already provides a recipe, a precise reference can supply steps if the report identifies the recipe and describes any changes. | required |
| Proof matches the issue | Test output, logs, screenshot, or concrete observed result against the issue and the reproduction steps. | Evidence shows the exact failing behavior or an evidenced cannot-reproduce attempt for the same trigger and target. A passing assertion, expected-failure marker, or generic error alone is insufficient unless its output or context identifies the relevant behavior. Adjacent issues, errors that prevent the trigger from running, and claims with no observable result fail. | required |
| Outcome matches the evidence | Expected and observed behavior, the report's conclusion, and any limitations against its supplied artifacts. | The report distinguishes what was expected from what happened. It states whether it reproduced or could not reproduce and limits its conclusion to the observed conditions. An evidenced cannot-reproduce on the correct target is acceptable. An unsupported diagnosis, failure reduced to a missing prerequisite, or confidence beyond the artifacts fails. | required |
| Repository conventions | Both drafts read against stated issue templates, contribution docs, and any explicit disclosure requirement in repo facts or the issue thread. | The relevant comments satisfy the repository's stated requirements, including an explicit disclosure where one is required. An absent optional heading does not matter. If the repo has no applicable stated requirement, this check passes. | required |

## Verdict rule

Accept when every applicable required check passes. Reject if an applicable required check fails or remains unclear. In live claim-only mode, grade only Targeted claim and the claim's applicable Repository conventions. Report the other checks as unclear because the reproduction draft is not yet applicable, and omit them from the verdict.
