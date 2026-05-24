# PR Review Checklist v0.1

Use this checklist for every PR.

---

## 1. Scope

- [ ] PR target branch is `dev`.
- [ ] Work branch was created from `dev`.
- [ ] PR does not target `main` / `master`.
- [ ] PR does not merge itself.
- [ ] Changes match `docs/10_CODEX_NEXT_TASK.md`.
- [ ] No scope expansion beyond current Milestone.

---

## 2. Protocol Compliance

- [ ] `docs/00_OAR_M_PROTOCOL.md` not modified unless explicitly authorized.
- [ ] `docs/01_DEEP_RESEARCH_PROTOCOL.md` not modified unless explicitly authorized.
- [ ] `docs/02_CODEX_GITHUB_RULES.md` not modified unless explicitly authorized.
- [ ] Codex task file was the single executable task source.
- [ ] PR description reports task source and test results.

---

## 3. Algorithm / Interface / Data Contract

- [ ] Algorithm logic change declared.
- [ ] Interface / IO contract change declared.
- [ ] Data format change declared.
- [ ] Test protocol change declared.
- [ ] No unapproved change to accepted Project Brief or Decision Cards.

---

## 4. Dependency / License

- [ ] No new production dependency unless explicitly authorized.
- [ ] No third-party source copied unless explicitly authorized.
- [ ] Any benchmark-only tool is marked research-only.
- [ ] GPL or mixed-license risks are not introduced into production implementation.

---

## 5. Data Safety

- [ ] No secrets.
- [ ] No credentials.
- [ ] No unapproved original human physiological data.
- [ ] Synthetic fixture or approved anonymized fixture only.
- [ ] Fixture results are not overstated as real dataset performance.

---

## 6. Tests

- [ ] Required tests were run.
- [ ] Failures are reported honestly.
- [ ] Tests not run have explicit reasons.
- [ ] Smoke tests cover CLI help and data validation.
