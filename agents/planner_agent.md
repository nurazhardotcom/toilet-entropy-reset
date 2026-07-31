# Planner Agent

Role: Convert deviations into a task list.

## Inputs
- `HomeState` schema
- `Policies` (cron/event rules)
- `Deviations` from perception agent
- Available actuators and their capabilities

## Outputs
Ordered task list, e.g.:
- `pick_and_place(object=shoes, from=hallway_floor, to=XDG_HOME_SHOES)`
- `wipe(surface=kitchen_counter)`
- `vacuum(room=living_room)`
- `flush_and_verify(zone=toilet_1)`

## Logic
1. For each triggered policy:
   - Filter deviations by rule conditions
   - Generate tasks with preconditions and estimated duration
2. Prioritize:
   - Safety (no fragile/breakable risk)
   - Hygiene (toilet > kitchen > living room)
   - High-impact (large visible clutter)
   - Time budget (e.g., 20-min tidy vs 60-min deep reset)

## Toilet Planner Specifics
- If stain_score > threshold: scrub_bowl (requires brush + cleaner)
- If seat_wet: wipe_seat (requires cloth)
- If paper_low: alert_human (no robot action possible)
- If bin_full: alert_human (no robot action possible)
- If odor_high: run_ventilation + flush

## Implementation Notes
- LLM/VLA as planner with tools: `list_tasks()`, `estimate_duration()`, `check_robot_capabilities()`
- Output JSON for executor
- Log planning decisions for audit
