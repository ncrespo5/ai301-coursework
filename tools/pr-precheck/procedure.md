# Procedure: how this tool grades a PR package

## Read order

1. Resolve one issue and package. In live mode enforce the scope and gather repo facts. In eval mode use the supplied snapshot.
2. Read the issue, repro, and plan before reading the candidate. Record the trigger, baseline behavior, accepted scope, exclusions, deviations, and proposed checks.
3. Read the commit list and diff to map actual changes. Then read the title, description, and captured results for the candidate's claims.
4. Review the repo template, policies, and concrete maintainer requests before assigning grades.

## Evidence gathering

For each changed area, pair the relevant hunks with plan scope or a documented deviation, then compare the description with the diff. Pair the original trigger and expected after-state with the test output, and list each applicable repo check with its result. Flag material diff debris and compare the actual title and body with applicable project standards. Use the evidence guide to locate each item.

## Check execution

Grade each row in rubric order, independently. Rewrite no evidence. If a deciding fact is missing after a targeted reread, mark unclear and name what is missing. Quote or describe one observed fact per check. Apply the voice guide separately in live mode.

## Verdict assembly

Use the rubric's binary verdict. For a reject, identify the first failed or unclear required check in rubric order in the summary and report all checks in the final JSON. Follow the fixed schema in SKILL.md.
