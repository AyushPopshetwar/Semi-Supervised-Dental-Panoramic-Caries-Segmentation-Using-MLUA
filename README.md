# Semi-Supervised-Dental-Panoramic-Caries-Segmentation-Using-MLUA

## Overview

This repository contains the implementation and experimental analysis of a semi-supervised deep learning framework for dental caries segmentation in panoramic dental radiographs.

The work is based on the paper:

**MLUA: Multi-Level Uncertainty-Aware Learning for Semi-Supervised Medical Image Segmentation**

and extends the original framework with several architectural and training modifications including:

* Attention-gated Feature Pyramid Network (FPN)
* Deep Supervision
* Monte Carlo Uncertainty Estimation
* Exponential Moving Average (EMA) Teacher-Student Learning
* Tversky Loss
* Focal Loss
* Weighted BCE Loss
* Gamma-based Monte Carlo Augmentation
* Test-Time Augmentation (TTA)

The framework was evaluated on the **DC1000 Dental Caries Dataset** for lesion segmentation from panoramic dental X-ray slices.

---

## Repository Structure

```text
.
├── Implementation/
│   ├── MLUA_Core_Implementation.ipynb
│   └── MLUA_Enhanced_Implementation.ipynb
│
├── Reports/
│   ├── MLUA_Core_Implementation_Report.pdf
│   └── MLUA_Enhanced_Implementation_Report.pdf
│
├── Presentation/
│   └── MLUA_Combined_Presentation.pptx
│
└── README.md
```

---

## Dataset

Experiments were performed using the **DC1000 Dental Caries Dataset**.

Dataset structure:

```text
DC1000_dataset/
├── org_train_dataset/
│   ├── images/
│   └── labels/
│
├── org_test_dataset/
│   ├── images/
│   └── labels/
```

The dataset contains annotated dental caries lesions extracted from panoramic dental radiographs.

---

## Core MLUA Implementation

The core implementation follows the original MLUA framework:

### Encoder

* ResNet34 Backbone

### Decoder

* Feature Pyramid Network (FPN)

### Semi-Supervised Components

* Student Network
* EMA Teacher Network
* Monte Carlo Sampling
* Uncertainty Filtering
* Consistency Regularization

### Loss Function

```text
L_total = L_supervised + λ(t) × L_consistency
```

where:

```text
L_supervised = Weighted BCE + Dice Loss
```

and

```text
L_consistency = MSE(Student, Teacher)
```

computed only in low-uncertainty regions.

---

## Enhanced MLUA Implementation

The enhanced implementation introduces several improvements over the baseline framework.

### Architectural Enhancements

* Attention Gates
* Multi-scale Feature Fusion
* Deep Supervision
* Feature Refinement Blocks
* Weighted Pyramid Aggregation

### Training Enhancements

* Tversky Loss
* Focal Loss
* Weighted BCE Loss
* Gamma Transformation Sampling
* Test-Time Augmentation

### Enhanced Supervised Loss

```text
L_supervised =
    L_Tversky
  + L_Focal
  + L_WeightedBCE
```

---

## Monte Carlo Uncertainty Estimation

The teacher network generates multiple stochastic predictions:

```text
T = 10
```

using:

* Gaussian Noise Injection
* Gamma Transformation

For each unlabeled image:

```text
Prediction 1
Prediction 2
...
Prediction T
```

are aggregated to obtain:

```text
Mean Prediction
```

and

```text
Uncertainty Map
```

The uncertainty map is used to suppress unreliable pseudo-labels.

---

## Training Pipeline

1. Load labeled and unlabeled batches.
2. Generate student predictions.
3. Generate teacher predictions using EMA weights.
4. Apply Monte Carlo perturbations.
5. Estimate uncertainty.
6. Compute uncertainty mask.
7. Calculate supervised loss on labeled data.
8. Calculate consistency loss on unlabeled data.
9. Update student parameters.
10. Update teacher using EMA.

---

## Hyperparameters

| Parameter               | Value     |
| ----------------------- | --------- |
| Image Size              | 384 × 384 |
| Batch Size              | 8         |
| Labeled Batch Size      | 4         |
| Unlabeled Batch Size    | 4         |
| Learning Rate           | 3e-4      |
| Epochs                  | 50        |
| EMA Alpha               | 0.99      |
| Monte Carlo Samples     | 10        |
| Uncertainty Threshold β | 0.75      |

---

## Evaluation Metrics

The following segmentation metrics are reported:

* Dice Score
* Intersection over Union (IoU)
* Sensitivity (Recall)
* Specificity
* Precision
* Accuracy

Definitions:

```text
Dice = 2TP / (2TP + FP + FN)

IoU = TP / (TP + FP + FN)

Sensitivity = TP / (TP + FN)

Specificity = TN / (TN + FP)
```

---

## Experimental Results

### Core MLUA

| Metric      | Score  |
| ----------- | ------ |
| Dice        | 0.6619 |
| IoU         | 0.5492 |
| Sensitivity | 0.6915 |
| Specificity | 0.9963 |

### Enhanced MLUA

Performance depends on the selected loss configuration and uncertainty settings.

Detailed ablation studies are presented in:

* Enhanced Project Report
* Final Presentation

---

## Included Documents

### Reports

* Project Report
* Enhanced Project Report

Both reports contain:

* Literature Review
* Methodology
* Experimental Setup
* Results
* Ablation Studies
* Comparative Analysis

### Presentation

The final presentation includes:

* Problem Statement
* Dataset
* Architecture
* Semi-Supervised Learning Framework
* Loss Functions
* Results
* Conclusions

---

## References

1. Wang et al., MLUA: Multi-Level Uncertainty-Aware Learning for Semi-Supervised Medical Image Segmentation.

2. Ghimire et al., When CNNs Outperform Transformers and Mambas: Revisiting Deep Architectures for Dental Caries Segmentation.

3. DC1000 Dental Caries Dataset.

---


Research Area:

* Medical Image Segmentation
* Semi-Supervised Learning
* Deep Learning for Dental Imaging
