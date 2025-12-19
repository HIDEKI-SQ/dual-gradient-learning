# Paper-A: Dual-Gradient Learning

**The Geometry of Dual-Gradient Learning: Phase Structure and the Misalignment Paradox under Label Noise**

## Overview

This directory contains the experimental code and results for Paper-A, which introduces **dual-gradient learning**—a framework for robust training under label noise that operates in gradient space by mixing structure gradients (from noisy labels) and value gradients (from trusted signals).

## Publication

- **Author**: HIDEKI (ORCID: [0009-0002-0019-6608](https://orcid.org/0009-0002-0019-6608))
- **Preprint DOI**: [10.5281/zenodo.17945912](https://doi.org/10.5281/zenodo.17945912) 
- **Target Journal**: Neural Computation

## Key Results

| Finding | Evidence |
|---------|----------|
| Phase structure in λ | Optimal region 0.25–0.40, collapse beyond 0.45 |
| 40% noise improvement | CE 38.4% → Aligned 11.2% (71% reduction) |
| 80% noise improvement | CE 62.3% → Aligned 22.0% (65% reduction) |
| Misalignment paradox | Random/Anti-label improve at low λ (cos ≈ 0) |
| True anti-alignment degrades | TrueAnti (cos ≈ −0.77) reliably worsens performance |
| Non-Oracle effectiveness | 1% clean samples → 60% error reduction |
| Critical noise threshold | ~65–70% noise rate |

## Notebooks

| Notebook | Description | Paper Section |
|----------|-------------|---------------|
| `exp_A_fixed.ipynb` | λ high-resolution scan | 3 (Phase Structure) |
| `exp_B_fixed.ipynb` | Misaligned: random labels | 4 (Misalignment Paradox) |
| `exp_B2_anti_aligned.ipynb` | Misaligned: (y+1) mod 10 | 4 (Misalignment Paradox) |
| `exp_B3_ablation.ipynb` | Ablation: TrueAnti, Renorm, K | 5 (Ablation) |
| `exp_C_fixed.ipynb` | Method comparison (CE, Aligned, Loss-mix) | 3 (Phenomena) |
| `exp_D1_fixed.ipynb` | Non-Oracle: clean ratio scan | 6 (Non-Oracle) |
| `exp_D2_fixed.ipynb` | Non-Oracle: 80% noise | 6 (Non-Oracle) |
| `exp_D3_noise_scan.ipynb` | Critical noise rate identification | 6 (Non-Oracle) |
| `exp_G_fixed.ipynb` | Asymmetric noise | 7 (Robustness) |

## Results
```
results/
├── exp_A_fixed/           # λ scan (40%, 80% noise)
├── exp_B_fixed/           # Random label experiments
├── exp_B2_anti_aligned/   # Anti-label (y+1) mod 10
├── exp_B3_ablation/       # Ablation study (TrueAnti, Renorm, K)
├── exp_C_fixed/           # Method comparison
├── exp_D1_fixed/          # Non-Oracle clean ratio
├── exp_D2_fixed/          # Non-Oracle 80% noise
├── exp_D3_noise_scan/     # Noise rate threshold
└── exp_G_fixed/           # Asymmetric noise
```

## Experimental Configuration

| Parameter | Value |
|-----------|-------|
| Dataset | CIFAR-10 (50,000 train / 10,000 test) |
| Model | ResNet-18 (11M parameters) |
| Training | SGD (momentum 0.9, weight decay 5×10⁻⁴) |
| Learning rate | 0.1, decayed ×0.1 at epochs 50, 75 |
| Epochs | 100 |
| Batch size | 256 |
| Label noise | 40%, 80% symmetric; 20%, 40% asymmetric |
| λ values | {0.1, 0.15, 0.2, 0.25, 0.3, 0.35, 0.4, 0.45, 0.5} |
| Cache K | 16 |
| Seeds | 3–5 per condition |
| **Total runs** | **350+** |

## Requirements

- Python 3.8+
- PyTorch
- torchvision
- NumPy
- Matplotlib

Designed for Google Colab (A100 GPU recommended).

## Reproduction

1. Open notebooks in Google Colab
2. Mount Google Drive or adjust save paths
3. Run cells sequentially
4. Results are saved to `results/` directory

## Citation
```bibtex
@misc{hideki2025dualgradient,
  author = {HIDEKI},
  title = {The Geometry of Dual-Gradient Learning: Phase Structure and the Misalignment Paradox under Label Noise},
  year = {2025},
  doi = {10.5281/zenodo.17945912},
  note = {Preprint}
}
```

## License

MIT License
