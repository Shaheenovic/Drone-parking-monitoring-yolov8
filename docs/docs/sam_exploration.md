# SAM Exploration Notes

## Purpose

Segment Anything Model (SAM) was explored as an annotation-assistance approach during dataset preparation. The purpose was not to replace human annotation, but to assess whether segmentation prompts could accelerate the creation or refinement of object boundaries in aerial parking images.

## What Helped

SAM can be useful when an object or parking-space boundary is visually distinct from its surroundings. In this project context, it may help annotators quickly identify approximate boundaries for:

- Clearly visible vehicles.
- High-contrast parking spaces.
- Objects with sharp edges and limited occlusion.
- Repetitive parking layouts where a human annotator can verify the generated region.

SAM-assisted outputs can reduce initial annotation effort when they are reviewed and corrected manually.

## What Did Not Work Reliably

SAM is less reliable for this dataset when:

- Vehicles are very small in the aerial image.
- Shadows overlap vehicle or parking-space boundaries.
- Multiple vehicles are close together.
- Parking lines are faded, partially hidden, or visually inconsistent.
- The object is partially occluded.
- License plates are too small or blurred.
- The visual distinction between an occupied space and a potentially illegal vehicle depends on parking context rather than object shape.

SAM outputs may therefore include incomplete masks, merged regions, or boundaries that do not match the intended YOLO bounding box.

## Decision for This Project

The final dataset uses the frozen source annotations reviewed through Roboflow. SAM is documented as an exploratory annotation-support tool only.

All training labels used for YOLOv8 are treated as human-reviewed dataset annotations. SAM outputs were not accepted automatically without manual verification.

## Lessons Learned

- Annotation consistency is more important than annotation speed.
- Small aerial objects require careful manual review.
- Parking-status labels depend on spatial context, not only segmentation quality.
- SAM can support an annotator, but it does not replace a clear labelling guide or human quality control.
