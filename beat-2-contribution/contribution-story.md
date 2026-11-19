# Contribution: Add an Allure results parser

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Nyla Crespo
**GitHub Username:** ncrespo5
**Issue:** https://github.com/surkuar/testledger/issues/11
**Pull Request:** [GitHub PR link, once opened]

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Issue-scout setup and ownership checks**

November 18, 2026. The issue-scout setup carries forward the issue-selection rubric and adds searches for small Python parser and CLI work. An exploratory GitHub scan surfaced issues with no listed assignee, but their threads showed existing claims or a competing pull request. The revised search strategy prioritizes zero-comment results, and the rubric still checks the thread and open pull requests before an issue is selected.

**Unit 6: [one line on the tool work]**

[2-4 sentences: the voice-guard, the repo-memory file. What broke or
fell short, and what changed because of it. "Nothing broke" counts when
it is true - say how you know.]

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

[1-2 paragraphs in your own words: how you searched, what your scan
surfaced, what your scout's verdict said, why this issue fits your
profile, and what you hope to learn. If your scout's verdict on it
was reject and you chose it anyway, say so here and say why; choosing
against your own tool silently is what loses points. Close with an
honest read of the tool itself: where the scout fell short on a real
wild search and what you changed or would change, or what convinced
you it held up. **Record the link to your claim comment in this section too.**
Not claimed yet? Write `claim pending` and today's date where the link goes,
and add the link the moment your claim lands.]

**Claim:** claim pending (November 18, 2026).

The direct review of TestLedger #11 passed all four required issue-selection checks. The issue lists explicit acceptance criteria and a retry fixture. It had no assignee or claim comment, and the open parser PR covered NUnit XML, a different input format. TestLedger’s contribution guide names Allure parsing as a good first contribution.

**Toolkit**

- Tool: issue-scout (your scout: your search strategy, your rubric),
  and how you used it
- What it produced: [the scan and its verdict on this issue, described]
- Difficulties: [where it fell short, or "none met" if none did]
- What changed: [what you patched or would update, or "nothing"]

---

## Understanding the Issue

**Problem Description**

TestLedger cannot import an `allure-results/` directory. Allure writes each test execution as a separate JSON file, so a single directory can contain both a failure and a subsequent pass for the same test.

**Expected Behavior**

Import each directory as a run. Preserve retries across files sharing a `historyId` as separate, chronologically ordered attempts so the ledger can observe the fail-to-pass sequence.

**Current Behavior**

Local discovery in `_load_local_runs` handles JUnit XML and Cucumber JSON. The configuration has no Allure glob, and the ingestion package has no Allure parser.

**Affected Components**

`src/testledger/ingest/`, `src/testledger/config.py`, and `src/testledger/cli.py` handle parsing, configuration, and local discovery. `src/testledger/models.py` defines the `TestRun` and `TestResult` records the parser must produce.

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**

TestLedger 0.1.0 at [baseline commit `83776f8`](https://github.com/surkuar/testledger/commit/83776f815ed5aa618b26a411331c461e65c25e44), on macOS arm64 with Python 3.12.1 and pytest 9.2.0. Set up an isolated environment with `python3 -m venv .venv` and `.venv/bin/python -m pip install -e '.[dev]'`.

**Steps to Reproduce**

1. Put two `*-result.json` fixtures in `reports/20261118-abcdef1-attempt1/allure-results/`. Use the same `historyId` and `fullName` in both. Set the first status to `failed` and the later status to `passed`.
2. Call `_load_local_runs(Config(), root)` with the directory containing `reports/` as `root`.
3. Observed two input files and zero imported runs. No fail-to-pass sequence reached the ledger.

**Reproduction Evidence**

- **Commit showing reproduction:** Fork commit pending. Reproduced against upstream `83776f8`.
- **Screenshots/logs:** `Input files: 2`, `Local runs: 0`, `Observed: []`. The unchanged full suite initially reported 46 passes and one failure in `test_custom_fix_pattern_replaces_default`. An immediate repeat reported 47 passes. The existing ingest suite separately passed all three tests. Ruff lint and format checks passed.
- **My findings:** The fixture reaches the existing local-discovery code path, which returned no runs for the Allure directory. This is the before result for checking the importer later.

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
