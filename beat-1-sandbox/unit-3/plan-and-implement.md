# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

ncrespo5

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-howard/issues/55#issuecomment-6976419244

I’ll start on #55 by tracing the five failing SkillExtractor fixtures to the language, database, and tool detectors. In my reproduction on macOS arm64 with Python 3.12.1 and pytest 8.3.5, running `python3 -m pytest tests/unit/test_skill_extractor.py --runxfail -q --tb=short` gave 5 failures and 13 passes on the original parser.

I suspect the detector patterns are missing some syntax or aliases. I’ll compare each fixture with what its detector actually checks, then update detection for CommonJS JavaScript, TypeScript declarations, PostgreSQL via `psycopg2`, and Dockerfile and Compose syntax. I’ll keep the extractor’s interface intact.

I’ll rerun the five cases with `--runxfail` and check that each returns the expected skill. Once they pass, I’ll remove the corresponding strict xfail markers and rerun the full SkillExtractor test file. I’ll also check that a Python-only import doesn’t get tagged as JavaScript.

---

## Your branch

**Branch**

`fix/55-skill-extractor-detection`

https://github.com/ncrespo5/pathreview-ai301-fa26-howard/tree/fix/55-skill-extractor-detection

Fix commit: `7a1c7f690bffa7e4cb3f187a10d4f9b25ebc98ca`

**Evidence**

On macOS arm64 with Python 3.12.1 and pytest 8.3.5, the original parser at `99673c7f53aa3c4666f99d38641a6ef0512a22e6` showed five expected failures. The same fixtures passed after applying the branch changes.

Before the fix:

```text
$ python3 -m pytest tests/unit/test_skill_extractor.py -q -rx
..x....xx..xx.....                                                       [100%]
=========================== short test summary info ============================
XFAIL tests/unit/test_skill_extractor.py::TestSkillExtractor::test_text_with_typescript_files - issue #55: skill extractor does not detect JavaScript/TypeScript
XFAIL tests/unit/test_skill_extractor.py::TestSkillExtractor::test_database_technology_detection - issue #55: skill extractor does not detect JavaScript/TypeScript
XFAIL tests/unit/test_skill_extractor.py::TestSkillExtractor::test_devops_tool_detection - issue #55: skill extractor does not detect JavaScript/TypeScript
XFAIL tests/unit/test_skill_extractor.py::TestSkillExtractor::test_javascript_detection - issue #55: skill extractor does not detect JavaScript/TypeScript
XFAIL tests/unit/test_skill_extractor.py::TestSkillExtractor::test_docker_compose_detection - issue #55: skill extractor does not detect JavaScript/TypeScript
13 passed, 5 xfailed in 0.02s

$ python3 -m pytest tests/unit/test_skill_extractor.py --runxfail -q --tb=short
..F....FF..FF.....                                                       [100%]
=================================== FAILURES ===================================
______________ TestSkillExtractor.test_text_with_typescript_files ______________
tests/unit/test_skill_extractor.py:65: in test_text_with_typescript_files
    assert any("typescript" in s.lower() for s in skill_names)
E   assert False
E    +  where False = any(<generator object TestSkillExtractor.test_text_with_typescript_files.<locals>.<genexpr> at 0x103e91d80>)
____________ TestSkillExtractor.test_database_technology_detection _____________
tests/unit/test_skill_extractor.py:146: in test_database_technology_detection
    assert any("postgres" in s.lower() or "sql" in s.lower() for s in skill_names)
E   assert False
E    +  where False = any(<generator object TestSkillExtractor.test_database_technology_detection.<locals>.<genexpr> at 0x103e93100>)
________________ TestSkillExtractor.test_devops_tool_detection _________________
tests/unit/test_skill_extractor.py:162: in test_devops_tool_detection
    assert any("docker" in s.lower() for s in skill_names)
E   assert False
E    +  where False = any(<generator object TestSkillExtractor.test_devops_tool_detection.<locals>.<genexpr> at 0x1047ec1e0>)
_________________ TestSkillExtractor.test_javascript_detection _________________
tests/unit/test_skill_extractor.py:195: in test_javascript_detection
    assert any("javascript" in s.lower() or "js" in s.lower() for s in skill_names)
E   assert False
E    +  where False = any(<generator object TestSkillExtractor.test_javascript_detection.<locals>.<genexpr> at 0x103e92cf0>)
_______________ TestSkillExtractor.test_docker_compose_detection _______________
tests/unit/test_skill_extractor.py:213: in test_docker_compose_detection
    assert any("docker" in s.lower() for s in skill_names)
E   assert False
E    +  where False = any(<generator object TestSkillExtractor.test_docker_compose_detection.<locals>.<genexpr> at 0x1047ee740>)
=========================== short test summary info ============================
FAILED tests/unit/test_skill_extractor.py::TestSkillExtractor::test_text_with_typescript_files
FAILED tests/unit/test_skill_extractor.py::TestSkillExtractor::test_database_technology_detection
FAILED tests/unit/test_skill_extractor.py::TestSkillExtractor::test_devops_tool_detection
FAILED tests/unit/test_skill_extractor.py::TestSkillExtractor::test_javascript_detection
FAILED tests/unit/test_skill_extractor.py::TestSkillExtractor::test_docker_compose_detection
5 failed, 13 passed in 0.03s
```

After applying the fix and removing the five strict xfail markers:

```text
$ python3 -m pytest tests/unit/test_skill_extractor.py --runxfail -q --tb=short
..................                                                       [100%]
18 passed in 0.02s

$ python3 -m pytest tests/unit/test_skill_extractor.py -q
..................                                                       [100%]
18 passed in 0.01s
```

The targeted language checks returned:

```text
Python-only imports: ['numpy', 'python']
Mixed CommonJS and TypeScript declarations: ['express', 'javascript', 'typescript']
```

The final live plan check returned `accept` with all seven required checks passing, including after the deviations entry was filled in. The test output above covers the focused parser suite and the targeted language checks. Full-repository checks are pending.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. `agreement: 18/20 scored items  (bar: 18/20: PASS)`

**Package analysis**

`pkg-06  scope-creep        reject  reject   yes`

Package `pkg-06` was `reject` in the run and in the gold labels. The repro showed an empty image archive and a swallowed export error. The proposed plan also wanted to “Introduce a unified image-operations abstraction” across three runtimes, bump containerd, and add a CI matrix. Those changes go beyond the single reproduced failure, and the repro did not establish the proposed root cause.

**Check rationale**

The **Bounded scope** check says:

> The plan covers one coherent, reviewable improvement. Necessary related edits are fine. Unrelated improvements, redesigned APIs without demonstrated need, and a broad rewrite when a local fix is viable fail.

A fix can need more than one file. The useful boundary is whether each edit addresses or verifies the same demonstrated problem. A dependency upgrade or API redesign needs its own evidence before it belongs in that plan.

**Trade-offs**

`pkg-14  clear-accept       accept  reject   NO     failed: Honest unknowns`

The `pkg-14` test plan gave a concrete way to verify the terminal reattach fix, and the gold label was `accept`. The rubric still rejected it because it treated “fresh attach (which performs the same queries behind the loading screen)” as an unverified claim about the cause. Requiring confident claims to match the repro catches overstatements, but it can hold back an otherwise actionable plan when the author could resolve the uncertainty by labeling it and adding a trace step.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
