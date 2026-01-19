# Paper-A: Dual-Gradient Learning

**Phase Transitions in Gradient-Mixed Learning: Path Dependence and Metastability under Label Noise**

## Overview

This repository contains experimental code and results for Paper-A, which introduces **dual-gradient learning**—a framework for robust training under label noise that operates in gradient space by mixing structure gradients (from noisy labels) and value gradients (from trusted signals).

## Publication

- **Author**: HIDEKI (ORCID: [0009-0002-0019-6608](https://orcid.org/0009-0002-0019-6608))
- **Preprint DOI**: TBD
- **Code & Data DOI**: TBD
- **Repository**: [https://github.com/HIDEKI-SQ/dual-gradient-learning/](https://github.com/HIDEKI-SQ/dual-gradient-learning/)

## Terminology

To maintain consistency across different noise rates and conditions:

| Term | Definition | Notes |
|------|------------|-------|
| **Low-error branch (L-branch)** | The better-performing branch at a given λ | η=0.4: ≲15% error; η=0.8: ~45% error |
| **High-error branch (H-branch)** | The worse-performing branch at a given λ | Typically 40–70% error |
| **Trap state (T-state)** | Extreme high-error state at ~90% (chance-level) | Characterized in Tδ1/Tδ2 |
| **Gap** | Δ = mean(e_H − e_L) at the same λ | Primary metric for bistability |

## Key Results

| Finding | Evidence |
|---------|----------|
| Phase structure in λ | Optimal region 0.25–0.40, collapse beyond 0.45 |
| Critical point | λ_c ≈ 0.46–0.50 with variance peak and critical slowing down |
| Hysteresis gap | 22–71% between L-branch and H-branch (speed-dependent) |
| Metastability | 100% survival in L-branch at λ=0.54 for 300 epochs |
| Trap state (T-state) | All escape interventions failed from 90% error state |
| Causal intervention | 67% performance control via gradient geometry |
| Dataset universality | CIFAR-100: Gap 40.6% |
| Architecture universality | ResNet34: Gap 53.5% |
| High noise robustness | η=0.8: Gap 44.6% |

## Experimental Summary

**Total runs: ~3,000** (1,750+ original + 1,200+ extended experiments)

### Original Experiments (exp_A–Q): 1,750+ runs

| Experiment | Runs | Purpose | Key Findings |
|------------|-----:|---------|--------------|
| **exp_A** | ~50 | λ high-resolution scan | Optimal region 0.25–0.40, collapse >0.45 |
| **exp_B, B2, B3** | ~100 | Misalignment paradox | Random/Anti-label improve at low λ |
| **exp_C** | ~30 | Method comparison | CE vs Aligned vs Loss-mix |
| **exp_D1, D2, D3** | ~80 | Non-Oracle | 1% clean → 60% improvement |
| **exp_G** | ~30 | Asymmetric noise | Robustness confirmed |
| **exp_I** | 63 | Cosine intervention (K=1) | Direct cos θ manipulation |
| **exp_J** | 39 | Mechanism decomposition | Direction dominates |
| **exp_K** | 60 | Learning dynamics | Critical slowing: 51→76 epochs |
| **exp_L** | 63 | Causal intervention (K=16) | 79% performance control |
| **exp_M1, M2, M3** | 297 | λ sweep (fine) | Variance peak, bimodality |
| **exp_N1, N2** | 140 | Phase diagram | 2D (λ × η) mapping |
| **exp_O** | 70 | CIFAR-100 | Dataset universality |
| **exp_P, P2** | 108 | Architecture | ResNet18/34, VGG11, SimpleCNN |
| **exp_Q1** | 305 | Finite-size scaling | Width dependence |
| **exp_Q2** | 60 | Hysteresis | Path dependence confirmed |
| **exp_Q3, Q4** | 181 | LR-λ interaction | Temporal dynamics |

### Extended Experiments (exp_R–W): 1,200+ runs

| Series | Runs | Purpose | Key Findings |
|--------|-----:|---------|--------------|
| **R1–R3** | 120 | Hysteresis loops | Gap +44.7% @ λ=0.22, kinetic lag effect |
| **S1–S2** | 902 | Bimodality/Coexistence | λ_c ≈ 0.48–0.50, phase boundary mapping |
| **T1, T13** | 100 | Lifetime (metastability) | **100% survival** at λ=0.54 for 300 epochs |
| **Tα, Tβ** | 28 | Speed dependence | Gap 22–71% (speed-dependent) |
| **Tγ1, Tγ2** | 10 | Asymmetry | L-branch robust, H-branch partial recovery |
| **Tδ1, Tδ2** | 13 | 90% Trap | **All escape attempts failed** |
| **V1** | 3 | Asymmetric noise | Gap 46.3% |
| **V2** | 12 | Trusted subset | 1–10% clean ratio |
| **V3_v3** | 3 | ResNet34 | Gap 53.5% |
| **V4** | 3 | CIFAR-100 | Gap 40.6% |
| **W1** | 6 | Gradient geometry | c_sv orthogonality in L-branch |
| **W2** | 3 | Causal intervention | Gap 67% after 30 epochs |

## Critical Phenomena Evidence

### 1. Hysteresis (R1, Tα, Tβ)

| λ | H-branch (λ↑) | L-branch (λ↓) | Gap |
|---|----------:|------------:|----:|
| 0.22 | 58.6% | 13.9% | **+44.7%** |
| 0.30 | 45.5% | 14.9% | +30.6% |
| 0.40 | 47.3% | 17.4% | +30.0% |
| 0.50 | 52.7% | 32.2% | +20.5% |

**Speed dependence (Tβ)**: Gap increases from 22% (3 ep/λ) to **71%** (10 ep/λ)

### 2. Spinodal Points (R3)

| Condition | λ↑ (H-branch collapse) | λ↓ (L-branch recovery) | Coexistence Width |
|-----------|------------------------|------------------------|-------------------|
| η=0.4, short | 0.556 ± 0.052 | 0.200 | 0.356 |
| η=0.4, long | 0.674 ± 0.022 | 0.200 | 0.474 |
| η=0.8 | 0.440 ± 0.000 | 0.200 | 0.240 |

**Key finding**: Kinetic lag effect at η=0.4 (λ↑ shifts from 0.56 to 0.67 with longer hold)

### 3. Phase Boundary (S1)

| λ | n | L-count | H-count | Classification |
|---|--:|--------:|--------:|----------------|
| 0.42 | 50 | 50 | 0 | Pure L-branch |
| 0.46 | 50 | 50 | 0 | L-branch |
| 0.48 | 50 | 30 | 0 | **Transition** |
| 0.50 | 50 | 1 | 3 | **Transition** |
| 0.52 | 50 | 0 | 28 | H-branch dominant |
| 0.56 | 50 | 0 | 44 | Pure H-branch |

### 4. Metastability (T1a, T13)

| Experiment | λ | Epochs | Survived | Final Error |
|------------|---|-------:|---------:|------------:|
| **T1a** | 0.46 | 150 | **50/50 (100%)** | 10.8% ± 3.5% |
| **T13** | 0.54 | 300 | **50/50 (100%)** | 10.4% ± 3.5% |

**Key finding**: L-branch survives even in "collapse region" (λ=0.54) for 300 epochs

### 5. 90% Trap (Tδ1, Tδ2)

| Intervention | λ | LR mult | Escaped |
|--------------|---|--------:|--------:|
| baseline | 0.60 | 0.01 | 0/3 |
| lambda_zero | 0.00 | 0.01 | 0/3 |
| lambda_low | 0.20 | 0.01 | 0/3 |
| lr_boost | 0.60 | 0.10 | 0/3 |
| lr_boost_high | 0.60 | 1.00 | 0/3 |
| combined | 0.00 | 0.10 | 0/3 |

**Key finding**: 90% trap is extremely robust—no intervention could escape

### 6. Universality

| Experiment | Condition | Gap @ λ=0.50 |
|------------|-----------|-------------:|
| V1 | Asymmetric noise | **46.3%** |
| V3_v3 | ResNet34 | **53.5%** |
| V4 | CIFAR-100 | **40.6%** |
| Tβ2_v3 | η=0.8 | **44.6%** |

### 7. Causal Intervention (W2)

| Target λ | L-branch | H-branch | Gap |
|----------|--------:|---------:|----:|
| 0.40 | 12.6% | 79.8% | **67.2%** |
| 0.50 | 12.6% | 79.0% | **66.3%** |
| 0.55 | 12.9% | 77.3% | **64.4%** |

## Results Directory Structure

```
results/
├── exp_A–G/                    # Original experiments (350+ runs)
├── exp_I–Q/                    # Extended experiments (1,403 runs)
├── exp_R1_hysteresis_loop/     # Hysteresis loops η=0.4
├── exp_R2_hysteresis_loop/     # Hysteresis loops η=0.8
├── exp_R3_spinodal/            # Spinodal estimation
├── exp_S1_coexistence_map/     # Phase boundary mapping
├── exp_S2_deep_bimodality/     # Large-n bimodality
├── exp_T1_lifetime_ordered/    # Metastability (T1a, T13)
├── exp_Tα_*/                   # Hysteresis sweep
├── exp_Tβ_*/                   # Speed dependence
├── exp_Tγ_*/                   # Asymmetry (recovery/collapse bounds)
├── exp_Tδ_*/                   # 90% trap analysis
├── exp_V1_asymmetric_noise/    # Noise type universality
├── exp_V2_trusted_subset/      # Trusted ratio sweep
├── exp_V3_resnet34_v3/         # Architecture universality
├── exp_V4_cifar100/            # Dataset universality
├── exp_W1_geometry/            # Gradient geometry analysis
├── exp_W2_causal_intervention/ # Causal intervention
└── archive/                    # Failed/superseded experiments
    ├── exp_Tb2_eta08_20260118_040949/      # v1, interrupted
    ├── exp_Tb2_eta08_v2_20260118_124918/   # v2, empty (superseded by v3)
    ├── exp_V3_vgg11_20260118_095347/       # VGG11 v1, failed
    ├── exp_V3_vgg11_v2_20260118_124820/    # VGG11 v2, empty
    └── notebooks/                          # Unused/superseded notebooks
        ├── nb_Tb2_eta08.ipynb              # v1
        ├── nb_Tb2_eta08_v2.ipynb           # v2
        ├── nb_V3_vgg11.ipynb               # VGG11 v1
        ├── nb_V3_vgg11_v2.ipynb            # VGG11 v2
        └── nb_T1*_lifetime_*.ipynb         # Planned but skipped (T1a/T13 sufficient)
```

### Archive Notes

- **Tb2 v1/v2**: Threshold-based detection failed at η=0.8; v3 uses branch existence check
- **V3 VGG11**: Architecture sensitivity issue; switched to ResNet34 for v3
- **T11/T12/T14 notebooks**: Skipped because T1a (λ=0.46) and T13 (λ=0.54) showed 100% survival, making intermediate λ experiments unnecessary

## Experimental Configuration

### Base Configuration

| Parameter | Value |
|-----------|-------|
| Dataset | CIFAR-10 (50,000 train / 10,000 test) |
| Model | ResNet-18 (11M parameters) |
| Training | SGD (momentum 0.9, weight decay 5×10⁻⁴) |
| Learning rate | 0.1, decayed ×0.1 at epochs 50, 75 |
| Epochs | 100 |
| Batch size | 256 |
| Label noise | 40%, 80% symmetric; 20%, 40% asymmetric |
| λ values | {0.1, 0.15, 0.2, 0.25, 0.3, 0.35, 0.4, 0.45, 0.5, ...} |
| Cache K | 16 (default), 1 (for fresh gradient experiments) |
| Seeds | 3–50 per condition |

### Extended Experiments Configuration

| Experiment | Special Parameters |
|------------|-------------------|
| R1/R2 | Sweep: λ = 0.20 → 0.65 → 0.20, hold = 1 or 5 epochs |
| R3 | Spinodal detection with threshold |
| S1 | λ ∈ {0.42, 0.44, 0.46, 0.48, 0.50, 0.52, 0.54, 0.56}, n=50 each |
| S2 | λ = 0.50, n = 60–102 per sub-experiment |
| T1a | λ = 0.46, 150 epochs, 50 seeds |
| T13 | λ = 0.54, 300 epochs, 50 seeds |
| Tβ | Speed: 1, 3, 10 epochs per λ step |
| V3_v3 | Architecture: ResNet34 |
| V4 | Dataset: CIFAR-100 |

## Statistical Mechanics Interpretation

### Two Deep Potential Wells

| State | Characteristics | Stability | Escape Difficulty |
|-------|-----------------|-----------|-------------------|
| **L-branch** | Low error (10–15% at η=0.4), c_sv ≈ 0 | **Extremely stable** | No collapse even at λ=0.90 |
| **T-state** | Error at 90% (chance-level), c_sv ≈ 0.95 | **Extremely stable** | All interventions failed |

### First-Order-Like Transition Evidence

| Evidence | Experiment | Result |
|----------|------------|--------|
| **Hysteresis** | R1, Tα | Gap 22–71% between L-branch and H-branch |
| **Bimodality** | S1, S2 | Phase coexistence at λ ≈ 0.48–0.50 |
| **Metastability** | T1a, T13 | 100% L-branch survival for 300 epochs |
| **Asymmetry** | Tγ1, Tγ2 | L→H difficult, H→L partial |
| **Critical slowing** | exp_K | 51→76 epochs at λ=0.47 |

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
@misc{hideki2026dualgradient,
  author = {HIDEKI},
  title = {Phase Transitions in Gradient-Mixed Learning: Path Dependence and Metastability under Label Noise},
  year = {2026},
  note = {Preprint, DOI to be assigned}
}
```

## License

MIT License
