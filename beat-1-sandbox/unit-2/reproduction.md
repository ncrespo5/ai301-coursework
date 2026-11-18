# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

`ncrespo5`

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-howard/issues/55#issuecomment-6975436766

Hi! I’d like to work on #55 for my CodePath sandbox assignment. The baseline run reproduced all five SkillExtractor failures listed in the issue. I’ll share the reproduction details in a follow-up and use those cases to verify the fix.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-howard/issues/55#issuecomment-6975445963

### Reproduced on the original parser

**Environment:** macOS arm64, Python 3.12.1, and pytest 8.3.5. The source, tests, and test configuration were taken from commit `99673c7f53aa3c4666f99d38641a6ef0512a22e6`. The parser was unmodified for both runs.

To reproduce, check out that commit, install pytest 8.3.5 in your Python environment, and run these commands from the repository root:

```bash
python3 -m pytest tests/unit/test_skill_extractor.py -q -rx
python3 -m pytest tests/unit/test_skill_extractor.py --runxfail -q --tb=short
```

The first command reported **13 passed, 5 xfailed**. With `--runxfail`, the same five assertions failed:

```text
FAILED tests/unit/test_skill_extractor.py::TestSkillExtractor::test_text_with_typescript_files
FAILED tests/unit/test_skill_extractor.py::TestSkillExtractor::test_database_technology_detection
FAILED tests/unit/test_skill_extractor.py::TestSkillExtractor::test_devops_tool_detection
FAILED tests/unit/test_skill_extractor.py::TestSkillExtractor::test_javascript_detection
FAILED tests/unit/test_skill_extractor.py::TestSkillExtractor::test_docker_compose_detection
5 failed, 13 passed
```

The tests expected the extractor to detect TypeScript from an exported interface, JavaScript from a CommonJS `require(...)` call, PostgreSQL from a `psycopg2` import, and Docker from Dockerfile instructions or a Compose service. Each test failed because the expected skill was absent.

This run covered the SkillExtractor test file. I’ll rerun these five cases against the fix and share the results.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

**Package analysis**

[Pick one scored package (`pkg-01` through `pkg-20` — the four `calib-` packages are never
scored). Name it by id, say what your rubric decided and what the gold label said, and
explain why your rubric read it that way.]

**Check rationale**

[Quote one check from the `rubric.md` you uploaded to `tools/repro-check/`, exactly as it reads now.
Then say why it reads that way — what you revised to get there, or what you rejected in
favour of it.]

**Trade-offs**

[Every check gives something up. Any one of these is a complete answer: a package whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
