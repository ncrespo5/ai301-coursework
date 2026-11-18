# Rubric: is this a good first issue?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Bounded change | Issue body, linked files, and maintainer comments that define expected behavior or expand the scope. | Pass when the issue has one clear goal and the change is plausibly limited to one component and at most three implementation files, plus its tests and documentation. Fail for umbrella issues, cross-component rewrites, unresolved design decisions, or support questions with no code or documentation change to make. | required |
| No duplicate work | Issue Development panel and comments, linked PR state and scope, and Assignees panel. | Pass after checking those sources and finding no open PR that implements the same change or other clear evidence of active ownership. Fail if there is an open PR for the same change, or a maintainer has assigned or confirmed another contributor is actively implementing it. Apply the Path Review house rule in live mode to classmates’ claim comments. A closed PR without a current owner or replacement does not by itself block the issue. | required |
| Repository open to contributions | Archived flag and any maintainer notice that the repository is read-only or no longer accepts contributions. | Pass if the repository is unarchived and has no notice closing contributions. Fail if it is archived, read-only, or explicitly closed to contributions. | required |
| Contribution policy | Contribution policy in the snapshot, or live contributor docs, AI policy, and PR template. | Pass if the published policy allows the planned workflow or the checked sources are silent. Disclosure, testing, and human-review requirements are acceptable if they can be followed. Fail if the policy explicitly rules out the planned AI-assisted workflow. | required |
| Recent activity | Last five default-branch commits and maintainer replies on the issue or in the repo-facts response sample. Use the snapshot date in eval mode and today in live mode. | Pass if there is a human-authored or human-merged commit or a maintainer reply within 90 days. Fail if the dates are known and all are older. | preferred |

## Verdict rule

Accept when every required check passes. Reject if a required check fails or remains unclear after checking its evidence. A preferred check only helps rank accepted issues. Old or unclear activity alone does not rule out a contribution.
