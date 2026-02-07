# README v4.1 (Final, Confirmed)

This document is the **confirmed and internally consistent specification** of all experiments
corresponding to the released raw data ZIP archives.
It supersedes README v4 and earlier drafts.

---

## 1. Definition of a Run

**Run** is defined as:

> One complete training-and-evaluation execution that produces a single
> `(ordered_error, collapse_error)` (or equivalent) pair **for a fixed configuration**:
> dataset × model × seed × primary intervention setting.

### Notes on compound experiments
- In **compound experiments** (e.g. W2, Tδ2), multiple *training sessions* or *trials*
  may occur internally.
- Only **distinct experimental conditions plus their explicit control/baseline states**
  are counted as *runs* in the census below.
- Internal multiplicities (e.g. multiple branches or intermediate probes) are reported
  descriptively but **not added** to the run total.

This definition matches exactly how runs are represented in the released ZIP data.

---

## 2. Released Data Scope

The following ZIP archives constitute the **entire released raw dataset**:

- Paper-A_AtoQ.zip
- Paper-A_RtoW.zip
- Paper-A_X.zip
- Paper-A_Y.zip

All run counts below are derived directly from these files.

---

## 3. Run Census (Confirmed)

| Series | Description | Runs |
|------|------------|------|
| A–Q | Vision (original) | **1,773** |
| R–W | Vision (extended) | **1,273** |
| X | NLP (discovery) | **790** |
| Y | NLP (controls) | **80** |
| **Total** |  | **3,916** |

---

## 4. Vision: A–Q (Original)

Counts and internal breakdown exactly match the raw data.
No archived or excluded runs are included.

**Total: 1,773 runs**

---

## 5. Vision: R–W (Extended)

**Total: 1,273 runs**

### Compound experiments (clarification)

- **W2**
  - Internal training sessions: 3 seeds × 3 λ × 2 branches = 18 sessions
  - Counted runs: 9 intervention conditions + 3 baseline controls = **12 runs**

- **Tδ1 / Tδ2**
  - Tδ1: 10 characterization runs
  - Tδ2: 6 interventions × 3 seeds = 18 runs
  - Baseline traps: 3 runs
  - **Total counted runs: 31**

### Naming consistency
Folders in the released data use `Tg1/Tg2`; these correspond to the
conceptual experiments referred to as `Tγ1/Tγ2` in the text.
They are **not double-counted**.

---

## 6. NLP: X Series (Discovery)

The X series reflects **exactly the configurations present in the released data**.
Earlier drafts referenced additional protocols or durations that are **not included**.

| Subseries | Runs |
|---------|------|
| X1 | 120 |
| X1b | 120 |
| X1c | 120 |
| X1d | 120 |
| X2 | 200 |
| X3_fast | 10 |
| X3_slow | 10 |
| X4 | 90 |
| **Total** | **790** |

Notes:
- All X1 variants use **20 seeds**.
- X2 uses a **single protocol**.
- X4 uses a **single duration**.
- Boundary and summary tables correctly use `n = 20`.

---

## 7. NLP: Y Series (Controls)

**Total: 80 runs**

| Subseries | Runs |
|---------|------|
| Y1A | 20 |
| Y1B | 20 |
| Y2k3 | 20 |
| Y2k10 | 20 |

The reported **time effect (+25.6 pp)** between Y1A and Y1B
matches the raw data averages.

---

## 8. Numerical Conventions

- Reported standard deviations and variances use **population definitions**
  (`ddof = 0`) unless explicitly stated otherwise.
- All tables in the manuscript are reproducible directly from the released data.

---

## 9. Status

This README v4.1 is the **final, confirmed version**.
All numbers are consistent with the released raw data
and are intended to be cited as authoritative.

