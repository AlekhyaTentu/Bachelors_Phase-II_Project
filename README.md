

---

# Robust Single-Image Super-Resolution (SISR) via Hybrid CNN-TV Optimization

**Advanced Computer Vision | Department of ECE | Malla Reddy Engineering College**

## 📌 Executive Summary

While State-of-the-Art (SOTA) Convolutional Neural Networks (CNNs) like EDSR and RCAN achieve high PSNR values, they often lack **Measurement Consistency**. If the reconstructed high-resolution (HR) image is down-sampled, it frequently fails to match the original low-resolution (LR) input, especially under "Operator Mismatch" (e.g., training on Bicubic but testing on Box-averaging).

This repository implements a **Post-Processing Framework** that bridges Data-Driven (CNN) and Model-Based (Optimization) methods. By utilizing **Total Variation (TV-TV) Minimization** solved via the **Alternating Direction Method of Multipliers (ADMM)**, we enforce physical consistency and suppress artifacts, resulting in superior morphological reconstruction.

## 📂 System Architecture

```text
├── docs/
│   └── Phase_2_Technical_Report.pdf  # Comprehensive mathematical proofs
├── simulation/
│   ├── admm_convergence_plots.png    # Residual error reduction over iterations
│   └── quality_metrics_comparison.png # PSNR/SSIM Delta (CNN vs. Hybrid)
├── src/
│   ├── admm_optimizer.m              # Core ADMM implementation for TV-TV
│   └── cnn_inference_wrapper.py      # Interface for EDSR/RCAN priors
└── README.md

```

## 🛠️ Technical Specifications & Toolchain

* **Optimization Meta-Heuristic:** ADMM (Alternating Direction Method of Multipliers).
* **Deep Learning Priors:** RCAN (Residual Channel Attention Networks), EDSR (Enhanced Deep Residual Networks).
* **Regularization:** Dual-term Total Variation (TV) for edge preservation and noise suppression.
* **Metric Suite:** Peak Signal-to-Noise Ratio (PSNR), Structural Similarity Index (SSIM).

## ⚙️ Mathematical Framework

The system treats the CNN output ($w$) as a structural prior and solves a constrained optimization problem to find the optimal HR image ($x$):

### **Objective Function:**

$$\min_{x} \text{TV}(x) + \beta \text{TV}(x - w) \quad \text{s.t. } Ax = b$$

**Where:**

* $Ax = b$ represents the **Measurement Consistency Constraint** (Down-sampling fidelity).
* $\text{TV}(x)$ enforces **Sparsity** in the gradient domain (preserving edges).
* $\beta \text{TV}(x - w)$ ensures **Fidelity** to the deep-learning learned features.

## 🚀 Key Impacts & Engineering Breakthroughs

* **Operator Robustness:** Demonstrated that the hybrid model maintains reconstruction integrity even when the down-sampling kernel $A$ is unknown or mismatched during training.
* **Artifact Suppression:** Significantly reduced "ringing" artifacts and checkerboard patterns commonly introduced by pure CNN up-sampling layers.
* **Global Convergence:** Implemented an efficient ADMM solver that processes the entire image manifold rather than local patches, ensuring global consistency.

---

