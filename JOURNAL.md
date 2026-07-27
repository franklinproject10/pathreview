## Week 7 — Issue selection

**Issue link:** https://github.com/ascherj/pathreview/issues/109

**Issue title:** Test coverage for `core/services/review_service.py` is below 40%

**Tier:** [ ] Tier 1 [x] Tier 2 [ ] Tier 3

**Problem summary:**
The review service is the most critical orchestration layer in the application,
handling creation, retrieval, listing, and deletion of reviews. Despite its
importance, most of its code paths have no unit tests, leaving coverage below
40%. The fix requires writing pytest unit tests targeting the major execution
paths in `core/services/review_service.py` — including success cases, partial
failure, and full failure scenarios — until coverage meaningfully exceeds the
40% threshold.

**Branch name:** feat/109-review-service-test-coverage

**Setup confirmation:** [x] App runs locally at localhost:5173

**Cohort ledger:** [ ] Issue added to cohort ledger

**Is this right for me? — checklist reasoning:**

- Scope is contained to one file: `tests/unit/test_review_service.py`
- No linked PRs exist; issue is unclaimed
- Pytest + async mocking skills match prior work (Mixtape Bug Hunt)
- Estimated effort (5–7 hrs) fits the Week 7–8 timeline
- Read `core/services/review_service.py` locally to confirm the functions exist

## Week 8 — Reproduction & solution planning

**Reproduction commit link:**
https://github.com/franklinproject10/pathreview/commit/d4a5969

**Reproduction summary:**
Ran `pytest tests/unit/test_review_service.py -v` and observed 13 of 19 tests
failing with `AttributeError: 'coroutine' object has no attribute 'first'`.
The existing mocks used `AsyncMock` for the full result chain including
`.scalars()` and `.first()`, which are synchronous methods on an already-awaited
result. Running coverage confirmed the service was below 40%.

**PLAN.md link:**
https://github.com/franklinproject10/pathreview/blob/feat/109-review-service-test-coverage/PLAN.md

**Walkthrough video (recommended):** N/A

**Blockers or open questions:**
Pre-existing mypy errors in `core/services/review_service.py` block the
pre-commit hook — these are out of scope for this issue. Private helper
functions remain untested; coverage could be pushed to ~85%+ by adding
tests for `_run_ingestion_pipeline` and `_run_safety_checks` in Week 9.
