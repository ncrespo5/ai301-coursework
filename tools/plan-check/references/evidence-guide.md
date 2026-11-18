# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

Read the issue's observed and expected behavior and the repro-evidence block before reading the plan's diagnosis. Live evidence comes from the issue and the student's posted reproduction, or the quoted house reproduction where applicable. Compare the specific trigger and output with what the proposed cause would explain.

## Scope

Compare the plan's proposed files, areas, behavior changes, and any exclusions with the issue and thread. Necessary supporting changes can share the same scope. Separate changes that would warrant their own issue or independent review.

## Executability

Read the implementation actions and their order. Locate the component or code path, the first verifiable step, and what the plan proposes after that step. Check whether the remedy changes the behavior responsible for the repro. Treat a concrete diagnostic step as valid when the root cause remains uncertain.

## Test plan

Map the stated command or manual action, inputs, and expected outcome to the original trigger. Prefer a test that would expose the bug before the fix and distinguish the intended result afterward. A reference to the documented reproduction can supply the input if the plan identifies the expected outcome.

## Honesty

Compare claims in the plan and comment with the evidence and explicit constraints. Distinguish established observations from hypotheses. Check whether unresolved prerequisites, scope choices, material risks, and any known deviations are named or paired with a validation step.

## Comms

Read the comment against the proposed plan, issue thread, and repository facts. In live mode consult the posted thread, contributor docs, and applicable templates. Record concrete maintainer requests and explicit rules, including any disclosure condition that applies to the communication. Missing optional formatting does not affect the verdict.
