# Rubric: is this pull request ready to submit?

## Checks

| Check | Evidence | Pass condition | Weight |
| --- | --- | --- | --- |
| Plan fidelity | Issue and plan scope, documented deviations, PR title and description, changed hunks and commits. | The diff delivers the described change within the plan and explained deviations. A scoped partial result or justified deviation may pass when the description states the boundary and does not claim omitted work. Silent extra work, missing promised behavior, and a misleading description fail. | required |
| Reproduction proof | Original reproduction, plan's validation steps, and actual test evidence on the PR branch. | The evidence connects the original trigger to a concrete post-fix observation, with the before result in the repro or in the PR. A clearly reported unchanged condition or limitation is acceptable if the delivered change still has direct, relevant proof. A vague claim or a test that misses the original behavior fails. | required |
| Repository verification | Repo facts and test or CI output for the changed files and required checks. | The report names the applicable project checks and gives their observed outcomes. An honestly explained gap can pass if policy permits it, the reason and impact are explicit, and other evidence verifies the delivered behavior. An unexplained missing check, a relevant unresolved failure, or an unsupported pass claim fails. | required |
| Reviewable diff | Diff and commit list, read against the scoped outcome. | A reviewer can trace the fix and tests without unrelated edits or material debris. Relevant cleanup and a small supporting test or diagnostic change may pass. Debug leftovers, dead blocks, and unrelated churn that obscures the fix fail. | required |
| Project standards | PR title and description against applicable PR template, repo policy, and explicit maintainer requests. | Required sections contain meaningful answers, required disclosures describe the requested scope, and explicit maintainer constraints are respected. Optional formatting and a missing disclosure where no policy requests one do not fail. | required |

## Verdict rule

Accept if all required checks pass. Reject for a required fail or unclear after inspecting the named evidence. A candid limitation only passes if it meets the specific check's conditions.
