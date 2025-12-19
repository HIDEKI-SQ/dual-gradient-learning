# Paper-C: ρ-Design

**Orthogonal Control of Gradient Direction and Mixing Strength in Learning Experiments**

## Overview

This directory contains the experimental code and results for Paper-C, which introduces **ρ-design**—a protocol for disentangling gradient direction and mixing strength in gradient-based learning experiments.

## Publication

- **Author**: HIDEKI (ORCID: [0009-0002-0019-6608](https://orcid.org/0009-0002-0019-6608))
- **Preprint DOI**: https://doi.org/10.5281/zenodo.17982236
- **Target Journal**: Journal of Machine Learning Research (JMLR)

## Key Results

| Claim | Evidence |
|-------|----------|
| Alignment guarantee cos = ρ | Max deviation 2.58 × 10⁻⁸ |
| Factor separation | Distinct axes in accuracy surface |
| Naïve measure confounding | A_naive varies with λ at fixed ρ |

## Notebooks

| Notebook | Description | Paper Section |
|----------|-------------|---------------|
| `paper_C_calibration_v4.ipynb` | Task difficulty calibration | 4.1.2 |
| `paper_C_E3_production.ipynb` | Main experiment (1,050 runs) | 4.2.1, 4.2.2 |
| `paper_C_A_naive.ipynb` | A_naive confounding demonstration (180 runs) | 4.2.3 |

## Results

```
results/
├── calibration_v4/     # Calibration outputs
├── E3_production/      # Main experiment (cos verification + learning performance)
└── E3_A_naive/         # A_naive confounding data
```

## Experimental Configuration

| Parameter | Value |
|-----------|-------|
| Task | 10-class classification, 16-dim input |
| Model | MLP: 16→64→64→10 |
| Training | SGD (momentum 0.9), lr=0.1, 100 epochs |
| Label noise | {0%, 30%, 50%} |
| ρ values | {−0.7, −0.4, −0.2, 0.0, +0.4, +0.7, +1.0} |
| λ values | {0.0, 0.25, 0.5, 0.75, 1.0} |
| Seeds | 10 (main) + 3 (A_naive) |
| **Total runs** | **1,230** |

## Requirements

- Python 3.8+
- PyTorch
- NumPy
- Matplotlib

Designed for Google Colab (A100 GPU).

## Reproduction

1. Open notebooks in Google Colab
2. Run cells sequentially
3. Results are saved to `results/` directory

## Citation

```bibtex
@misc{hideki2025rhodesign,
  author = {HIDEKI},
  title = {ρ-Design: Orthogonal Control of Gradient Direction and Mixing Strength in Learning Experiments},
  year = {2025},
  note = {Preprint}
}
```

## License

MIT License
