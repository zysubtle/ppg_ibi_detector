# Evaluation Protocol v0.1

Status: M1 draft
Scope: Offline evaluation for PPG peak-to-peak IBI against ECG RRI reference

---

## 1. Primary Metrics

### 1.1 IBI MAE

For all one-to-one matched valid PPG outputs within tolerance:

```text
IBI_MAE_ms = mean(abs(ppg_ibi_ms - ref_rri_ms))
```

Target:

```text
per-file IBI_MAE_ms < 60 ms
```

### 1.2 Coverage

Coverage denominator:

> ECG RRI beat count in the evaluable period.

Coverage numerator:

> Count of ECG RRI beats that are successfully matched one-to-one to a valid PPG IBI output within tolerance.

```text
coverage = matched_valid_count / evaluable_ecg_rri_count
```

Target:

```text
per-file coverage > 90%
```

---

## 2. Evaluable Period

A sample / interval is evaluable only when:

1. It belongs to a supported evaluation scenario;
2. `motion_flag=0` is present;
3. severe input failure is not explicitly marked;
4. ECG reference is valid.

Motion scenarios are excluded from first-release acceptance.

---

## 3. Matching Protocol

Use one-to-one ordered matching with ±100 ms tolerance.

Recommended M1/M2 implementation rule:

1. Sort ECG reference beats and PPG outputs by timestamp.
2. Consider only valid PPG outputs for primary MAE / coverage.
3. For each ECG RRI beat, find the next unmatched PPG output whose `peak_timestamp_ms` is within ±100 ms of the expected corresponding PPG beat timestamp policy.
4. Each PPG output can match at most one ECG beat.
5. Unmatched ECG beats count as missed.
6. Unmatched valid PPG outputs count as false positives.
7. Invalid PPG outputs are recorded but not counted as valid matches.

Open detail to finalize in M2:

- Whether matching should use ECG beat timestamp directly or an offset-tolerant ordered association. Since IBI is the primary target, the timestamp rule must be validated on real files.

---

## 4. Secondary Metrics

Recommended secondary metrics:

| Metric | Description |
|---|---|
| `rmse_ms` | Root mean squared IBI error. |
| `median_abs_error_ms` | Median absolute IBI error. |
| `p90_abs_error_ms` | 90th percentile absolute error. |
| `bias_ms` | Mean signed IBI error. |
| `valid_output_count` | Count of valid PPG IBI outputs. |
| `invalid_output_count` | Count of invalid PPG outputs. |
| `invalid_rate` | Invalid outputs / total outputs. |
| `missed_count` | ECG beats without matched valid PPG output. |
| `false_positive_count` | Valid PPG outputs not matched to ECG beat. |
| `out_of_tolerance_count` | Candidate matches outside tolerance. |

---

## 5. Per-file Summary CSV

Recommended columns:

```text
file_id,evaluable_ecg_rri_count,matched_valid_count,coverage,
ibi_mae_ms,ibi_rmse_ms,median_abs_error_ms,p90_abs_error_ms,bias_ms,
valid_output_count,invalid_output_count,invalid_rate,
missed_count,false_positive_count,out_of_tolerance_count,pass_mae,pass_coverage,pass_overall
```

---

## 6. Error-case CSV

See `docs/05_DATA_CONTRACT.md` for error-case field definitions.

---

## 7. Small Dataset Limitation

The current known dataset is 5 subjects / 5 files / 8 min each, sleep or rest.

Any result on this dataset is MVP validation only. It must not be described as generalized performance, medical-grade clinical validation, or population-level evidence.
