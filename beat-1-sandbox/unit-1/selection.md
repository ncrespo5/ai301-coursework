# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

[The individual Path Review issue page. A link to the repository or the issue list
does not satisfy this field.]

**Verdict output**

[Your skill's live-mode output for this issue, pasted verbatim and ending with the
fenced JSON verdict block. A summary does not satisfy this field.]

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

```
paste the output here, including the closing JSON block
```

---

## Eval iterations

**Run history**

1. `agreement: 14/20 scored items  (bar: 18/20: below the bar)`
2. `agreement: 18/20 scored items  (bar: 18/20: PASS)`

**Issue analysis**

**issue-02** changed from accept to reject, matching the gold label of reject. The required repository check failed on this evidence from the second run:

> Last push 2024-06-19, release 2023-12-09 and last commit 2023-12-09 are all over 12 months before the 2026-08-05 capture; all 5 sampled issues show 'no maintainer comment in thread'.

The original rubric accepted the bounded fix because the repo was unarchived and the recent-activity check was a preference. The revised rubric rejects the combination of old repository activity and no maintainer response.

**Check rationale**

The **Repository open to contributions** check reads:

> Fail if archived, read-only, or explicitly closed to contributions. Also fail if there is direct evidence of prolonged inactivity: all available push, release, and commit dates are older than 12 months, and the reviewed threads and response sample show no maintainer intervention within that period. Pass for an unarchived repo without a closure notice when there is evidence of a push, commit, release, or maintainer response within 12 months. A missing release record by itself is not evidence of inactivity.

The check gives an older but maintained project a path to pass while filtering out a project with sustained inactivity. The separate 90-day preference still ranks candidates without excluding every quiet repository.

**Trade-offs**

The inactivity rule can reject a mature project that still quietly accepts patches when GitHub shows no recent activity or replies. The scope rule also rejected two gold-accept cases in the passing run:

```text
issue-04  accept  reject   NO     failed: Bounded change
issue-19  accept  reject   NO     failed: Bounded change
```

One description left its list of fixes open-ended, and the other proposed several possible changes across UI and concurrency. Requiring a bounded change makes the rubric more cautious in those cases.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

[Answer all three:

1. The issue's fit to your interests and to the time available.
2. What the verdict identified correctly, and what you weighed that the rubric could
   not.
3. The anticipated difficulty in claiming it.]

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
