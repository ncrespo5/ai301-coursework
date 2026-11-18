# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-howard/pull/98

**PR precheck verdict**

The first live precheck returned `reject` because the draft changed existing database display labels. The branch now preserves those labels, and the PostgreSQL fixture checks the exact label and one result when both a direct reference and an alias are present. The revised draft returned `accept` with all five required checks passing.

```json
{
  "item": "codepath/pathreview-ai301-fa26-howard#55 <- ncrespo5:fix/55-skill-extractor-detection (fa9bd21)",
  "checks": [
    {
      "name": "Plan fidelity",
      "grade": "pass",
      "evidence": "Diff updates the language, database and tool detectors and removes the five xfail markers as planned; the extra name/suffix signals and stronger PostgreSQL test are listed in the PR's Changes section."
    },
    {
      "name": "Reproduction proof",
      "grade": "pass",
      "evidence": "Same --runxfail command: pytest-before.txt '5 failed, 13 passed' on 99673c7 vs pytest-after-runxfail.txt '18 passed' on fa9bd21; normal run also '18 passed'."
    },
    {
      "name": "Repository verification",
      "grade": "pass",
      "evidence": "Local versions of all five CI jobs reported (lint/Black pass, mypy 76 files clean, 380 passed/48 xfailed, integration exit 5 per workflow shim, frontend 18 passed); hosted CI is honestly marked as pending until the PR is opened, which CONTRIBUTING allows."
    },
    {
      "name": "Reviewable diff",
      "grade": "pass",
      "evidence": "Only ingestion/parsers/skill_extractor.py and tests/unit/test_skill_extractor.py changed; no debug output, dead code or unrelated churn."
    },
    {
      "name": "Project standards",
      "grade": "pass",
      "evidence": "All template sections filled with 'Closes #55', conventional fix(ingestion) commits, xfail markers removed, and the required Unit 8 AI-use disclosure is in Notes for Reviewers."
    }
  ],
  "verdict": "accept"
}
```

**GitHub Actions**

https://github.com/codepath/pathreview-ai301-fa26-howard/actions/runs/44296758197

**Branch**

`fix/55-skill-extractor-detection`

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. `agreement: 20/20 scored items  (bar: 18/20: PASS)`

**Package analysis**

`pkg-02  clear-accept    accept  accept   yes`

The rubric accepted `pkg-02`, matching the gold label. The before run lost the recorded console output after a failed save. The branch preserved it, as shown by the after result `'IMPORTANT OUTPUT\n'`. The tests also checked that a successful save still clears the output. The diff follows the plan’s order of exporting with `clear=False`, writing, and clearing only after a successful write.

**Check rationale**

The **Reproduction proof** check says:

> The evidence connects the original trigger to a concrete post-fix observation, with the before result in the repro or in the PR. A clearly reported unchanged condition or limitation is acceptable if the delivered change still has direct, relevant proof. A vague claim or a test that misses the original behavior fails.

The same failing input gives a direct way to tell whether a fix changed the reported behavior. The rule also accommodates a scoped change when the author can show a relevant improvement and state which condition still remains.

**Trade-offs**

`pkg-07  not-tested      reject  reject   yes`

The rubric rejected `pkg-07` even though its diff followed the plan and the one-file control passed. The package only recorded `golangci-lint run --fix ./onefile/ && go build ./onefile/`, while the original problem required edits spanning two files. This rule can hold a correct patch until the author captures a comparable result, but it prevents a passing control from covering for missing evidence on the reported failure.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
