# Paper-A: Dual-Gradient Learning

**The Geometry of Dual-Gradient Learning: Phase Structure and the Misalignment Paradox under Label Noise**

## Overview

This directory contains the experimental code and results for Paper-A, which introduces **dual-gradient learning**—a framework for robust training under label noise that operates in gradient space by mixing structure gradients (from noisy labels) and value gradients (from trusted signals).

## Publication

- **Author**: HIDEKI (ORCID: [0009-0002-0019-6608](https://orcid.org/0009-0002-0019-6608))
- **Preprint DOI**: [10.5281/zenodo.17945912](https://doi.org/10.5281/zenodo.17945912)
- **Code & Data DOI**: [10.5281/zenodo.18030355](https://doi.org/10.5281/zenodo.18030355)
- **Repository**: [https://github.com/HIDEKI-SQ/dual-gradient-learning/](https://github.com/HIDEKI-SQ/dual-gradient-learning/)

## Key Results

| Finding | Evidence |
|---------|----------|
| Phase structure in λ | Optimal region 0.25–0.40, collapse beyond 0.45 |
| Critical point | λ_c ≈ 0.46–0.48 with variance peak and critical slowing down |
| 40% noise improvement | CE 38.4% → Aligned 11.2% (71% reduction) |
| 80% noise improvement | CE 62.3% → Aligned 22.0% (65% reduction) |
| Misalignment paradox | Random/Anti-label improve at low λ (cos ≈ 0) |
| True anti-alignment degrades | TrueAnti (cos ≈ −0.77) reliably worsens performance |
| Causal intervention | cos(g_value, g_clean) manipulation: 79% performance control |
| Non-Oracle effectiveness | 1% clean samples → 60% error reduction |
| Critical noise threshold | ~65–70% noise rate |
| Dataset universality | CIFAR-100 preserves phase structure |
| Architecture universality | ResNet18/34, VGG11, SimpleCNN preserve phase structure |
| Hysteresis | Path-dependent behavior observed |

## Experimental Summary

**Total runs: 1,750+** (350+ original + 1,403 extended experiments)

### Original Experiments (exp_A–G): 350+ runs

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

### Extended Experiments (exp_I–Q): 1,403 runs

| Experiment | Runs | Purpose | Key Findings |
|------------|-----:|---------|--------------|
| **exp_I** | 63 | Cosine intervention (K=1) | Direct cos θ manipulation affects performance |
| **exp_J** | 39 | Mechanism decomposition | Direction dominates; implicit LR effect is small |
| **exp_K** | 60 | Learning dynamics | **Critical slowing down**: convergence 51→76 epochs at λ=0.47 |
| **exp_L** | 63 | Causal intervention (K=16) | **79% performance control** via cos manipulation (22.6%→11.5%) |
| **exp_M1** | 132 | Coarse λ sweep | Phase structure overview across η={0.4, 0.8} |
| **exp_M2** | 70 | Fine sweep η=0.4 | **Critical point λ_c ≈ 0.46–0.48**, variance peak, bimodal distribution |
| **exp_M3** | 70 | Fine sweep η=0.8 | Critical region characterization at high noise |
| **exp_M3b** | 25 | Low λ supplement η=0.8 | Additional coverage for 80% noise |
| **exp_N1** | 70 | Phase diagram (low noise) | 2D phase diagram for η={0.2, 0.4} |
| **exp_N2** | 70 | Phase diagram (high noise) | 2D phase diagram for η={0.6, 0.8} |
| **exp_O** | 70 | CIFAR-100 universality | **Same phase structure** on 100-class dataset |
| **exp_P** | 72 | Architecture universality | ResNet18/34/VGG11/SimpleCNN (lr=0.1) |
| **exp_P2** | 36 | Architecture (lr=0.01) | VGG11/SimpleCNN stabilized with lower lr |
| **exp_Q1** | 305 | Finite-size scaling | Width dependence of critical point |
| **exp_Q2** | 60 | Hysteresis | **Path dependence**: ordered→collapse preserves; collapse→ordered fails |
| **exp_Q3** | 151 | LR-λ interaction | Learning rate modulates critical boundary |
| **exp_Q4** | 30 | Cosine temporal evolution | Detailed cos θ dynamics across training |

## Critical Phenomena Evidence

### 1. Critical Slowing Down (exp_K)

| λ | Region | Convergence Epoch |
|---|--------|------------------:|
| 0.30 | Ordered | 51 |
| 0.35 | Ordered | 51 |
| 0.43 | Critical | 51 |
| 0.45 | Critical | 52–57 |
| **0.47** | **Critical** | **58–76** |
| 0.55 | Collapse | — (no convergence) |

### 2. Variance Peak (exp_M2, η=0.4)

| λ | Mean Error | Std |
|---|----------:|----:|
| 0.38 | 11.3% | 0.3% |
| 0.44 | 13.2% | 0.4% |
| 0.46 | 15.5% | **2.2%** |
| 0.48 | 22.3% | **4.0%** |
| 0.50 | 30.4% | **8.0%** |

### 3. Causal Intervention (exp_L)

| cos(g_value, g_clean) | Test Error | Interpretation |
|----------------------:|----------:|----------------|
| −0.9 | 22.6% | Anti-aligned → degradation |
| 0.0 | 29.8% | Orthogonal → regularization |
| +0.9 | 11.5% | Aligned → optimal |

**Performance range: 79% controllable by gradient geometry alone**

### 4. Hysteresis (exp_Q2)

| Schedule | η=0.4 Error | Interpretation |
|----------|------------:|----------------|
| fixed_ordered (λ=0.35) | ~11% | Stable ordered phase |
| fixed_collapse (λ=0.6) | 10–90% | Unstable collapse phase |
| **quench_to_collapse** (0.35→0.6) | ~13% | **Ordered training protects against collapse** |
| **quench_to_ordered** (0.6→0.35) | 10–90% | **Recovery from collapse is difficult** |

## Universality Evidence

### Dataset Universality (exp_O: CIFAR-100)

| Noise Rate | Optimal λ | Collapse λ | Phase Structure |
|------------|-----------|------------|-----------------|
| 40% | 0.30 | >0.50 | ✅ Preserved |
| 80% | 0.35 | >0.50 | ✅ Preserved |

### Architecture Universality (exp_P, P2)

| Model | Optimal λ | Collapse λ | Notes |
|-------|-----------|------------|-------|
| ResNet18 | 0.35 | >0.50 | Reference |
| ResNet34 | 0.35 | >0.50 | ✅ Preserved |
| VGG11 (lr=0.01) | 0.35–0.45 | >0.55 | ✅ Preserved (lr-sensitive) |
| SimpleCNN (lr=0.01) | 0.15–0.25 | >0.55 | ✅ Preserved (shifted optimal) |

## Results Directory Structure

```
results/
├── exp_A_fixed/                    # λ scan (40%, 80% noise)
├── exp_B_fixed/                    # Random label experiments
├── exp_B2_anti_aligned/            # Anti-label (y+1) mod 10
├── exp_B3_ablation/                # Ablation study (TrueAnti, Renorm, K)
├── exp_C_fixed/                    # Method comparison
├── exp_D1_fixed/                   # Non-Oracle clean ratio
├── exp_D2_fixed/                   # Non-Oracle 80% noise
├── exp_D3_noise_scan/              # Noise rate threshold
├── exp_G_fixed/                    # Asymmetric noise
├── exp_I_cosine_intervention/      # Direct cosine manipulation (K=1)
├── exp_J_mechanism_decomposition/  # Mechanism analysis
├── exp_K_learning_dynamics/        # Convergence time measurement
├── exp_L_causal_intervention/      # Causal cos manipulation (K=16)
├── exp_M1_coarse_sweep/            # Coarse phase structure
├── exp_M2_fine_sweep_eta04/        # Fine sweep η=0.4 (critical region)
├── exp_M3_fine_sweep_eta08/        # Fine sweep η=0.8
├── exp_M3b_low_lambda_eta08/       # Low λ supplement
├── exp_N1_phase_diagram_low_noise/ # 2D phase diagram (η=0.2, 0.4)
├── exp_N2_phase_diagram_high_noise/# 2D phase diagram (η=0.6, 0.8)
├── exp_O_cifar100_universality/    # CIFAR-100 dataset
├── exp_P_architecture_universality/# ResNet18/34/VGG11/SimpleCNN
├── exp_P2_architecture_vgg_cnn/    # VGG11/SimpleCNN with lr=0.01
├── exp_Q1_finite_size_scaling/     # Width dependence
├── exp_Q2_hysteresis/              # Path dependence
├── exp_Q3_lr_lambda_interaction/   # LR-λ interaction
└── exp_Q4_cos_temporal/            # Cosine dynamics over time
```

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
| λ values | {0.1, 0.15, 0.2, 0.25, 0.3, 0.35, 0.4, 0.45, 0.5} |
| Cache K | 16 (default), 1 (for fresh gradient experiments) |
| Seeds | 3–10 per condition |

### Extended Experiments Configuration

| Experiment | Special Parameters |
|------------|-------------------|
| exp_I | K=1 (fresh gradients every step) |
| exp_K | λ ∈ {0.30, 0.35, 0.43, 0.45, 0.47, 0.55} |
| exp_L | cos_target ∈ {−0.9, −0.6, −0.3, 0.0, 0.3, 0.6, 0.9} |
| exp_M2/M3 | λ ∈ {0.38, 0.40, 0.42, 0.44, 0.46, 0.48, 0.50}, 10 seeds |
| exp_N1/N2 | η ∈ {0.2, 0.4, 0.6, 0.8} × λ grid |
| exp_O | Dataset: CIFAR-100 (100 classes) |
| exp_P | Models: ResNet18, ResNet34, VGG11, SimpleCNN |
| exp_P2 | lr=0.01 for VGG11/SimpleCNN |
| exp_Q1 | width_mult ∈ {0.5, 1.0, 2.0, 4.0} |
| exp_Q2 | Schedules: fixed, quench, ramp |
| exp_Q3 | lr ∈ {0.05, 0.1, 0.2} |

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
