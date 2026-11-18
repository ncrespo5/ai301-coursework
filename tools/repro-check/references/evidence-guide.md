# Evidence guide: where proof lives in a reproduction package

## Environment

- In eval, compare the repro report's environment and setup with the issue context and repo facts. In live mode, use the draft and the upstream issue's platform, version, and configuration details.
- Look for the code revision or release and the local variables that matter to the trigger. A clearly scoped platform or version difference can be valid when the report explains what was tested.

## Steps

- Read the setup and action sequence in the repro report. If it refers to a recipe, find the exact steps in the issue context or the linked issue section. Check that the package identifies any variations.
- A stranger should be able to locate inputs or fixtures, set up the relevant state, and take the action that triggers the result. Count missing prerequisites rather than the number of lines.

## Behavior shown

- Find command output, logs, screenshots, concrete observations, or assertion evidence under the repro report and compare them to the issue body, expected behavior, and exact trigger.
- A passing or failing command is only diagnostic if the report ties it to the disputed behavior. A well-evidenced attempt where the bug does not occur can count. An unrelated error or a command that never reached the trigger cannot establish either result.

## Honesty

- Compare what the report says happened with the actual artifact and any differences in environment or inputs. In live mode, use only evidence actually included in the drafts.
- A claim of reproduction needs observed evidence of the reported behavior. A cannot-reproduce conclusion should name the same target, what ran, what happened, and the circumstances that bound the conclusion. Keep suspected causes separate from observations.

## Comms

- Compare the claim text to the issue title, body, and thread. Check both comments against the repo-facts policy in eval mode or the upstream project's contributor docs and applicable templates in live mode.
- A claim should tell maintainers what will be investigated. Apply the course house rule for classmates' claims in live mode. Apply expressed repository requirements, including any mandatory disclosure. Use no layout or heading requirement unless the project actually requires it.
