# Improving SIRENs for Image Representation

This project explores architectural and optimization modifications to improve the image-fitting performance of **Sinusoidal Representation Networks (SIRENs)**, introduced in *Implicit Neural Representations with Periodic Activation Functions* (Sitzmann et al., 2020).

Using the official SIREN implementation as the baseline, I experimented with learning-rate scheduling, shortcut connections, and self-attention mechanisms. Model performance was evaluated using Peak Signal-to-Noise Ratio (PSNR) and Structural Similarity Index (SSIM).

## Overview

SIRENs are implicit neural representations that use periodic activation functions to model complex signals as continuous functions of their coordinates. For image representation, the network learns a mapping from 2D pixel coordinates to pixel intensity values.

The baseline SIREN achieved a **PSNR of 35.840 dB** and an **SSIM of 0.923**. I explored three modifications to examine whether its image-fitting performance could be improved.

## Experiments

### 1. Learning Rate Scheduling

I compared increasing and decreasing learning-rate schedules using cosine annealing.

| Learning Rate Schedule | PSNR (dB) | SSIM |
|---|---:|---:|
| Baseline | 35.840 | 0.923 |
| Decreasing (0.0001 → 0.00001) | 33.207 | 0.895 |
| Increasing (0.0001 → 0.001) | **44.708** | **0.987** |

Under the experimental setup used here, gradually increasing the learning rate substantially improved both PSNR and SSIM relative to the baseline.

### 2. Shortcut Connections

Inspired by residual connections in ResNet, I added shortcut connections to the SIREN architecture and evaluated their effect on image fitting.

| Model | PSNR (dB) | SSIM |
|---|---:|---:|
| Baseline | 35.840 | 0.923 |
| + Shortcut Connections | **39.171** | **0.962** |

Adding shortcut connections improved both evaluation metrics relative to the baseline.

### 3. Self-Attention

I incorporated self-attention at five different positions within the SIREN architecture to examine how attention placement affects representation quality.

| Attention Position | PSNR (dB) | SSIM |
|---:|---:|---:|
| 1 | 29.548 | 0.814 |
| 2 | 35.342 | 0.923 |
| 3 | **37.996** | **0.955** |
| 4 | 36.075 | 0.904 |
| 5 | 26.365 | 0.654 |

Among the tested positions, placing self-attention in the middle of the network (Position 3) produced the best performance and outperformed the baseline.

## Implementation

The implementation was adapted from the official [SIREN repository by Vincent Sitzmann et al.](https://github.com/vsitzmann/siren) and extended to evaluate alternative training and architectural configurations for image fitting.

The experiments include:

- Compared increasing and decreasing learning-rate schedules using cosine annealing
- Added ResNet-inspired shortcut connections to the SIREN architecture
- Incorporated self-attention at different positions within the network
- Evaluated image-fitting performance using PSNR and SSIM

## Report

For a detailed description of the methodology, experimental setup, and results, see the full project report.

## References

- Sitzmann, V., Martel, J. N. P., Bergman, A. W., Lindell, D. B., & Wetzstein, G. (2020). *Implicit Neural Representations with Periodic Activation Functions*. NeurIPS 2020.
- Baseline implementation: [vsitzmann/siren](https://github.com/vsitzmann/siren)
