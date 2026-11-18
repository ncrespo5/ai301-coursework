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

[Link to the pull request you opened. It must be the pull request's own page on the Path
Review repo, not your fork's branch page.]

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
