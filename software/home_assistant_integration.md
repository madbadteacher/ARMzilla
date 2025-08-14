# ArmZilla – Home Assistant Integration (Stub)

> **Status:** Planning phase. This doc will be expanded as hardware and software progress.

## Goals
- Integrate ArmZilla control and monitoring into The Lab’s existing Home Assistant ecosystem.
- Enable control from **ZillaPad** (wall-mounted dashboard).
- Allow automations triggered by sensors/events.

## Proposed Entities
- `armzilla.state` (idle, moving, error)
- `armzilla.pose` (x, y, z, yaw, pitch, roll)
- `armzilla.task` (pick_plate, place_plate, follow_me, custom)
- `armzilla.error` (code/message)

## Service Calls
- `armzilla.move_to(x, y, z, orientation)`
- `armzilla.pick_plate(printer_id)`
- `armzilla.place_plate(rack_slot)`
- `armzilla.follow_me(enable: bool)`

## Automations
- Plate swap when a print finishes (`printer.state == 'completed'`).
- Screw sorting after detection event from vision module.
- Follow-me mode triggered by mobile touchscreen docking.

## Dashboard Ideas
- Mushroom buttons for common tasks.
- Live camera view of the gripper.
- Position slider controls for manual moves.

## Next Steps
- Decide on protocol (likely **MQTT** with JSON payloads).
- Define HA `configuration.yaml` entries or use MQTT Discovery.
- Implement test script to move arm from HA service call.
