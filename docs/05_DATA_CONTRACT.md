# Data Contract v0.1

Status: M1 draft
Scope: Python baseline / evaluation pipeline input and output data schema

---

## 1. Runtime PPG CSV Schema

Required columns:

| Column | Type | Unit | Required | Description |
|---|---|---:|---|---|
| `timestamp_ms` | integer or float | ms | yes | PPG sample timestamp. Must be monotonic non-decreasing. |
| `ppg` | float | normalized raw value | yes | Single-channel raw PPG, range expected 0–1. |
| `motion_flag` | integer | binary | yes | `0` = external static; `1` = external motion. Missing value is treated as motion / invalid. |

Recommended optional columns: `segment_id`, `subject_id` if anonymized, `note`.

Runtime assumptions:

- Sampling rate target: 50 Hz.
- Expected timestamp interval: 20 ms.
- Missing timestamp or missing motion flag must cause invalid handling.
- `motion_flag=1` causes runtime invalid for the corresponding sample / interval.

---

## 2. ECG RRI Reference CSV Schema

ECG RRI is used only for offline evaluation.

Required columns:

| Column | Type | Unit | Required | Description |
|---|---|---:|---|---|
| `r_timestamp_ms` | integer or float | ms | yes | ECG R peak timestamp for the current beat. |
| `rri_ms` | integer or float | ms | yes | ECG R-R interval ending at `r_timestamp_ms`, or between previous R and current R. |

Recommended optional columns: `prev_r_timestamp_ms`, `quality`, `segment_id`, `subject_id` if anonymized.

---

## 3. Algorithm Beat Output CSV Schema

Required columns:

| Column | Type | Unit | Description |
|---|---|---:|---|
| `output_timestamp_ms` | integer or float | ms | Time when output is emitted. May be later than `peak_timestamp_ms` because backfill is allowed. |
| `peak_timestamp_ms` | integer or float | ms | Actual timestamp of the confirmed current PPG main peak. |
| `prev_peak_timestamp_ms` | integer or float | ms | Actual timestamp of previous valid PPG main peak. |
| `ibi_ms` | integer or float | ms | PPG peak-to-peak interval. Empty if invalid. |
| `valid` | integer or bool | binary | `1/true` valid; `0/false` invalid. |
| `confidence` | float | 0–1 | Reliability score. |
| `sqi` | float | 0–1 | Signal quality score. |
| `state` | string | n/a | Algorithm state. |
| `invalid_reason` | string | n/a | Empty for valid outputs, enum for invalid outputs. |

---

## 4. Error Case CSV Schema

Required columns:

| Column | Type | Description |
|---|---|---|
| `file_id` | string | Input file id or path stem. |
| `ref_index` | integer | Reference ECG beat index. |
| `ref_timestamp_ms` | float | ECG R timestamp. |
| `ref_rri_ms` | float | Reference ECG RRI. |
| `matched_output_index` | integer | Matched PPG output index, empty if missed. |
| `ppg_peak_timestamp_ms` | float | Matched PPG peak timestamp. |
| `ppg_ibi_ms` | float | Matched PPG IBI. |
| `abs_error_ms` | float | Absolute error for matched valid IBI. |
| `match_status` | string | `matched`, `missed`, `false_positive`, `invalid`, `out_of_tolerance`. |
| `invalid_reason` | string | Invalid reason if applicable. |
| `state` | string | Algorithm state if available. |
| `confidence` | float | Confidence if available. |
| `sqi` | float | SQI if available. |

---

## 5. Synthetic Fixture Policy

M1 may add small synthetic fixture CSV files under `tests/fixtures/` for parser and evaluation smoke tests.

M1 must not commit real PPG / ECG human data unless Owner separately confirms repository visibility, anonymization, and allowed fields.
