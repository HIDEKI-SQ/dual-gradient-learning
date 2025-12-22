# Paper-D: Beyond Dual Flatness

**Curvature Emergence via Anisotropic Metric Perturbations**

## Overview

This directory contains the experimental code and results for Paper-D, which establishes a dichotomy framework characterizing when metric perturbations preserve or destroy dual flatness in information geometry. The key finding is that anisotropic point-dependent perturbations constitute the minimal mechanism for curvature emergence.

## Publication

- **Author**: HIDEKI (ORCID: [0009-0002-0019-6608](https://orcid.org/0009-0002-0019-6608))
- **Preprint DOI**: [To be added upon Zenodo publication]
- **Target Journal**: Information Geometry (Springer)

## Key Results

| Experiment | Perturbation Class | Pythagorean Residual ε |
|------------|-------------------|------------------------|
| **Gaussian (2D)** | Anisotropic | ε_max = 9.75 |
| **Gaussian (2D)** | Isotropic | ε = 0.0 (exact) |
| **Categorical (4-class)** | Anisotropic | ε_max = 0.435 |
| **Categorical (4-class)** | Isotropic | ε ≈ 10⁻¹¹ (machine precision) |

### Theoretical Contributions

1. **Dichotomy Theorem**: Isotropic perturbations preserve the Pythagorean theorem for all triples; anisotropic point-dependent perturbations violate it for all non-degenerate triples.

2. **Degenerate Conditions**: Complete characterization of ε = 0 cases (Appendix A.2):
   - Case 1: Δ_PQ = 0 (trivial projection)
   - Case 2: h_R = h_Q and Δ_PQ Δ_QR = 0 (equal modulation with orthogonality)
   - Case 3: h_R ≠ h_Q and Δ_PQ = −2h_R/(h_R − h_Q) · Δ_QR (compensating ratio)

3. **Explicit Curvature Formula** (Appendix B):
   - Connection perturbation: δΓ_ij,k = −2β (∂_k h) u_i u_j
   - Curvature tensor: R^k_lij = −4βγ u_l v^k (v_i u_j − v_j u_i) + O(β²)

## Notebook

| Notebook | Description | Paper Section |
|----------|-------------|---------------|
| `D_point_dependent_experiment.ipynb` | Dichotomy validation on Gaussian and Categorical manifolds | 5.1–5.4 |

## Results

```
results/
├── D_gaussian_point_dependent.{csv,pdf,png}      # Gaussian manifold data & figure
├── D_categorical_point_dependent.{csv,pdf,png}   # Categorical manifold data & figure
├── D_comparison_point_dependent.{pdf,png}        # Cross-distribution comparison figure
└── D_point_dependent_results.json                # Experiment metadata and summary
```

**File naming convention**:
- `*_point_dependent.{pdf,png}`: Publication-ready figures (Figure 1–3)
- `*_point_dependent.csv`: Raw experimental data
- `*_results.json`: Experiment metadata and summary statistics

## Experimental Configuration

### Perturbation Model

**Isotropic Perturbation (Definition 3.1)**:
```
D_iso(P, Q; λ) = (1 + λ) D(P ‖ Q)
```

**Anisotropic Point-Dependent Perturbation (Definition 3.2)**:
```
D_aniso(P, Q; β) = D(P ‖ Q) + β h(θ_Q) (u^T (θ_P − θ_Q))²
```
where h(θ) = 1 + γ(v^T θ)² with u ⊥ v.

### Experiment 1: 2D Gaussian Manifold

| Parameter | Value |
|-----------|-------|
| Manifold | Gaussian location family (Σ = I) |
| Dimension | n = 2 |
| Triple (P, Q, R) | P = (0, 1.5), Q = (0, 0), R = (2, 0) |
| Direction u | (1/√2, 1/√2) |
| Direction v | (1/√2, −1/√2) |
| β | 1.0 |
| γ | 0.5 |
| α | 0.5 |
| Magnitude range | \|w\| ∈ [0, 2] |

### Experiment 2: 4-Category Categorical Manifold

| Parameter | Value |
|-----------|-------|
| Manifold | Categorical distribution (K = 4) |
| Dimension | n = 3 (simplex interior) |
| Parameterization | Natural parameters θ_i = log p_i |
| Vertex Q | Uniform distribution (0.25, 0.25, 0.25, 0.25) |
| Direction u | (0.5, −0.5, 0.5, −0.5), satisfies u^T 1 = 0 |
| Direction v | (0.5, 0.5, −0.5, −0.5), satisfies v^T 1 = 0 |
| β | 0.5 |
| γ | 0.1 |
| α | 0.5 |
| Magnitude range | \|w\| ∈ [0, 1] |

### Gauge Invariance

For categorical manifolds with redundant parameterization (θ → θ + c·1), the gauge conditions u^T 1 = v^T 1 = 0 ensure well-definedness of the perturbation.

## Requirements

- Python 3.10+
- NumPy
- SciPy
- Matplotlib

Designed for Google Colab.

## Reproduction

### Quick Start
1. Open `D_point_dependent_experiment.ipynb` in Google Colab
2. Run cells sequentially
3. Results are saved to `results/` directory

### Deterministic Execution
All experiments use deterministic execution:
```python
np.random.seed(42)
```

### Expected Runtime
- **Total**: ~1–2 minutes

## Key Findings

### Dichotomy Theorem (Theorem 3.3)

The Pythagorean theorem is preserved if and only if the perturbation is isotropic:

| Perturbation Class | Pythagorean Residual |
|-------------------|---------------------|
| Isotropic | ε = 0 for all triples |
| Anisotropic point-dependent | ε > 0 for non-degenerate triples |

### Minimal Mechanism for Curvature

Neither directional selectivity alone nor point dependence alone suffices to break dual flatness. The **combination** of both features—directional selectivity (u_i u_j term) and point-dependent modulation (h(θ) with ∂_k h ≠ 0)—constitutes the minimal mechanism for curvature emergence.

### Machine-Precision Validation

- **Gaussian**: Isotropic perturbation maintains ε = 0.0 exactly
- **Categorical**: Isotropic perturbation maintains ε ≈ 5 × 10⁻¹¹ (machine precision in orthogonality construction)

## Citation

```bibtex
@misc{hideki2025dualflatness,
  author = {HIDEKI},
  title = {Beyond Dual Flatness: Curvature Emergence via Anisotropic Metric Perturbations},
  year = {2025},
  note = {Preprint},
  doi = {[To be added]}
}
```

## Scope and Limitations

**Validated setting**: 
- 2D Gaussian location family
- 4-category categorical distribution
- Specific modulation function h(θ) = 1 + γ(v^T θ)²

**Future work needed**:
- Higher-dimensional manifolds
- General C² modulation functions with non-vanishing gradient
- Non-exponential families
- Infinite-dimensional settings

See paper Section 6.4 for detailed discussion of limitations.

## License

MIT License

## Contact

For questions or issues, please open an issue on this repository or contact:
- HIDEKI: hideki@r3776.jp
- ORCID: [0009-0002-0019-6608](https://orcid.org/0009-0002-0019-6608)

## Acknowledgments

This research was conducted independently. The dichotomy framework builds on foundational work by Amari, Nagaoka, and the information geometry community.

---

**Last updated**: December 2025  
**Status**: Preprint preparation complete, pending Zenodo publication
