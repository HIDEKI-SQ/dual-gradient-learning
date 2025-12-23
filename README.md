# Dual-Gradient Learning

This repository contains the experimental code and results for the **Dual-Gradient Learning Series**—a collection of six papers extending information geometry through value-perturbation theory and empirical validation.

## Author

**HIDEKI**  
Independent Researcher, Japan  
ORCID: [0009-0002-0019-6608](https://orcid.org/0009-0002-0019-6608)  
Contact: hideki@r3776.jp

## Papers

| Paper | Title | Preprint DOI |
|-------|-------|--------------|
| **A** | The Geometry of Dual-Gradient Learning: Phase Structure and the Misalignment Paradox under Label Noise | [10.5281/zenodo.17945912](https://doi.org/10.5281/zenodo.17945912) |
| **B-I** | The Sub-Additivity Principle: How Integration and Value Alignment Jointly Determine Cognitive Capacity | [10.5281/zenodo.17970754](https://doi.org/10.5281/zenodo.17970754) |
| **B-II** | Sub-additive Interaction between Integration and Value Alignment in Learning Systems: Evidence from 14,400 Simulations | [10.5281/zenodo.17940361](https://doi.org/10.5281/zenodo.17940361) |
| **C** | ρ-Design: Orthogonal Control of Gradient Direction and Mixing Strength in Learning Experiments | [10.5281/zenodo.17982236](https://doi.org/10.5281/zenodo.17982236) |
| **D** | Beyond Dual Flatness: Curvature Emergence via Anisotropic Metric Perturbations | [10.5281/zenodo.18027618](https://doi.org/10.5281/zenodo.18027618) |
| **E** | Natural Gradient Descent: Characterizing Local Efficiency and Coordinate Invariance in Controlled Settings | [10.5281/zenodo.18004827](https://doi.org/10.5281/zenodo.18004827) |

## Repository Structure

```
notebooks/
├── Paper-A/          # Dual-Gradient Learning (14,400+ runs)
│   ├── README.md
│   ├── *.ipynb       # Experimental notebooks
│   └── results/      # Outputs and figures
│
├── Paper-B/          # Sub-Additivity Principle (B-I theory + B-II evidence)
│   ├── README.md
│   ├── *.ipynb
│   └── results/
│
├── Paper-C/          # ρ-Design methodology (1,230 runs)
│   ├── README.md
│   ├── *.ipynb
│   └── results/
│
├── Paper-D/          # Curvature Emergence
│   ├── README.md
│   ├── *.ipynb
│   └── results/
│
└── Paper-E/          # Natural Gradient Validation (234 trials)
    ├── README.md
    ├── *.ipynb
    └── results/
```

## Key Contributions

### Theoretical Framework
- **Structure-Value-Meaning (SVM) Framework**: Meaning emerges through value-mediated projection of structure: M = Π_V(S)
- **Sub-Additivity Principle**: Integration and value alignment combine sub-additively (β₃ < 0)
- **Dichotomy Theorem**: Characterization of when metric perturbations preserve or destroy dual flatness

### Methodological Innovations
- **ρ-Design**: Protocol for orthogonal control of gradient direction (ρ) and mixing strength (λ)
- **Gate Validation System**: Quality assurance framework for Fisher matrix properties and KL calibration
- **KL-Controlled Learning**: Fair comparison protocol for optimization methods

### Empirical Findings
- Phase structure in dual-gradient learning with optimal λ ∈ [0.25, 0.40]
- Machine-precision coordinate invariance of Natural Gradient (10⁻¹⁶ to 10⁻¹¹)
- Curvature emergence requires both directional selectivity AND point dependence

## Experimental Scale

| Paper | Experimental Runs | Key Metrics |
|-------|-------------------|-------------|
| A | 14,400+ | Phase boundaries, 71% error reduction |
| B-II | 14,400 | β₃ = -0.311, f² = 0.37 |
| C | 1,230 | cos deviation < 3×10⁻⁸ |
| D | Gaussian + Categorical | ε_max = 9.75 (Gaussian), 0.435 (Categorical) |
| E | 234 | ~10⁹-fold invariance advantage |

## Requirements

- Python 3.10+
- PyTorch 2.0+
- NumPy, SciPy, Matplotlib

All notebooks are designed for **Google Colab** (A100 GPU recommended for Paper-A, B-II).

## Reproducibility

All experiments follow a **Deterministic Execution Contract**:

```python
torch.manual_seed(seed)
np.random.seed(seed)
torch.backends.cudnn.deterministic = True
torch.backends.cudnn.benchmark = False
torch.set_default_dtype(torch.float64)
```

Each Paper directory contains:
- Complete source notebooks
- Raw experimental data (CSV, JSON)
- Publication-ready figures (PDF, PNG)
- Detailed README with parameters

**Experimental Environment**: All experiments were conducted on Google Colab (December 2025).

## Citation

If you use this code or data, please cite the relevant paper(s):

```bibtex
@misc{hideki2025dualgradient,
  author = {HIDEKI},
  title = {The Geometry of Dual-Gradient Learning: Phase Structure and the Misalignment Paradox under Label Noise},
  year = {2025},
  doi = {10.5281/zenodo.17945912}
}

@misc{hideki2025subadditivity_theory,
  author = {HIDEKI},
  title = {The Sub-Additivity Principle: How Integration and Value Alignment Jointly Determine Cognitive Capacity},
  year = {2025},
  doi = {10.5281/zenodo.17970754}
}

@misc{hideki2025subadditivity_evidence,
  author = {HIDEKI},
  title = {Sub-additive Interaction between Integration and Value Alignment in Learning Systems: Evidence from 14,400 Simulations},
  year = {2025},
  doi = {10.5281/zenodo.17940361}
}

@misc{hideki2025rhodesign,
  author = {HIDEKI},
  title = {ρ-Design: Orthogonal Control of Gradient Direction and Mixing Strength in Learning Experiments},
  year = {2025},
  doi = {10.5281/zenodo.17982236}
}

@misc{hideki2025dualflatness,
  author = {HIDEKI},
  title = {Beyond Dual Flatness: Curvature Emergence via Anisotropic Metric Perturbations},
  year = {2025},
  doi = {10.5281/zenodo.18027618}
}

@misc{hideki2025natgrad,
  author = {HIDEKI},
  title = {Natural Gradient Descent: Characterizing Local Efficiency and Coordinate Invariance in Controlled Settings},
  year = {2025},
  doi = {10.5281/zenodo.18004827}
}
```

## License

MIT License

## Acknowledgments

This research was conducted independently. The theoretical framework builds on foundational work by Shun-ichi Amari and the information geometry community.

---

**Last updated**: December 2025
