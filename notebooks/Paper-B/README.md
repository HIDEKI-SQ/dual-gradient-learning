# Paper-B: Sub-Additivity Principle

**How Integration and Value Alignment Jointly Determine Cognitive Capacity**

## Overview

This directory contains the theoretical framework and computational evidence for Paper-B, which proposes the **Sub-Additivity Principle**—a general composition rule stating that integration (*I*) and value alignment (*A*) combine sub-additively, yielding diminishing returns when both factors are already high.

Paper-B consists of two complementary articles:
- **B-I (Theory)**: Theoretical framework for Psychological Review
- **B-II (Evidence)**: Computational demonstration with 14,400 simulations

## Publications

| Paper | Title | Target Journal | DOI |
|-------|-------|----------------|-----|
| **B-I** | The Sub-Additivity Principle: How Integration and Value Alignment Jointly Determine Cognitive Capacity | Psychological Review | [10.5281/zenodo.17970754](https://doi.org/10.5281/zenodo.17970754) |
| **B-II** | Sub-additive interaction between integration and value alignment in learning systems: Evidence from 14,400 simulations | Neural Computation | [10.5281/zenodo.17940361](https://doi.org/10.5281/zenodo.17940361) |

- **Author**: HIDEKI (ORCID: [0009-0002-0019-6608](https://orcid.org/0009-0002-0019-6608))

## Key Results

| Finding | Evidence |
|---------|----------|
| Negative interaction (β₃ < 0) | β₃ = −0.311, f² = 0.37 (large effect) |
| Integration main effect | β₁ = +0.664 |
| Value alignment main effect | β₂ = +0.289 |
| Survives boundary correction | β₃ = −0.140 after logit transformation |
| Concave capacity-performance | Power-law exponent b = 0.148 ≪ 1 |
| Weaker Factor First | Marginal effects largest for weaker factor |

## Core Predictions (P1–P6)

| ID | Prediction | Falsification Condition |
|----|------------|------------------------|
| P1 | β₁ > 0, β₂ > 0, β₃ < 0 | β₃ ≈ 0 or β₃ > 0 |
| P2 | Weaker factor yields larger marginal gain | Uniform marginal effects |
| P3 | A-effect shrinks at high I | A-effect constant across I |
| P4 | I-effect shrinks at high A | I-effect constant across A |
| P5 | Concave capacity-performance (b < 1) | Linear fit better |
| P6 | β₃ < 0 survives logit/d'/log-RT | β₃ → 0 after correction |

## Notebooks

| Notebook | Description | Paper Section |
|----------|-------------|---------------|
| `T_A3_v6_1_stratified_regression.ipynb` | Main experiment & stratified regression analysis | B-II Section 4–5 |

## Results
```
results/
├── figures/
│   ├── fig2-1_trilogy_structure.png      # Trilogy structure diagram
│   ├── fig3-1_rho_design.png             # ρ-design illustration
│   ├── fig3-2_factor_independence.png    # Factor independence demonstration
│   ├── fig4-1_task_structure.png         # Task structure
│   ├── fig4-2_architecture.png           # Model architecture
│   ├── fig4-3_experimental_design.png    # Experimental design matrix
│   ├── fig6-1_saturation_curve.png       # Saturation/capacity curve
│   ├── fig6-2_marginal_effects.png       # Marginal effects visualization
│   └── fig7-1_future_directions.png      # Future directions
├── T-A3_v6.1_results_FINAL.csv           # Final results (14,400 runs)
├── T-A3_v6.1_rho_curves.png              # ρ curves visualization
├── T-A3_v6.1_stratified_betas.png        # Stratified β coefficients
├── T-A3_v6.1_stratified_regression.csv   # Stratified regression output
├── T-A3_v6.1_summary.png                 # Summary visualization
└── checkpoint_*.csv                       # Checkpoints (2000–14000 runs)
```

## Experimental Configuration (B-II)

| Parameter | Value |
|-----------|-------|
| Task | Two-view disambiguation (10-class) |
| Model | MLP with modulable cross-connections |
| Integration manipulation | Architecture (modular vs. integrated) |
| Integration measure | I_JS (lesion-based Jensen-Shannon divergence) |
| Value alignment manipulation | ρ-design (direction × magnitude) |
| ρ values | {−1.0, −0.5, 0.0, +0.5, +1.0} |
| λ values | {0.0, 0.25, 0.5, 0.75, 1.0} |
| Seeds | 10 per condition |
| **Total runs** | **14,400** |

## Theoretical Framework (B-I)

### Three Complementary Formalizations

1. **Negative interaction**: β₃ < 0 (defining signature)
2. **Diminishing marginal effects**: ∂²P/∂I∂A < 0
3. **Multiplicative capacity with concave mapping**: C = I × A, P = f(C), f″(C) < 0

### Repositioned Theories

| Theory | I Emphasis | A Emphasis | Interaction Specified? |
|--------|------------|------------|----------------------|
| IIT | High | Low | No |
| Global Workspace | High | Moderate | No |
| Reinforcement Learning | Low-Moderate | High | No |
| Attention/Control | Moderate | High | No |
| Working Memory | Moderate | Moderate | No |
| **This Paper** | **Explicit** | **Explicit** | **Yes: β₃ < 0** |

## Requirements

- Python 3.8+
- PyTorch
- NumPy
- SciPy
- Matplotlib

Designed for Google Colab (A100 GPU).

## Reproduction

1. Open `T_A3_v6_1_stratified_regression.ipynb` in Google Colab
2. Run cells sequentially
3. Results are saved to `results/` directory
4. Checkpoints saved at 2000, 4000, 6000, 8000, 10000, 12000, 14000 runs

## Citation
```bibtex
@misc{hideki2025subadditivity_theory,
  author = {HIDEKI},
  title = {The Sub-Additivity Principle: How Integration and Value Alignment Jointly Determine Cognitive Capacity},
  year = {2025},
  doi = {10.5281/zenodo.17970754},
  note = {Preprint, Target: Psychological Review}
}

@misc{hideki2025subadditivity_evidence,
  author = {HIDEKI},
  title = {Sub-additive interaction between integration and value alignment in learning systems: Evidence from 14,400 simulations},
  year = {2025},
  doi = {10.5281/zenodo.17940361},
  note = {Preprint, Target: Neural Computation}
}
```

## Related Work

- **Paper-A** ([Dual-Gradient Learning](../Paper-A/)): Phase structure and misalignment paradox under label noise
- **Paper-C** ([ρ-Design](../Paper-C/)): Methodological foundation for orthogonal control of gradient direction and mixing strength

## License

MIT License
