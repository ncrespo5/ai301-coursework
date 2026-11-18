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

https://github.com/codepath/pathreview-ai301-fa26-howard/issues/55

**Verdict output**

**Verdict: accept.** Issue #55 ("Skill extractor fails to detect JavaScript and TypeScript") passes all four required checks and the preferred one.

Scope check: the issue is in `codepath/pathreview-ai301-fa26-howard`, the scoped repo. Under the Path Review house rule, classmates' claim comments don't block it. There are none anyway.

| Check | Weight | Grade | Evidence |
|---|---|---|---|
| Bounded change | required | pass | The fix is detection logic in `ingestion/parsers/skill_extractor.py` (`_detect_languages`, `_detect_tools`, `_detect_databases`). It is verified by five existing `xfail` tests via `pytest tests/unit/test_skill_extractor.py -q`. It carries `bug`, `ingestion` and `tier-1` labels. |
| No duplicate work | required | pass | No assignees, nothing in the Development panel and no comments. None of the 23 open PRs touches `skill_extractor`. The closest, #85, is a tech detector fix for issue 57, a different issue. |
| Repository open to contributions | required | pass | No archive notice and no closure notice. The newest commit is Sep 16, 2026 and the newest PR is #97, opened Nov 16, 2026, both within 12 months. No release exists, which isn't evidence of inactivity. |
| Contribution policy | required | pass | `docs/CONTRIBUTING.md` says nothing about AI. It requires tests, `make check && make test-unit`, the PR template, `<type>/<issue-number>-<desc>` branch names and Conventional Commits. I couldn't read the PR template's text, so I can't rule out an AI-disclosure checkbox. Disclosure wouldn't be a ban anyway. |
| Recent activity | preferred | pass | Human-authored commits on Sep 16, 2026, which is about 62 days before today (Nov 17, 2026). I saw no maintainer reply on the issue. |

**Fit:** it matches your profile closely. It's a Python parser bug about JavaScript and TypeScript detection, in one file, verified by focused tests.

**Notes for the PR:**
- Per `docs/CONTRIBUTING.md`, remove the `xfail(strict=True)` markers when the tests pass. Otherwise CI fails with `XPASS(strict)`.
- Remove any matching `pyproject.toml` suppressions for the seeded bugs.
- Don't run `ruff --fix --unsafe-fixes`.
- Two of the five tests, the devops and docker-compose ones, concern `_detect_tools` rather than JS/TS. You could do the JS/TS pair first, but the issue as written covers all five.

```json
{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-howard/issues/55",
  "checks": [
    {"name": "Bounded change", "grade": "pass", "evidence": "Detection fixes in one file (ingestion/parsers/skill_extractor.py: _detect_languages/_detect_tools/_detect_databases), verified by five existing xfail tests via pytest tests/unit/test_skill_extractor.py -q; labeled bug, ingestion, tier-1."},
    {"name": "No duplicate work", "grade": "pass", "evidence": "Assignees: None; Development: none; zero comments; none of the 23 open PRs touches skill_extractor (#85 is for issue 57, a different issue)."},
    {"name": "Repository open to contributions", "grade": "pass", "evidence": "No archive or closure notice; latest commits Sep 16, 2026 and newest PR #97 opened Nov 16, 2026, both within 12 months of today (2026-11-17)."},
    {"name": "Contribution policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has no AI/LLM restriction or disclosure rule; requires tests, make check && make test-unit, PR template, removal of xfail markers. PR template text not read."},
    {"name": "Recent activity", "grade": "pass", "evidence": "Human-authored commits on Sep 16, 2026 (about 62 days before today); no maintainer reply seen on the issue."}
  ],
  "verdict": "accept"
}
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
