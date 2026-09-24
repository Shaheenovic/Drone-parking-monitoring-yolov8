# Class Definitions and Label Rules

## Purpose

This document defines the four object-detection classes used in the Drone Parking Monitoring YOLOv8 dataset. The definitions describe how the existing dataset annotations are interpreted for training, evaluation, and error analysis.

The classes represent visual patterns in aerial or high-angle parking images. They do not independently establish whether a vehicle is legally or illegally parked under local regulations.

## Class Mapping

| Class ID | Class Name | Operational Definition |
|---:|---|---|
| 0 | `Empty` | A marked parking space that contains no vehicle. |
| 1 | `Illegal` | A vehicle or parking condition labelled by the source dataset as visibly inconsistent with the represented parking arrangement. |
| 2 | `LicensePlate` | A visible vehicle registration plate annotated as an object, without reading or storing its characters. |
| 3 | `Occupied` | A marked parking space containing a vehicle positioned within the represented parking area. |

## Empty

### Include

- Clearly visible marked parking spaces containing no vehicle.
- Spaces that remain identifiable despite moderate shadows or lighting variation.
- Partially visible empty spaces when their parking boundaries remain sufficiently clear.

### Exclude

- Unmarked open ground.
- Driving lanes and pedestrian paths.
- Spaces whose occupancy cannot be determined because of severe obstruction.
- Areas outside the defined parking layout.

### Labelling Rule

The bounding box should cover the annotated parking-space area as consistently as possible without unnecessarily including adjacent spaces.

## Occupied

### Include

- Marked parking spaces visibly occupied by a vehicle.
- Vehicles positioned within the parking-space boundaries represented by the dataset.
- Partially occluded vehicles when their occupied-space status remains visually identifiable.

### Exclude

- Vehicles moving through a driving lane.
- Vehicles labelled as `Illegal` in the source annotations.
- Empty parking spaces.
- Vehicles whose position cannot be determined reliably.

### Labelling Rule

The annotation should follow the source dataset convention for an occupied parking space. It should not be interpreted as confirmation that the vehicle is legally parked under local law.

## Illegal

### Include

- Vehicles labelled by the source dataset as parked outside the represented parking arrangement.
- Vehicles visibly positioned across parking boundaries.
- Vehicles occupying circulation or other non-parking areas when this is apparent in the image.
- Other visually apparent parking configurations assigned to the `Illegal` class in the frozen dataset.

### Exclude

- Vehicles correctly positioned within marked parking spaces.
- Vehicles whose legal status depends on information absent from the image, such as permits, time restrictions, ownership, or local enforcement rules.
- Moving vehicles when stopping or parking cannot be established from the image.
- Ambiguous cases that cannot be interpreted visually.

### Labelling Rule

`Illegal` means a **potential visually apparent parking violation according to the dataset annotation**, not a legal judgment. Every prediction requires human verification.

## LicensePlate

### Include

- Vehicle registration plates that are visibly identifiable as plate objects.
- Partially visible plates when their location and object type remain clear.

### Exclude

- Text that is not a vehicle registration plate.
- Plate-like regions that are too blurred or obstructed to identify as plate objects.
- Reflections, vehicle badges, road markings, and signs.

### Labelling Rule

The bounding box should tightly enclose the visible plate. The project performs object detection only and does not use OCR, transcribe characters, identify vehicle owners, or connect plates to external databases.

## General Annotation Rules

- Use one bounding box per labelled object or parking-space instance.
- Keep bounding boxes as tight and consistent as possible.
- Avoid including unnecessary background.
- Apply the same interpretation across training and validation images.
- Include partially visible objects only when their class remains identifiable.
- Do not guess labels when visibility or parking context is insufficient.
- Record ambiguous and inconsistent annotations for later error analysis.
- Do not change validation labels after reviewing model predictions unless a genuine annotation error is independently confirmed.

## Known Ambiguities

The dataset combines parking-space classes (`Empty` and `Occupied`) with object-oriented classes (`Illegal` and `LicensePlate`). Their bounding boxes may therefore represent different types and scales of visual targets.

The `Illegal` class also depends partly on parking context. A single aerial image may not show vehicle movement, stopping duration, permits, temporary restrictions, or local regulations. Model outputs must consequently be described as preliminary visual flags.

`LicensePlate` objects may be very small in aerial images, which can increase missed detections and
