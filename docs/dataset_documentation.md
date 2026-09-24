# Dataset Documentation

## Dataset Summary

This project uses a frozen object-detection dataset for drone-based parking monitoring. The dataset contains aerial or high-angle parking-area images annotated with four classes:

| Class ID | Class Name |
|---:|---|
| 0 | `Empty` |
| 1 | `Illegal` |
| 2 | `LicensePlate` |
| 3 | `Occupied` |

The dataset supports an academic YOLOv8 prototype for parking-space occupancy monitoring and visually apparent potential illegal-parking detection.

## Dataset Source

- **Roboflow Universe project:**  
  https://universe.roboflow.com/eng-ahmed_shaheen-hotmail-com/drone-parking-monitoring-yolov8

- **Dataset version used for training:** Version 1 – Clean 80/20 Baseline
- **Export format:** YOLOv11
- **Declared dataset licence:** CC BY 4.0

Roboflow is used for dataset management, annotation review, and versioning. It is not the primary download path in the reproducible Colab workflow.

## Frozen Training Dataset

The exact ZIP export used in the project is hosted as a public GitHub Release asset:

- **Release tag:** `v1.0`
- **Dataset ZIP:**  
  https://github.com/Shaheenovic/Drone-parking-monitoring-yolov8/releases/download/v1.0/drone-parking-v1-yolo11.zip

- **SHA256 checksum:**

```text
3F9E38E8AE7F7725F19F5F120165A1F19E8A54808D27690648A530CFB6B12999
```

The Colab notebook downloads this ZIP directly from GitHub, verifies the SHA256 checksum, extracts it, and updates the dataset YAML paths for cloud execution.

## Dataset Size and Split

The uploaded project contains 495 annotated images after import and dataset validation in Roboflow.

| Split | Images | Intended Use |
|---|---:|---|
| Training | 396 | Model learning |
| Validation | 99 | Metric calculation and model evaluation |
| Test | 0 | Not used in the frozen version |
| External inference images | 5 | Held outside the training dataset for unseen-image inference |

The five external inference images are not part of the frozen training ZIP and are not used for training or validation.

## Preprocessing

The frozen Version 1 dataset applies:

- Auto-Orient.
- Resize to 640 × 640 pixels using stretch resizing.
- No augmentation in the baseline dataset version.

## Dataset Limitations

- The images represent aerial or high-angle parking conditions and may not generalise to street-level CCTV.
- The source dataset contains mixed target types: parking spaces, vehicles, and licence plates.
- `Illegal` is a dataset annotation describing a visually apparent potential parking violation; it is not a legal judgement.
- Licence plates may be small, blurred, partially hidden, or difficult to localise in aerial images.
- Images may not represent all parking geometries, environmental conditions, traffic patterns, or local regulations.

## Attribution and Redistribution

The dataset is released under the declared CC BY 4.0 licence. Any reuse or redistribution must retain appropriate attribution to the dataset source and comply with the original licence terms.

The project repository uses the MIT License for code and documentation only. The MIT License does not replace or override the dataset licence.
