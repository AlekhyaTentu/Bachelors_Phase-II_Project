
---

## Robust Single-Image Super-Resolution via CNNs and TV-TV Minimization

**Advanced Computer Vision & Signal Optimization | MREC (Undergraduate Research)**

### Technical Narrative

Modern Super-Resolution (SR) pipelines often rely exclusively on Convolutional Neural Networks (CNNs). While these models yield high-quality visual textures, they frequently violate **Measurement Consistency**—a phenomenon where the reconstructed High-Resolution (HR) image, when down-sampled, does not mathematically align with the original Low-Resolution (LR) input. This lack of robustness is particularly evident in production environments where the down-sampling kernel (A) is unknown or differs from the training data (Operator Mismatch).

This project implements a hybrid reconstruction framework that treats the CNN output as a structural prior within a formal optimization problem. By applying **Total Variation (TV-TV) Minimization** and solving the resulting non-smooth objective function via the **Alternating Direction Method of Multipliers (ADMM)**, we enforce strict physical fidelity while preserving learned morphological features.

---

### Project Structure

```text
├── documents/
│   └── Technical_Report.pdf     # Research Methodology, Proofs, and Performance Analysis
└── README.md                    # Technical Specification and Executive Summary

```

---

### Engineering Stack & Domain Expertise

* **Optimization Meta-Heuristics:** Alternating Direction Method of Multipliers (ADMM).
* **Deep Learning Priors:** Integration with Residual Channel Attention Networks (RCAN) and Enhanced Deep Residual Networks (EDSR).
* **Mathematical Modeling:** Total Variation (TV) Regularization and Gradient Sparsity.
* **Metric Frameworks:** Signal-to-Noise Ratio (PSNR) and Structural Similarity (SSIM) Benchmarking.

---

### Mathematical Implementation Details

The framework solves for a reconstructed image $x$ by minimizing a multi-term objective function. This approach ensures that the output is not only visually sharp but also mathematically grounded in the input data.

**Objective Function:**


$$\min_{x} TV(x) + \beta TV(x - w) \quad \text{subject to } Ax = b$$

* **Data Fidelity ($Ax = b$):** A hard constraint ensuring the reconstructed HR image remains consistent with the LR measurement $b$ under the down-sampling operator $A$.
* **Geometric Prior ($TV(x)$):** Enforces a sparsity constraint on the image gradients to mitigate ringing artifacts and suppress noise while maintaining sharp edge transitions.
* **Prior Regularization ($\beta TV(x - w)$):** Measures the distance between the solution $x$ and the CNN-generated prior $w$, effectively utilizing the network's learned features as a guide for high-frequency detail.

---

### Key Engineering Impacts

* **Convergence Accuracy:** Demonstrated a near-perfect reduction in reconstruction residual error ($4.7 \times 10^{-7}$), validating the efficacy of the ADMM solver.
* **Operator Robustness:** Quantified superior performance against pure CNN architectures when tested against mismatched blur kernels (e.g., Box-averaging kernels vs. Bicubic training).
* **Benchmark Performance:** Achieved systematic improvements in SSIM and PSNR metrics across standard datasets (Set5, Set14, and BSD100), effectively bridging the gap between data-driven and model-based image restoration.

---

