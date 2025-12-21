# Paper-E: Natural Gradient Empirical Validation

**Empirical Validation of Local Efficiency and Coordinate Invariance**

## Overview

This directory contains the experimental code and results for Paper-E, which provides systematic empirical validation of Natural Gradient's fundamental properties in softmax regression with exact Fisher matrices.

## Publication

- **Author**: HIDEKI (ORCID: [0009-0002-0019-6608](https://orcid.org/0009-0002-0019-6608))
- **Preprint DOI**: [To be added upon Zenodo publication]
- **Target Journal**: Journal of Machine Learning Research (JMLR)

## Key Results

| Experiment | Claim | Evidence |
|------------|-------|----------|
| **E1: Local Efficiency** | NG achieves 1.98% greater loss reduction per step | Consistent across 4 orders of magnitude (ε ∈ [10⁻⁵, 10⁻¹]) |
| **E2: KL Control** | Protocol precision ±0.34% | Gate B: 100% pass rate, mean KL ratio = 1.003 |
| **E2: Performance Parity** | Identical convergence under strict KL budgeting | Accuracy difference: 0.0006 (< 1 std dev) |
| **E3: Coordinate Invariance** | Machine-precision invariance (10⁻¹⁶ to 10⁻¹¹) | ~10⁹-fold better than SGD at κ=1000 |

## Notebooks

| Notebook | Description | Paper Section |
|----------|-------------|---------------|
| `E1_pareto_frontier_final.ipynb` | Local efficiency measurement | 3.3, 4.1 |
| `E2_kl_calibration_final.ipynb` | KL-controlled learning protocol | 3.4, 4.2 |
| `E3_invariance_test_final.ipynb` | Coordinate invariance validation | 3.5, 4.3 |

## Results

```
results/
├── E1_*.{pdf,png,csv,json}    # Pareto frontier data & figures
├── E2_*.{pdf,png,csv,pkl,json} # KL calibration data & figures
└── E3_*.{pdf,png,csv,json}    # Invariance test data & figures
```

**File naming convention**:
- `*_figure.{pdf,png}`: Publication-ready figures
- `*_results_*.csv`: Aggregated and raw experimental data
- `*_gate_validation.csv`: Quality control validation records
- `*_summary.json`: Experiment metadata and summary statistics

## Experimental Configuration

### Model and Data
| Parameter | Value |
|-----------|-------|
| Model | Softmax regression (no bias) |
| Parameters | 160 (10 classes × 16 features) |
| Data | Synthetic Gaussian mixtures |
| Training samples | N = 5,000 |
| Test samples | N = 1,000 |
| Feature dimension | D = 16 |
| Number of classes | C = 10 |

### Experiment 1: Pareto Frontier
| Parameter | Value |
|-----------|-------|
| Target KL values (ε) | {10⁻⁵, 3×10⁻⁵, ..., 10⁻¹} (9 values) |
| Random seeds | 10 |
| Methods | SGD, Natural Gradient |
| **Total trials** | **180** (9 × 10 × 2) |

### Experiment 2: KL-Controlled Learning
| Parameter | Value |
|-----------|-------|
| Target KL values (ε) | {10⁻⁴, 3×10⁻⁴, 10⁻³} |
| Training epochs | 100 |
| Random seeds | 5 |
| Methods | SGD, Natural Gradient |
| KL tolerance | ±20% |
| **Total runs** | **30** (3 × 5 × 2) |

### Experiment 3: Coordinate Invariance
| Parameter | Value |
|-----------|-------|
| Condition numbers (κ) | {1, 10, 100, 1000} |
| Random seeds | 3 |
| Methods | SGD, Natural Gradient |
| **Total trials** | **24** (4 × 3 × 2) |

### Gate Validation System
| Gate | Purpose | Pass Criterion |
|------|---------|----------------|
| **Gate A** | Fisher PSD quality | λ_min ≥ -10⁻⁸ × \|λ_max\| |
| **Gate B** | KL calibration | 0.8 ≤ D_KL/ε ≤ 1.2 |
| **Gate C** | Initial equivalence | max logit diff < 10⁻⁵ |

## Requirements

- Python 3.10+
- PyTorch 2.0+
- NumPy
- Matplotlib
- SciPy

Designed for Google Colab (A100 GPU recommended).

## Reproduction

### Quick Start
1. Open notebooks in Google Colab
2. Ensure GPU runtime (A100 recommended)
3. Run cells sequentially
4. Results are saved to `results/` directory

### Deterministic Execution
All experiments use deterministic execution with fixed random seeds:
```python
torch.manual_seed(seed)
np.random.seed(seed)
torch.backends.cudnn.deterministic = True
torch.backends.cudnn.benchmark = False
torch.set_default_dtype(torch.float64)
```

### Expected Runtime
- **E1**: ~5-10 minutes (180 single-step trials)
- **E2**: ~2-4 hours (30 runs × 100 epochs each)
- **E3**: ~5 minutes (24 trials)

## Key Findings

### Local Efficiency (E1)
Natural Gradient achieves **1.98% ± 0.04%** greater loss reduction per step compared to SGD when both methods induce identical KL divergence. This advantage is remarkably consistent across four orders of magnitude in step size (ε ∈ [10⁻⁵, 10⁻¹]).

### KL Control Protocol (E2)
The KL-controlled learning protocol achieves:
- **±0.34%** calibration precision (mean KL ratio = 1.003)
- **100%** Gate B pass rate across all epochs
- Performance parity under strict KL budgeting in linear models

### Coordinate Invariance (E3)
Natural Gradient exhibits **machine-precision invariance**:
- Deviations: 10⁻¹⁶ (κ=10) → 10⁻¹¹ (κ=1000)
- SGD degrades: 10⁻³ (κ=10) → 10⁻¹ (κ=1000)
- **~2 billion-fold** advantage at κ=1000

## Citation

```bibtex
@misc{hideki2025natgrad,
  author = {HIDEKI},
  title = {Natural Gradient Descent: Empirical Validation of Local Efficiency and Coordinate Invariance},
  year = {2025},
  note = {Preprint},
  doi = {[To be added]}
}
```

## Scope and Limitations

**Validated setting**: Softmax regression with exact analytic Fisher matrices (160 parameters)

**Future work needed**:
- Deep neural networks (MLPs, CNNs, Transformers)
- Approximate Fisher methods (K-FAC, empirical Fisher)
- Real datasets (MNIST, CIFAR, ImageNet)
- Large-scale models (10⁶-10⁹ parameters)

See paper Section 5.3 for detailed discussion of limitations.

## License

MIT License

## Contact

For questions or issues, please open an issue on this repository or contact:
- HIDEKI: hideki@r3776.jp
- ORCID: [0009-0002-0019-6608](https://orcid.org/0009-0002-0019-6608)

## Acknowledgments

This research was conducted independently. Thanks to the open-source community for PyTorch, NumPy, and related tools.

---

**Last updated**: December 2025  
**Status**: Preprint preparation complete, pending Zenodo publication
