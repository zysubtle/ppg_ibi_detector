# License and Dependency Policy v0.1

Status: M1 draft

---

## 1. Core Rule

Production code must remain self-contained and must not introduce third-party production dependencies unless Owner explicitly approves.

---

## 2. Four Categories

| Category | Allowed in M1? | Notes |
|---|---:|---|
| Read papers / docs | yes | Must cite source in docs when used. |
| Use third-party tools for offline benchmark | no by default in M1 | Allowed only if task explicitly says so. |
| Add third-party production dependency | no | Requires Owner approval. |
| Copy / adapt third-party source | no | Requires Owner approval and license review. |

---

## 3. Known Tool Boundaries

| Tool / Library | Boundary |
|---|---|
| NeuroKit2 | Research reference / possible offline benchmark only; not production dependency. |
| HeartPy | Research reference / possible offline benchmark only; not production dependency. |
| ppg-beats / MSPTDfast | Research-only; mixed license per-file; do not copy source; do not treat as globally MIT. |
| pyPPG | Research reference only unless license is reviewed. |
| scipy / numpy / pandas | Python research / offline only; not MCU production. |

---

## 4. PR Reporting

Every PR that mentions third-party material must state:

1. whether third-party source was copied;
2. whether a dependency was added;
3. whether usage is research-only or production;
4. known license.
