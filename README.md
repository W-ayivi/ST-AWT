# ST-AWT: Structure Tensor-Guided Adaptive Wavelet Thresholding for Edge-Preserving Speckle Suppression in Ultrasound Imaging

This repository provides information about the proposed **ST-AWT** framework for ultrasound speckle suppression.

ST-AWT is a hybrid image enhancement method that combines structure tensor-based local coherence estimation, U-Net-based coherence refinement, adaptive wavelet thresholding, and residual-preserving spatial fusion. The method is designed to reduce speckle noise in ultrasound images while preserving tissue boundaries and edge-related anatomical structures.

> **Note:** The full source code will be released after manuscript review and acceptance.

---

## Overview

Ultrasound images are commonly affected by speckle noise, a granular pattern caused by the coherent interference of backscattered acoustic waves. While speckle suppression can improve image readability, excessive filtering may remove diagnostically relevant boundary and texture information.

The proposed ST-AWT framework addresses this problem using a structure-aware thresholding strategy. Instead of applying a uniform wavelet threshold across the image, ST-AWT uses a local coherence field derived from the structure tensor to modulate the threshold spatially.

In homogeneous regions, stronger thresholding is applied to suppress speckle. Near tissue boundaries and coherent anatomical structures, weaker thresholding is applied to preserve structural information.

---

## Main Components

The ST-AWT framework consists of the following components:

1. **Synthetic Speckle Modelling**  
   Multiplicative Rayleigh speckle noise is added to ultrasound images to create paired noisy and pseudo-clean samples for controlled evaluation.

2. **Structure Tensor Coherence Estimation**  
   A fixed, non-trainable structure tensor module estimates local image coherence from Gaussian-smoothed gradient products.

3. **U-Net-Based Coherence Refinement**  
   A lightweight U-Net branch learns a contextual coherence refinement map from the noisy ultrasound image.

4. **Adaptive Wavelet Thresholding**  
   The final coherence map guides spatially adaptive soft-thresholding in the wavelet domain.

5. **Spatial Fusion and Residual Preservation**  
   A trainable fusion module combines the wavelet-denoised image with the original noisy input to reduce over-smoothing and preserve weak tissue structures.

---

## Dataset

The experiments use the publicly available **Ultrasound Nerve Segmentation** dataset from Kaggle:

https://www.kaggle.com/competitions/ultrasound-nerve-segmentation/data

The original dataset was created for brachial plexus nerve segmentation. In this work, only the ultrasound image files are used for speckle suppression experiments. The segmentation masks are not used for model training or evaluation.

---

## Experimental Setting

The study evaluates ST-AWT against three reference methods:

- Speckle Reducing Anisotropic Diffusion (SRAD)
- Non-Local Means filtering (NLM)
- Uniform wavelet soft-thresholding

The evaluation metrics include:

- Structural Similarity Index Measure (SSIM)
- Peak Signal-to-Noise Ratio (PSNR)
- Contrast-to-Noise Ratio (CNR)
- Edge Preservation Index (EPI)
- Mean Squared Error (MSE)

---

## Summary of Results

In the present experimental setting, ST-AWT achieved the following results on the held-out test set:

| Method | SSIM | PSNR (dB) | CNR | EPI | MSE |
|---|---:|---:|---:|---:|---:|
| ST-AWT | 0.9235 ± 0.0120 | 22.9756 ± 0.6430 | 4.5055 ± 0.3668 | 0.9734 ± 0.0041 | 0.0051 ± 0.0007 |
| SRAD | 0.5316 ± 0.0487 | 18.2625 ± 0.8453 | 3.7714 ± 0.4412 | 0.7601 ± 0.0159 | 0.0152 ± 0.0029 |
| NLM | 0.9119 ± 0.0095 | 21.9791 ± 0.6183 | 4.6276 ± 0.3840 | 0.9667 ± 0.0049 | 0.0064 ± 0.0008 |
| Wavelet-Soft | 0.9066 ± 0.0101 | 22.1143 ± 0.6943 | 4.4854 ± 0.3840 | 0.9678 ± 0.0043 | 0.0062 ± 0.0009 |

These results indicate that ST-AWT achieved the highest SSIM, PSNR, and EPI, together with the lowest MSE, among the compared methods. NLM achieved the highest CNR.

---

## Repository Status

This repository currently contains documentation and manuscript-related information only.

The complete implementation will be added after the manuscript review process.

Planned future release:

- Training script
- Testing script
- Dataset preparation instructions
- Baseline implementations
- Evaluation scripts
- Pretrained checkpoint, where permitted
- Example qualitative outputs

---

## Citation

If you use this work or refer to the method, please cite the paper once it becomes available.

```bibtex
@article{Ayivi2026STAWT,
  title   = {ST-AWT: Structure Tensor-Guided Adaptive Wavelet Thresholding for Edge-Preserving Speckle Suppression in Ultrasound Imaging},
  author  = {Ayivi, Williams},
  journal = {Under review},
  year    = {2026}
}
