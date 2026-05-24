# Interface Contract Draft v0.1

Status: M1 draft
Scope: Conceptual interface for future Python and C99 implementations

---

## 1. Python CLI Concept

M1 should create a Python CLI skeleton, not a production algorithm.

Suggested commands:

```bash
python -m ppg_ibi_detector.cli --help
python -m ppg_ibi_detector.cli validate-data --ppg <ppg.csv> --ecg <ecg.csv>
python -m ppg_ibi_detector.cli evaluate --ppg <ppg.csv> --ecg <ecg.csv> --out <out_dir>
```

M1 may implement parser validation and synthetic-fixture smoke evaluation.

M1 must not claim algorithm performance.

---

## 2. Future Python Module Boundary

Suggested modules:

```text
ppg_ibi_detector/
  __init__.py
  cli.py
  io.py
  eval.py
  baseline_stub.py
  types.py
```

M1 may create these files as skeletons.

M2 should implement real baseline A.

---

## 3. Future C99 API Concept

C implementation is not in M1 scope. The following is a draft boundary only.

Suggested future API concepts:

```c
typedef struct {
    float ppg;
    uint32_t timestamp_ms;
    uint8_t motion_flag;
    uint8_t motion_flag_valid;
} ppg_ibi_sample_t;

typedef struct {
    uint8_t valid;
    float ibi_ms;
    uint32_t peak_timestamp_ms;
    uint32_t prev_peak_timestamp_ms;
    float confidence;
    float sqi;
    uint8_t state;
    uint8_t invalid_reason;
} ppg_ibi_output_t;
```

Future C99 requirements:

- no dynamic memory;
- caller-provided or static workspace;
- no large stack arrays;
- deterministic state machine;
- optional debug disabled by default.

---

## 4. State Enum Draft

```text
INIT
ACQUIRE
TRACK
LOW_QUALITY
MOTION_INVALID
REACQUIRE
INVALID
```

---

## 5. Invalid Reason Enum Draft

```text
startup
motion_flag
motion_flag_missing
dropout
timestamp_gap
saturation
gain_jump
low_sqi
no_peak_candidate
unstable_interval
wear_loose_or_contact_loss
out_of_range_ibi
internal_state_not_ready
```
