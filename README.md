# Dual-Gradient Learning

This repository contains experimental code, data, and figures for the **Dual-Gradient Learning** research program.
The central result is a regime-structured view of robust learning under label noise, formalized and empirically validated
in **Paper A**, with extensions across vision and NLP.

The repository is organized to support **full numerical reproducibility** of all reported results, figures, and statistics.

---

## Author

**HIDEKI**  
Independent Researcher, Japan  
ORCID: [0009-0002-0019-6608](https://orcid.org/0009-0002-0019-6608)  
Contact: **hideki@r3776.jp**

---

## Papers

| ID | Title | Status / DOI |
|----|-------|--------------|
| **A** | **Designing Robust Learning as Phase Control: Identical Training Produces Stable Success or Irreversible Failure** | DOI to be assigned |
| **B‑I** | The Sub‑Additivity Principle: How Integration and Value Alignment Jointly Determine Cognitive Capacity | https://doi.org/10.5281/zenodo.17970754 |
| **B‑II** | Sub‑additive Interaction between Integration and Value Alignment in Learning Systems: Evidence from 14,400 Simulations | https://doi.org/10.5281/zenodo.17940361 |
| **C** | ρ‑Design: Orthogonal Control of Gradient Direction and Mixing Strength in Learning Experiments | https://doi.org/10.5281/zenodo.17982236 |
| **D** | Beyond Dual Flatness: Curvature Emergence via Anisotropic Metric Perturbations | https://doi.org/10.5281/zenodo.18027618 |
| **E** | Natural Gradient Descent: Characterizing Local Efficiency and Coordinate Invariance in Controlled Settings | https://doi.org/10.5281/zenodo.18163401 |

---

## Repository Structure

```
.
├── notebooks/
│   ├── Paper-A/
│   │   ├── README.md            # Detailed experimental ledger (v4.1)
│   │   ├── notebooks/           # Training / analysis notebooks
│   │   ├── results/             # CSV / JSON summaries
│   │   └── figures/
│   │       ├── main/             # Figure 1–5 (paper)
│   │       └── extended_data/    # Extended Data Fig. 1–8
│   │
│   ├── Paper-B/
│   ├── Paper-C/
│   ├── Paper-D/
│   └── Paper-E/
│
└── README.md  (this file)
```

---

## Paper A at a Glance

**Problem**  
Robust learning under label noise is typically assumed to degrade smoothly as noise increases.

**Core Finding**  
Dual‑gradient learning exhibits **regime structure**:
identical training conditions can produce either stable low‑error solutions or persistent high‑error failures.

**Key phenomena**
- Sharp boundary and variance peak as a function of mixing coefficient λ
- Bimodality, hysteresis, and metastability in vision
- Absorbing high‑error failure states at high noise
- Cross‑domain validation in NLP with domain‑specific phenomenology
- Causal decomposition of non‑recovery into **time‑driven corrosion** and **path‑dependent damage**

This motivates reframing robust learning as **phase control** rather than loss optimization.

---

## Experimental Scale (Paper A)

| Domain | Series | Runs |
|-------|--------|-----:|
| Vision | A–Q | 1,773 |
| Vision | R–W | 1,273 |
| NLP | X | 790 |
| NLP (controls) | Y | 80 |
| **Total** | | **3,916** |

All run counts are derived from released data archives and exclude archived or failed runs.
The complete census and definitions are documented in `notebooks/Paper-A/README.md` (v4.1).

---

## Reproducibility

This repository constitutes the **complete reproducibility package** for Paper A.

All numerical values and figures in the manuscript can be regenerated from:
- raw data (CSV / JSON),
- analysis notebooks, and
- fixed experimental protocols documented in Paper‑A/README.md.

**Deterministic Execution Contract**
```python
torch.manual_seed(seed)
np.random.seed(seed)
torch.backends.cudnn.deterministic = True
torch.backends.cudnn.benchmark = False
torch.set_default_dtype(torch.float64)
```

All experiments were executed on **Google Colab (A100 GPU)**.

---

## License

MIT License

---

## Acknowledgments

This research was conducted independently.
The theoretical foundations build on information geometry and related work by Shun‑ichi Amari and collaborators.

---

**Last updated**: March 2026
