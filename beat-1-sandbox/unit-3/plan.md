# PathReview #55 implementation plan

## Diagnosis

The [posted reproduction](https://github.com/codepath/pathreview-ai301-fa26-howard/issues/55#issuecomment-6975445963) used the original parser at commit `99673c7f53aa3c4666f99d38641a6ef0512a22e6` on macOS arm64 with Python 3.12.1 and pytest 8.3.5. The five focused failures show that the extractor misses signals for TypeScript declarations, CommonJS JavaScript, PostgreSQL via `psycopg2`, Dockerfile instructions, and Compose services. I suspect the relevant detector patterns are missing or too narrow. I’ll trace which detector handles each fixture and compare its patterns with the input before editing it.

## Scope and implementation

1. Start with the five failing fixtures in `tests/unit/test_skill_extractor.py`. Trace them to `_detect_languages`, `_detect_databases`, and `_detect_tools` in `ingestion/parsers/skill_extractor.py`.
2. Update language detection to collect JavaScript and TypeScript signals independently. Cover CommonJS calls and TypeScript declarations alongside filename and import signals. Check that Python-only imports do not trigger JavaScript detection.
3. Add PostgreSQL recognition for postgres and psycopg aliases. Recognize Dockerfile and Compose syntax even if the input omits the word Docker.
4. Once the five cases pass with `--runxfail`, remove their strict xfail markers. Keep the public API, extraction categories, and confidence bounds intact.

## Verification

- Baseline: `python3 -m pytest tests/unit/test_skill_extractor.py --runxfail -q --tb=short` reported 5 failures and 13 passes on the original parser.
- After the detection changes: rerun the same command and check that the five fixtures return their expected skill and all 18 tests pass. After removing the markers, confirm that `python3 -m pytest tests/unit/test_skill_extractor.py -q` reports 18 passes.
- Check mixed JavaScript/TypeScript input and Python-only imports for false positives. Run the repository's `make check` and `make test-unit` before opening the PR, and report any checks I cannot complete.

## Deviations

The posted plan held. The branch updates the three detectors and removes the five strict xfail markers after verification. An earlier draft included typing cleanup, which was removed before the plan was posted to keep the fix focused on issue #55.
