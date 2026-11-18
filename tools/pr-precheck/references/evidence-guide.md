# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

In an eval bundle, compare plan-context scope and deviations with the candidate diff, commits, title, and description. In live mode use plan.md, branch diff, commit list, and draft PR text. Match material hunks to plan intent. Look for an explanation of related additions or omitted work and a description that states the actual boundaries.

## Test evidence (harness category: not-tested)

In eval use the repro block, plan's test plan, test evidence, repo facts, and any output quoted in the candidate. In live mode inspect the original reproduction, captured reruns, and relevant test or CI results. A before observation and a directly comparable after observation support the fix. List actual observed outcomes for required project checks and any justified omissions.

## Diff quality (harness category: unreviewable)

Read the diff and commits. Verify that changes and tests can be located and understood together. Check whether unrelated renames, generated files, formatting churn, debugging output, or commented-out code distract from review.

## Standards and comms (harness category: standards-wall)

Read the repo-facts block and thread in eval. In live mode inspect the upstream contributor docs, PR template, and the issue thread. Compare required sections, stated disclosures, and explicit maintainer requests to actual PR text. Distinguish repository rules from optional conventions.
