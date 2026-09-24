# Problem Framing

## Project Title

**Drone-Based Parking Occupancy and Potential Illegal Parking Detection Using YOLOv8**

## AECO Context

Large facilities, construction compounds, campuses, transport hubs, and managed parking assets require regular monitoring of parking-space occupancy and improperly positioned vehicles. Manual inspection can be repetitive, time-consuming, and difficult across large sites.

This project explores how drone or high-angle imagery and computer vision can support parking and facility-management teams by automatically identifying parking-space conditions and visually apparent potential parking violations.

## Problem Statement

The project aims to develop a cloud-reproducible YOLOv8 object-detection prototype capable of detecting four classes in aerial parking-area images:

- `Empty`: A marked parking space with no vehicle occupying it.
- `Occupied`: A marked parking space occupied by a vehicle.
- `Illegal`: A vehicle visibly positioned outside, across, or inconsistently with the represented parking boundaries.
- `LicensePlate`: A visible vehicle registration plate treated only as an object-detection class.

The `Illegal` class represents a potential visually apparent parking violation based on the dataset annotations. It does not constitute a legal determination.

## Proposed Workflow

The system receives an aerial or high-angle parking image and returns bounding boxes, class labels, and confidence scores. The detections can support preliminary parking monitoring and help a human operator identify areas that may require further review.

The prototype uses:

1. A frozen public dataset version prepared in Roboflow.
2. A YOLOv8 model trained and evaluated in Google Colab.
3. Validation images for quantitative evaluation.
4. Withheld images for inference on unseen examples.
5. Human review before any operational decision.

## Success Criteria

The prototype will be considered successful if it:

- Runs from top to bottom in a fresh Google Colab session without local installation or private credentials.
- Downloads the frozen dataset through a public, keyless GitHub Release URL.
- Verifies dataset integrity using a SHA256 checksum.
- Completes a YOLOv8 training run of at least 30 epochs.
- Reports Precision, Recall, mAP50, and mAP50–95.
- Produces training curves and a confusion matrix.
- Generates detections on validation and previously withheld images.
- Documents representative successes, false positives, false negatives, and localization errors.
- Provides a clear human-in-the-loop and governance statement.

No fixed accuracy threshold is guaranteed before training. The achieved metrics will be reported transparently and interpreted in relation to the dataset size, class balance, and deployment limitations.

## Intended Users

Potential users include:

- Facility-management teams.
- Parking-asset operators.
- Construction-site logistics teams.
- Campus and transport-hub operators.
- Authorized personnel responsible for reviewing parking conditions.

## Scope

The prototype is designed for aerial or high-angle parking-area images that are visually similar to the training data. It supports preliminary screening and evidence prioritization.

## Out of Scope

The project does not:

- Determine legal liability.
- Automatically issue parking penalties.
- Identify vehicle owners.
- perform optical character recognition on registration plates.
- Replace an authorized human reviewer.
- Guarantee reliable performance on street-level CCTV footage.
- Guarantee generalization to locations, weather conditions, or camera perspectives absent from the dataset.
- Support safety-critical or law-enforcement decisions without independent verification.

## Risk Priority

A false negative may allow an improperly positioned vehicle to remain undetected. A false positive may incorrectly flag a compliant vehicle and create unnecessary review work.

Because an `Illegal` prediction may affect individuals, every alert must be reviewed by an authorized human operator before any action is taken.

## Ethical Position

This system is an academic prototype and a decision-support tool. It must not be used as the sole basis for enforcement, legal, financial, or life-safety decisions.
