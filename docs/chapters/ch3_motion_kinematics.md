# Chapter 3 – Motion & Kinematics

This chapter explains how ArmZilla moves and how we calculate the joint angles needed to put the gripper where we want it.

## Key Terms
- **Pose**: Position + orientation of the end effector (gripper).
- **Forward Kinematics (FK)**: Joint angles → end‑effector pose.
- **Inverse Kinematics (IK)**: Desired pose → joint angles (what we need for “go here”).
- **Workspace**: All points ArmZilla can reach.
- **Repeatability vs. Accuracy**: Being able to hit the *same* spot vs. the *true* spot.

## Coordinate Frames
- Define a **base frame** at the shoulder.
- Define a **tool frame** at the gripper.
- Use tags/fixtures to align to printers and bins.

## Links & Joints (ArmZilla mental model)
- J1 (Shoulder yaw), J2 (Shoulder pitch), J3 (Elbow), J4–J6 (Wrist yaw/pitch/roll).
- Link lengths: upper arm `L1`, forearm `L2`. Keep these in mm in your notes.

## Forward Kinematics (concept)
- Multiply transforms from base → tool:
  - `T_base^tool = T1 * T2 * T3 * T4 * T5 * T6`
- Each `Ti` is a rotation/translation from joint i.
- Result gives `(x, y, z)` + orientation (yaw/pitch/roll or quaternions).

## Inverse Kinematics (concept)
- Given a target pose `(x, y, z, orientation)`, solve for `θ1…θ6`.
- Start simple: **planar 2‑link** (J2/J3) for plate pick/place:
  - With target in a vertical plane, solve elbow/shoulder first, then set wrist to match orientation.
- Use numeric solvers (MoveIt/IKFast) once the geometry is fixed.

## Practical Strategy for ArmZilla
1. **Teach points**: Save key poses (printer park, plate rack slots, bin locations).
2. **Approach vectors**: Add a small offset normal to the surface (e.g., +Z 20 mm), move, then descend.
3. **Blending**: Use small radius blending between waypoints for smooth motion.
4. **Speed/Accel**: Start slow (e.g., 50–100 mm/s, low accel), increase once reliable.
5. **Soft limits**: Define joint angle limits to avoid self‑collision.

## Calibration Tips
- Put **AprilTags** on printers and racks; compute pose from the camera to auto‑correct.
- Home joints → move to a **fixture block** to verify zero.
- Save and reuse a **kinematics config** (link lengths, offsets).

## Checklist Before First Moves
- Joint directions correct (positive angles move as expected).
- Homing & limit switches verified.
- Emergency stop tested.
- Tool offset measured (TCP from wrist to gripper tips).

---

**Next:** Chapter 4 will cover **Payload & Torque** with concrete numbers for your 1 kg max payload and recommended gear ratios.
