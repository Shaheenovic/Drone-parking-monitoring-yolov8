# Governance Checklist

## Project Purpose

This project is an academic YOLOv8 prototype for drone-based parking occupancy monitoring and potential illegal-parking detection. It is intended to support preliminary visual screening and human review.

## Data Source and Rights

- **Dataset source:** Roboflow Universe project: Drone Parking Monitoring YOLOv8.
- **Original dataset format:** Aerial or high-angle parking-area images with object-detection annotations.
- **Dataset version used:** Version 1 – Clean 80/20 Baseline.
- **Dataset redistribution:** The frozen dataset export is published as a GitHub Release asset for keyless reproducibility.
- **Dataset license:** CC BY 4.0, subject to attribution requirements and confirmation of the source dataset's redistribution rights.
- **Code license:** MIT License.

## Privacy and Consent

- The system does not perform facial recognition.
- The system does not perform optical character recognition on vehicle registration plates.
- The system does not read, store, or publish plate characters.
- The `LicensePlate` class is used only as an object-detection label.
- The system does not identify vehicle owners or connect detections to external databases.
- No client, private project, or personally collected surveillance images are used in this prototype.

## Data Minimisation

The project uses only the visual information required for parking occupancy and potential illegal-parking detection.

The project does not collect or infer:

- Vehicle-owner identity.
- Driver identity.
- Registration-plate text.
- Personal contact details.
- Legal history or penalties.
- Location tracking over time.

## Limitations

The model is trained on a limited dataset of aerial or high-angle parking images. It may not generalise reliably to:

- Street-level CCTV footage.
- Different camera heights or viewing angles.
- Different parking layouts.
- Severe glare, shadows, rain, fog, or low-light conditions.
- Very small, partially occluded, or blurred objects.
- Locations with different parking rules, signs, permits, or enforcement practices.

The `Illegal` class represents a potential visually apparent parking violation based on dataset annotations. It is not a legal determination.

## Risk Assessment

### False Negatives

A false negative may fail to flag a potentially improperly positioned vehicle. This could delay review of an obstruction or parking issue.

### False Positives

A false positive may flag a compliant vehicle, creating unnecessary workload or concern for a reviewer.

### Risk Control

- Every `Illegal` prediction requires human verification.
- The model must not automatically issue penalties or enforcement actions.
- The model must not be used as the sole basis for legal, financial, disciplinary, safety-critical, or law-enforcement decisions.
- Confidence scores, image context, and operational rules must be considered by the reviewer.

## Human-in-the-Loop Process

1. The model produces a detection, class label, bounding box, and confidence score.
2. An authorised human reviewer examines the image and surrounding parking context.
3. The reviewer determines whether further operational action is required.
4. Any action is based on human judgment and applicable site procedures, not solely on the model output.

## Accountability

The final decision remains the responsibility of the authorised facility, parking, or site-management operator. The model developer and automated system do not determine legal liability.

## Deployment Position

This academic prototype is suitable only for preliminary screening and research demonstration. It is not approved for production deployment without additional data collection, testing, privacy assessment, operational validation, and governance approval.
