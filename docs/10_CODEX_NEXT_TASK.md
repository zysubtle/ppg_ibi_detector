# M1 Codex Next Task: Project Foundation and Python Baseline / CLI Skeleton

Update mode for this file: **COMPLETE REPLACEMENT / 完全覆盖**

This file is the single authoritative executable task for Codex.

---

## 1. Current Stage / Milestone

Stage: **M1 — Project Foundation and Baseline Skeleton**

Owner has accepted:

1. Project Brief v0.2;
2. Algorithm Decision Cards D1–D7;
3. target branch `dev`;
4. work branches must be created from `dev`;
5. PR target branch must be `dev`;
6. Codex must not merge PRs.

---

## 2. Task Type

New Milestone task.

This task replaces any previous `docs/10_CODEX_NEXT_TASK.md` content.

---

## 3. Repository and Branch

Repository:

```text
https://github.com/zysubtle/ppg_ibi_detector
```

Base branch:

```text
dev
```

Create a new work branch from `dev`:

```text
feature/m1-project-foundation
```

PR target branch:

```text
dev
```

Do not code on `main` / `master`.
Do not push to `main` / `master`.
Do not merge the PR.

---

## 4. Objective

Create the M1 project foundation:

1. Put accepted project decisions into repo docs.
2. Add data contract, evaluation protocol, interface draft, milestone plan, PR review checklist, license/dependency policy, and test data policy.
3. Add a minimal Python package / CLI skeleton for later baseline development.
4. Add synthetic fixture data only.
5. Add smoke tests for CLI help, data parsing, and evaluation skeleton behavior.

M1 must **not** implement the MCU production algorithm and must **not** claim IBI performance.

---

## 5. Required Repository Documents

Create or update these files:

```text
docs/03_PROJECT_BRIEF_v0.2.md
docs/04_ALGORITHM_DECISION_CARDS.md
docs/05_DATA_CONTRACT.md
docs/06_EVALUATION_PROTOCOL.md
docs/07_INTERFACE_CONTRACT.md
docs/08_MILESTONE_PLAN.md
docs/09_PR_REVIEW_CHECKLIST.md
docs/10_CODEX_NEXT_TASK.md
docs/11_LICENSE_AND_DEPENDENCY_POLICY.md
docs/12_TEST_DATA_POLICY.md
```

The docs must reflect the accepted M0-B decisions:

- IBI = PPG main peak-to-main peak interval.
- Input = single-channel raw PPG, 50 Hz, range 0–1, timestamped, ambient-light removed.
- Motion flag = per-sample binary, synchronized; `1` = external motion; `0` = external static; missing = motion / invalid.
- Runtime output = beat-level IBI, valid/invalid, confidence, SQI, state, invalid_reason.
- Max output delay ≤ 2 s; backfill allowed with actual peak timestamp.
- Evaluation = ECG RRI reference, one-to-one ordered matching, ±100 ms tolerance, per-file IBI MAE and coverage.
- Target = per-file IBI MAE < 60 ms and coverage > 90% on evaluable periods.
- M1 does not submit real human data.
- M1 does not add third-party production dependencies.
- M1 does not copy third-party source code.
- MSPTDfast / ppg-beats is research-only and must not be copied or treated as globally MIT.
- Main algorithm direction is light hybrid, but implementation starts in later milestones.

If similarly named docs already exist, update them carefully without deleting useful existing repo-specific content unless it conflicts with accepted decisions.

---

## 6. Python Skeleton Scope

Inspect the repository first and preserve existing structure when possible.

If no Python package structure exists, create a minimal structure such as:

```text
src/ppg_ibi_detector/__init__.py
src/ppg_ibi_detector/cli.py
src/ppg_ibi_detector/io.py
src/ppg_ibi_detector/evaluation.py
src/ppg_ibi_detector/types.py
tests/test_cli.py
tests/test_io.py
tests/test_evaluation.py
tests/fixtures/synthetic_ppg_ibi_minimal.csv
tests/fixtures/synthetic_ecg_rri_minimal.csv
```

If the repo already uses another layout, adapt to the existing layout instead of duplicating.

The CLI should support at least:

```bash
python -m ppg_ibi_detector.cli --help
python -m ppg_ibi_detector.cli validate-data --ppg tests/fixtures/synthetic_ppg_ibi_minimal.csv --ecg tests/fixtures/synthetic_ecg_rri_minimal.csv
python -m ppg_ibi_detector.cli evaluate --ppg tests/fixtures/synthetic_ppg_ibi_minimal.csv --ecg tests/fixtures/synthetic_ecg_rri_minimal.csv --out <tmp_out_dir>
```

M1 CLI may implement only:

1. CSV schema validation;
2. synthetic-fixture smoke evaluation;
3. output folder creation;
4. placeholder summary/error CSV format.

M1 must not implement or claim the final peak detector.

If a placeholder detector is needed for tests, it must be explicitly named as synthetic/test-only or reference-passthrough and must not be described as algorithm performance.

---

## 7. Allowed Files to Modify

Allowed:

```text
README.md
pyproject.toml
setup.cfg
src/**
ppg_ibi_detector/**
tests/**
docs/03_PROJECT_BRIEF_v0.2.md
docs/04_ALGORITHM_DECISION_CARDS.md
docs/05_DATA_CONTRACT.md
docs/06_EVALUATION_PROTOCOL.md
docs/07_INTERFACE_CONTRACT.md
docs/08_MILESTONE_PLAN.md
docs/09_PR_REVIEW_CHECKLIST.md
docs/10_CODEX_NEXT_TASK.md
docs/11_LICENSE_AND_DEPENDENCY_POLICY.md
docs/12_TEST_DATA_POLICY.md
```

