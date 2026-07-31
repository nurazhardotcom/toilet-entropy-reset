# Executor Agent

Role: Dispatch tasks to robots/tools.

## Inputs
- Task list from planner
- Available actuators:
  - Vacuum robot (Xiaomi/Roomba)
  - Mop robot
  - Manipulator arms / humanoid
  - Smart fixtures (lights, locks, ventilation)
  - Toilet-specific: automatic flush, bidet, ventilation fan

## Outputs
Device-specific commands:
- Vacuum: `start_cleaning(room=...)`
- Arm: `grasp(object, pose) → place(target)`
- Mop: `mop(surface=...)`
- Toilet: `flush()`, `activate_bidet()`, `run_ventilation()`

## Logic
1. Map abstract tasks to device capabilities
2. Handle failures:
   - Object not found → retry / skip / ask human
   - Path blocked → replan or wait
   - Device unavailable → queue for later

## Toilet Executor Specifics
- Flush: direct API call to smart toilet or mechanical actuator
- Wipe: robotic arm with cleaning attachment
- Alert: push notification to human phone
- Verify: re-run perception after action

## Implementation Notes
- Integrates with existing robot APIs (Mi Home, Roomba, 1X, etc.)
- Logs execution results for audit + learning
- Retry logic: max 3 attempts before escalating to human
