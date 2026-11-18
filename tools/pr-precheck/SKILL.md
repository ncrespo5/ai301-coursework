---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

Decide whether exactly one pull request package is ready to submit. Compare the candidate title, description, commits, diff, and test evidence with its plan and the issue.

## Inputs and modes

In live mode, read the issue and its thread, the student's plan.md and deviations, the commits, the branch diff from git diff main...HEAD in the working copy, the proposed PR title and body, and captured test results. Read the upstream template and policies. Use the house plan and reproduction pack when assigned to the house chain. In eval mode, read only the supplied bundle and the eval components. Use no tools to fetch evidence, run every check, and apply the full verdict rule.

## The scope seam (live mode only)

Read scope.md first. Stop if the Repo line is an unfilled placeholder and tell the student to fill it with the cohort repo. Refuse packages outside the named repo. Apply its live house rules. Ignore scope.md in eval mode.

## The voice seam (live mode only)

Read voice-guide.md after scope.md. Compare the PR title and body to those rules. Quote any broken rule in the summary. The voice check changes the verdict only if a rubric check explicitly uses it. Ignore the voice guide in eval mode.

## Component reads

Read rubric.md for checks and verdict, references/evidence-guide.md to locate evidence, and procedure.md for the evaluation sequence. Refuse to grade if the rubric or procedure has no authored content. Report a gap in the procedure without inventing a replacement step.

## Verdict and output

Use accept for ready to submit and reject for hold. End the reply with this fenced JSON schema, replacing the placeholders with actual values. Put any summary above the block and leave nothing after it.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

Cite a specific fact or quote for each check. Judge the behavior and evidence, regardless of formatting polish. Apply the rubric and procedure as written. Treat unresolved unclear grades as failures if the verdict rule is silent.
