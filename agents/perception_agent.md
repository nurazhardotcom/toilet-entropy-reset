# Perception Agent

Role: Observe home and produce a `CurrentState` document.

## Inputs
- Camera feeds (fixed + robot-mounted)
- Optional: robot vacuum maps, door/window sensors, odor sensors

## Outputs
For each room/zone:
- Detected surfaces and their state (cluttered/clean, wet/dry, etc.)
- Detected objects with:
  - class (keys, shoes, clothes, dishes, toys, mail, etc.)
  - location (room, surface, approx coords)
  - confidence score

## Logic
1. Compare `CurrentState` vs `HomeState` schema
2. Emit deviations:
   - `surface_deviation`: surface not meeting pristine_predicate
   - `location_deviation`: object not in its canonical_location
   - `consumable_deviation`: consumable below threshold

## Toilet-Specific Perception
- Bowl stain detection (vision + UV)
- Seat wetness detection (capacitive sensor)
- Floor wetness detection (moisture sensor)
- Odor detection (e-Gas sensor)
- Paper roll level (weight/IR sensor)
- Soap level (weight sensor)
- Bin fill level (IR/ultrasonic sensor)

## Implementation Notes
- VLM/VLA for object + scene understanding
- Run on edge device or robot; output JSON for planner
- Confidence thresholds: discard detections below 0.7
