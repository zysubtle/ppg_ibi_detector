# Milestone Plan v0.1

Status: M1 draft

---

## M1：Project Foundation and Baseline Skeleton

Goal:

- Put Project Brief v0.2 and Decision Cards into repo docs.
- Define data contract, evaluation protocol, interface draft, license/data policy.
- Create Python baseline / CLI skeleton.
- Add synthetic fixture and smoke tests.

Not in scope:

- No MCU C implementation.
- No production algorithm.
- No real human data commit.
- No third-party source copy.

---

## M2：Python Baseline A

Goal:

- Implement simple interpretable baseline: bandpass / smoothing, adaptive threshold, refractory period, local maxima, basic invalid rules, evaluation CLI.
- Run per-file evaluation if Owner provides approved data.

---

## M3：Python Hybrid Prototype

Goal:

- Implement accepted hybrid research route: ERMA-style candidate generation, upslope / derivative-assisted peak localization, pulse-wise SQI, template / morphology consistency, interval tracking, ≤2 s backfill.

---

## M4：C99 Streaming Core

Goal:

- Translate verified Python semantics into C99 streaming core.
- Static buffers only.
- No dynamic memory.
- No production dependencies.

---

## M5：Python/C Consistency Verification

Goal:

- Run identical synthetic and selected approved fixtures through Python and C.
- Compare outputs and error cases.

---

## M6：MCU Porting Preparation

Goal:

- nRF54L15 / Keil integration plan.
- RAM / Flash static budget.
- Cycle / latency profiling plan.

---

## M7：Error-case Analysis and Parameter Convergence

Goal:

- Analyze false positives, misses, invalid reasons.
- Tune thresholds under MAE / coverage tradeoff.

---

## M8：Acceptance Report and Risk Review

Goal:

- Summarize final results.
- Distinguish MVP validation from generalized claims.
- Prepare risk review and out-of-scope list.
