# Test Data Policy v0.1

Status: M1 draft

---

## 1. Current Data Understanding

Owner has stated that the known dataset contains:

- 5 subjects;
- 5 files;
- 8 min per file;
- sleep / rest scenes;
- complete files may be submitted.

However, these files contain physiological signals, so M1 must still treat them as sensitive until repository visibility and anonymization are confirmed.

---

## 2. M1 Rule

M1 must not commit real human PPG / ECG data.

M1 may commit only:

1. synthetic fixture data;
2. minimal parser fixture with no human signal;
3. documentation examples.

---

## 3. Before Real Data Commit

Owner must explicitly confirm:

1. repository visibility: public or private;
2. data anonymization status;
3. no names;
4. no device IDs unless anonymized;
5. no personal subject IDs unless anonymized;
6. no location or sensitive timestamps unless allowed;
7. whether complete files or only small fixtures may enter the repo.

---

## 4. Reporting Boundary

Results on synthetic fixtures must be described only as smoke-test results.

Results on 5 files may be described only as MVP / small dataset validation.

Do not describe results as generalized, population-level, clinical, or medical-grade validation.
