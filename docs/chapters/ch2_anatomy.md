# Chapter 2 – Basic Robot Arm Anatomy

Robotic arms mirror human anatomy: segments (links) joined by joints to place and orient a tool (end effector). Designing ArmZilla “from the fingertips back” ensures every joint is sized for real loads.

## Human → Robot mapping
- **Fingers → End Effector:** Gripper, vacuum cup, or other tools.
- **Hand → Wrist:** 2–3 rotational axes (yaw/pitch/roll) to orient the tool.
- **Forearm → Lower Link:** Light, stiff structure (carbon/alu) between wrist and elbow.
- **Elbow → Mid Joint:** Extends/retracts reach; must handle forearm + wrist + payload.
- **Upper Arm → Link to Shoulder:** Strongest structural link; keep weight low.
- **Shoulder → Base Joint:** Lifts/rotates entire arm; highest torque demand.
- **Torso → Rail Carriage:** Moving platform carrying the shoulder.
- **Legs → Ceiling Rail:** Fixed track; straight, rigid, well-mounted with end-stops.

## Design principle
Start at the payload (plate/screw) → specify gripper → size the wrist → estimate forearm mass → specify elbow torque → size upper-arm and shoulder → confirm carriage and rail stiffness.