Only modify `README.md`, `pyproject.toml`, or packaging files if needed for the CLI/test skeleton.

---

## 8. Forbidden Changes

Do not modify unless explicitly required by a blocking repository-specific issue:

```text
docs/00_OAR_M_PROTOCOL.md
docs/01_DEEP_RESEARCH_PROTOCOL.md
docs/02_CODEX_GITHUB_RULES.md
```

Forbidden:

1. Do not code on `main` / `master`.
2. Do not push to `main` / `master`.
3. Do not merge PR.
4. Do not change Project Brief v0.2 decisions.
5. Do not change Decision Cards D1–D7.
6. Do not implement the final MCU algorithm in M1.
7. Do not implement the full hybrid peak detector in M1.
8. Do not claim algorithm accuracy or benchmark performance.
9. Do not add third-party production dependencies.
10. Do not copy or adapt third-party source code.
11. Do not add GPL or mixed-license code.
12. Do not commit real PPG / ECG human physiological data.
13. Do not commit secrets, credentials, tokens, personal data, or restricted data.
14. Do not alter accepted evaluation targets.
15. Do not silently skip tests.
16. Do not fabricate test, benchmark, PR, or GitHub results.

---

## 9. Fixture Rules

M1 may add only small synthetic fixture files.

Synthetic fixture rules:

1. No real human physiological signal.
2. Small enough for repository tests.
3. Clearly documented as synthetic.
4. Used only for parser, CLI, and evaluation smoke tests.
5. Fixture test results must not be described as real performance.

Recommended synthetic PPG columns:

```text
timestamp_ms,ppg,motion_flag
```

Recommended synthetic ECG columns:

```text
r_timestamp_ms,rri_ms
```

---

## 10. Implementation Steps

1. Confirm current branch and repository remotes.
2. Checkout `dev` and pull latest changes.
3. Create branch `feature/m1-project-foundation` from `dev`.
4. Inspect existing repository layout.
5. Add or update M1 docs listed above.
6. Add minimal Python CLI/package skeleton if absent.
7. Add synthetic fixtures.
8. Add smoke tests using only the standard library where possible.
9. Run required tests.
10. Commit with message:

```text
M1: add project foundation and baseline skeleton
```

11. Push work branch.
12. Create PR targeting `dev`.
13. Fill PR description using the required template below.

---

## 11. Required Test Commands

Run these commands if the repository environment supports them:

```bash
python -m unittest discover -s tests
python -m ppg_ibi_detector.cli --help
python -m ppg_ibi_detector.cli validate-data --ppg tests/fixtures/synthetic_ppg_ibi_minimal.csv --ecg tests/fixtures/synthetic_ecg_rri_minimal.csv
python -m ppg_ibi_detector.cli evaluate --ppg tests/fixtures/synthetic_ppg_ibi_minimal.csv --ecg tests/fixtures/synthetic_ecg_rri_minimal.csv --out /tmp/ppg_ibi_m1_eval
```

If the package is under `src/`, ensure the test command can import it by using editable install if appropriate:

```bash
python -m pip install -e .
```

Do not add new runtime dependencies just to make tests pass.

If any command cannot be run, report why.

---

## 12. PR Description Requirements

PR description must contain:

```markdown
## Summary

## Changed Files

## Task Source
- `docs/10_CODEX_NEXT_TASK.md`
- Update mode: COMPLETE REPLACEMENT / 完全覆盖
- Current task: M1 Project Foundation and Baseline Skeleton

## Algorithm Logic Change
- Yes / No
- Explanation:

## Interface / IO Contract Change
- Yes / No
- Explanation:

## Dependency Change
- Yes / No
- Explanation:

## Data Format Change
- Yes / No
- Explanation:

## Test Protocol Change
- Yes / No
- Explanation:

## Test Commands and Results

## Tests Not Run and Reasons

## Data / Privacy Check
- Real human physiological data committed: Yes / No
- Fixture type: synthetic / anonymized / none
- Explanation:

## License / Third-party Source Check
- Third-party source copied: Yes / No
- New production dependency added: Yes / No
- Explanation:

## Known Risks

## Suggested Reviewer Focus

## Out-of-scope Items
```

---

## 13. Completion Report Requirements

After execution, report:

1. Branch name;
2. Commit hash;
3. PR URL;
4. Files changed;
5. Whether `docs/10_CODEX_NEXT_TASK.md` was fully replaced;
6. Whether tests were run and exact outputs;
7. Whether any tests were not run and why;
8. Whether any real data was committed;
9. Whether any third-party source or dependency was introduced;
10. Known risks and recommended reviewer focus.

Do not claim PR creation, push, or test success unless actually completed.

---

## 14. Known Risks for Reviewer

1. M1 is a foundation milestone; it must not be judged as an algorithm-performance PR.
2. Synthetic fixture results are smoke tests only.
3. Matching protocol semantics may need refinement in M2 after real file inspection.
4. `invalid_reason` enum may expand later, but M1 should stabilize initial names.
5. Real human data submission remains blocked until Owner separately confirms anonymization and repository visibility.
6. No third-party source copy is allowed.
7. If existing repo layout differs from this task, Codex should adapt minimally and report differences.

---

## 15. Out-of-scope for M1

1. Full PPG peak detector.
2. Hybrid ERMA + SQI + tracker implementation.
3. MSPTDfast / ppg-beats benchmark execution.
4. C99 MCU runtime implementation.
5. nRF54L15 integration.
6. Real dataset evaluation.
7. Parameter tuning.
8. Claims of MAE / coverage performance.
