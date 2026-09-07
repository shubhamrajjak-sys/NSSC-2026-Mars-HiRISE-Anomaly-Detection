# Dataset

This directory is reserved for the Mars HiRISE dataset used in the
NSSC 2026 anomaly detection project.

## Dataset Source

The project uses official Mars Reconnaissance Orbiter (MRO) HiRISE v3
imagery provided for the NSSC 2026 problem statement.

The dataset contains approximately 10,000 cropped grayscale images,
standardized to 227×227 pixels.

## Local Dataset Structure

Place the dataset locally using a structure similar to:

```text
NSSC_2026/
├── images (1)/
│   ├── sample_00001.jpg
│   ├── sample_00002.jpg
│   └── ...
│
└── source_image_metadata.csv
