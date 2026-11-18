# Rubric: is this plan ready to post and build from?

## Checks

| Check | Evidence | Pass condition | Weight |
| --- | --- | --- | --- |
| Grounded diagnosis | Issue's expected behavior, repro steps and output, and the plan's diagnosis. | The diagnosis explains the reproduced behavior without contradicting the evidence. A plausible but unconfirmed cause may pass when clearly labeled and paired with a concrete investigation. | required |
| Bounded scope | Issue and thread requirements versus the plan's stated changes and exclusions. | The plan covers one coherent, reviewable improvement. Necessary related edits are fine. Unrelated improvements, redesigned APIs without demonstrated need, and a broad rewrite when a local fix is viable fail. | required |
| Remedy addresses the cause | Proposed implementation compared with diagnosis, repro evidence, and relevant code path. | The change targets the defect or provides a concrete first step to locate and address it. Suppressing the reported symptom or changing expected behavior without resolving the mismatch fails. | required |
| Actionable implementation | Plan's ordered steps, named files, symbols, or unambiguously located behavior, and necessary prerequisites. | Another maintainer can identify the first concrete action and how to proceed to the fix. Exact line numbers and settled implementation choices are optional when the investigation or code path is clear. | required |
| Observable verification | Test plan compared with the repro trigger and expected behavior. | Identifies a check, a trigger or fixture, and what success looks like. It can use the supplied reproduction, an automated regression case, or a specified manual sequence. A generic instruction to run tests without a relevant outcome fails. | required |
| Honest unknowns | Plan and comment's claims, uncertainty, and constraints compared with repro and thread evidence. | Confident statements match the evidence. Material unknowns are stated or have an investigation step. A report may omit a risks heading if the work has no unresolved issue material to the plan. | required |
| Thread and repo fit | Draft plan comment against the plan, existing issue thread, maintainer constraints, and applicable contribution policy. | The comment identifies the approach in context, is consistent with the plan, and respects explicit, applicable constraints and disclosure requirements. A concise comment may reference the plan or reproduction for detail. | required |

## Verdict rule

Accept if every required check passes. Reject if any required check fails or remains unclear after inspecting its stated sources. Record one concrete fact or quote for each check. Preserve the distinction between genuinely missing evidence and evidence of failure.
