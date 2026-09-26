# Drone Parking Monitoring with YOLOv8

A computer-vision project for detecting parking-space status and parking-related objects in drone imagery using YOLOv8.

## Problem Framing

The project supports parking monitoring from aerial/drone images. It detects parking-related visual classes to help human operators review parking availability and potential parking violations.

The model is intended as decision support only. It must not be used as the sole basis for enforcement or automated penalties.

## Classes

| ID | Class | Description |
|---:|---|---|
| 0 | Empty | An empty parking space |
| 1 | Illegal | A vehicle or parking situation labelled as illegal |
| 2 | LicensePlate | A visible vehicle licence plate |
| 3 | Occupied | An occupied parking space |

Detailed label rules: [`docs/class_definitions.md`](docs/class_definitions.md)

## Dataset

- Format: YOLO detection format
- Split: 401 training images and 94 validation images
- Dataset source: [Roboflow Universe dataset](https://universe.roboflow.com/eng-ahmedshaheen-hotmail-com/drone-parking-monitoring-yolov8/dataset/1)
- Dataset documentation: [`docs/dataset_documentation.md`](docs/dataset_documentation.md)
- Dataset release asset: `drone-parking-v1-yolo11.zip` (release `v1.0`)
- SHA256: `3f9e38e8ae7f7725f19f5f120165a1f19e8a54808d27690648a530cfb6b12999`

## Model and Training

- Model: YOLOv8n
- Image size: 640
- Epochs: 30
- Batch size: 16
- Seed: 42
- Optimizer: Auto-selected AdamW
- Hardware: NVIDIA Tesla T4 GPU in Google Colab
- Ultralytics version: 8.4.163

## Results

Validation performance using the best trained checkpoint:

| Metric | Score |
|---|---:|
| Precision | 0.917 |
| Recall | 0.888 |
| mAP@50 | 0.903 |
| mAP@50-95 | 0.720 |

The model performed strongly on the validation set. `Illegal` and `Occupied` were the strongest classes, while small or difficult visual objects such as license plates and empty spaces remain more sensitive to image scale, lighting, occlusion, and scene ambiguity.

- Training results: [`results/curves/results.png`](results/curves/results.png)
- Confusion matrix: [`results/curves/confusion_matrix.png`](results/curves/confusion_matrix.png)
- Per-epoch metrics: [`results/curves/results.csv`](results/curves/results.csv)

## Evidence

- Ground-truth annotations: [`results/evidence/annotations`](results/evidence/annotations)
- Validation predictions: [`results/evidence/validation_predictions`](results/evidence/validation_predictions)
- New-image predictions: [`results/evidence/new_image_predictions`](results/evidence/new_image_predictions)

## Reproduce in Google Colab

1. Open [`notebooks/02_training_evaluation.ipynb`](notebooks/02_training_evaluation.ipynb).
2. Click **Open in Colab**.
3. In Colab, select **Runtime → Change runtime type → T4 GPU**.
4. Select **Runtime → Run all**.
5. The notebook installs dependencies, clones this repository, downloads the versioned dataset release, verifies the SHA256 checksum, prepares `data.yaml`, trains YOLOv8n for 30 epochs, validates the best model, and creates evidence outputs.
6. Expected training time on a T4 GPU is approximately 10–20 minutes. If GPU access is unavailable, load the provided weights for verification and inference instead of repeating full training.

## Reproducibility Checklist

- [x] Dataset version and source link documented
- [x] SHA256 checksum documented and verified in the notebook
- [x] Model variant documented: YOLOv8n
- [x] Training parameters documented: 30 epochs, batch 16, image size 640
- [x] Random seed documented: 42
- [x] Ultralytics version documented: 8.4.163
- [x] Validation metrics and training plots saved
- [x] Validation and new-image inference evidence included
- [x] Error analysis included

## Limitations and Governance

- The model supports human review and does not replace a trained operator.
- Predictions may fail in poor lighting, glare, shadows, heavy occlusion, motion blur, or unfamiliar parking layouts.
- False positives and false negatives should be reviewed before any operational action.
- Governance checklist: [`docs/governance_checklist.md`](docs/governance_checklist.md)
- Error analysis and improvement plan: [`docs/error_analysis.md`](docs/error_analysis.md)

## Repository Structure

```text
.
├── docs/
├── notebooks/
│   └── 02_training_evaluation.ipynb
├── results/
│   ├── curves/
│   └── evidence/
├── LICENSE
└── README.md
```

## License and Dataset Rights

This repository is released under the included [`LICENSE`](LICENSE). The dataset remains subject to its stated Roboflow/CC BY 4.0 terms, and users are responsible for complying with image rights, privacy obligations, and applicable local regulations.
