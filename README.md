
# 🚀 NSSC 2026 — Unsupervised Anomaly Detection in Mars HiRISE Imagery

## 📌 Project Overview

This project addresses the NSSC 2026 Data Analytics problem:

**"Unsupervised Anomaly Detection in Mars HiRISE Orbital Imagery."**
 
The objective is to learn the dominant visual distribution of Martian surface imagery without using ground-truth anomaly labels or pretrained feature extractors, and then identify images that significantly deviate from the learned representation.

The solution combines:

- Deep convolutional autoencoder
- Compact latent representation
- Unsupervised Isolation Forest
- Statistical anomaly thresholding
- Metadata-based location analysis
- Reconstruction error analysis
- Pixel-level anomaly heatmaps

---

## 🎯 Objective

The main goal is to build an end-to-end unsupervised novelty detection pipeline capable of:

1. Learning a compact representation of Mars HiRISE imagery.
2. Detecting unusual samples using latent-space anomaly detection.
3. Establishing a statistically defensible anomaly threshold.
4. Analyzing anomaly locations using available metadata.
5. Interpreting detected anomalies using reconstruction differences.

No ground-truth anomaly labels are used during model development.

---

# 🛰️ Dataset

The project uses Mars Reconnaissance Orbiter (MRO) HiRISE imagery provided for the NSSC 2026 challenge.

The dataset contains approximately **10,000 cropped grayscale images**, standardized to:

**227 × 227 pixels**

The provided metadata contains information such as:

- Source image ID
- Latitude
- Longitude
- Sun angle
- Season
- Resolution

Raw competition images are not included in this repository.

---

# 🧠 Methodology

The complete pipeline consists of three major phases.

```text
Mars HiRISE Images
        │
        ▼
Image Preprocessing
227 × 227 Grayscale
        │
        ▼
┌─────────────────────────┐
│ Phase 1                 │
│ Deep Latent Compression │
│                         │
│ CNN Autoencoder         │
│        ↓                │
│ 256-D Latent Vector     │
└─────────────────────────┘
        │
        ▼
┌─────────────────────────┐
│ Phase 2                 │
│ Anomaly Detection       │
│                         │
│ Isolation Forest        │
│        ↓                │
│ Novelty Score           │
│        ↓                │
│ Statistical Threshold   │
└─────────────────────────┘
        │
        ▼
┌─────────────────────────┐
│ Phase 3                 │
│ Reconstruction Analysis │
│                         │
│ Top Anomalies           │
│        ↓                │
│ Reconstruction Error    │
│        ↓                │
│ Error Heatmaps          │
└─────────────────────────┘
