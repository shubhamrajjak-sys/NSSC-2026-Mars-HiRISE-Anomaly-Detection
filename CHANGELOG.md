# Engineering Changelog

This document records the major engineering iterations of the Mars HiRISE
unsupervised anomaly detection pipeline.

---

## V1 — Baseline Convolutional Autoencoder

### Symptom
The initial model was designed as a simple convolutional autoencoder using
227×227 grayscale images and a 256-dimensional latent representation.

### Diagnosis
A baseline reconstruction model was required first to establish a reference
for reconstruction quality and latent-space anomaly detection.

### Fix
Implemented a custom convolutional autoencoder from scratch:

- Input: 227×227×1
- Encoder: convolutional layers with downsampling
- Latent dimension: 256
- Decoder: transposed convolutional layers
- Reconstruction loss: MSE
- No pretrained feature extractor or transfer learning

### Outcome
V1 establishes the baseline latent representation and reconstruction pipeline.

---

## V2 — Reconstruction / Representation Improvement

### Symptom
The baseline reconstruction may lose fine-grained terrain details and produce
overly smooth reconstructions.

### Diagnosis
Pixel-wise MSE alone can prioritize overall pixel similarity while missing
small structural differences that may be useful for anomaly interpretation.

### Fix
The reconstruction pipeline will be improved and evaluated using an additional
structural-quality measure such as SSIM, while maintaining the required
from-scratch architecture.

### Outcome
Compare V2 against V1 using reconstruction metrics and visual inspection.

---

## V3 — Anomaly Detection and Interpretability Improvement

### Symptom
A good reconstruction model alone does not directly provide an anomaly
decision or explain why an image is considered unusual.

### Diagnosis
Anomaly detection requires analysis of the learned latent representation,
followed by a statistically justified threshold and reconstruction-error
visualization.

### Fix
The pipeline will:

1. Extract latent vectors from the trained autoencoder.
2. Apply Isolation Forest to the latent vectors.
3. Convert anomaly scores so higher values represent greater novelty.
4. Determine a statistical anomaly threshold.
5. Select the top-5 highest-novelty samples.
6. Generate reconstruction-error heatmaps.
7. Compare anomalous regions with available metadata.

### Outcome
The final pipeline combines latent-space novelty detection with
reconstruction-based visual interpretation.

---

## Version Comparison

| Version | Main Change | Purpose |
|---|---|---|
| V1 | Baseline convolutional autoencoder | Establish baseline |
| V2 | Reconstruction/structural-quality improvement | Improve representation |
| V3 | Isolation Forest + threshold + heatmaps | Detect and interpret anomalies |

> Note: Final numerical results and measured improvements will be added after
> completing the experiments.
