# Chapter 4 – Payload & Torque

This chapter sizes ArmZilla’s “muscle” so joints aren’t under‑ or over‑built.

## Key Terms
- **Payload (m):** Mass at the wrist (tool + object).
- **Torque (τ):** Rotational force at a joint, τ = m · g · r.
- **Reach (r):** Distance from joint axis to the payload’s center of mass.
- **Safety factor (SF):** Margin for acceleration, friction, surprises (typically 1.5–2.0).

## Baseline Assumptions
- Max payload: **1.0 kg** (e.g., 460 g plate + print + gripper).
- Link lengths (example): **L1 = 300 mm**, **L2 = 300 mm** (full reach ≈ 600 mm).
- Gravity: **g = 9.81 m/s²**.

## Static Torque (worst case: arm fully extended)
- **Shoulder torque (payload only):**
  τ₁ = m · g · (L1 + L2)
  = 1.0 · 9.81 · 0.6 ≈ **5.9 N·m**

- **Elbow torque (payload only):**
  τ₂ = m · g · L2
  = 1.0 · 9.81 · 0.3 ≈ **2.9 N·m**

> Add link/self‑weight: estimate upper‑arm+forearm+wrist ~1.5 kg with CoM ~0.3 m from shoulder → +~4.4 N·m at shoulder.  
> **Shoulder total static ≈ 10 N·m.** Use **SF 1.5** → **design ≈ 15 N·m**.

## What that means for motors
- Typical NEMA17 stepper torque ~**0.4–0.5 N·m** (holding).  
- With gearing:
  - **Shoulder:** NEMA17 + **~1:30 cycloidal** → ~12–15 N·m (good).  
  - **Elbow:** NEMA17 + **~1:20–1:25** → ~8–12 N·m (ample).  
  - **Wrist:** 1:10 gearbox or 50–60 kg·cm servo (5–6 N·m peak) for orientation.

**Closed‑loop/servo‑steppers** are recommended on shoulder/elbow for stall detection and smoother motion.

## Speed & Acceleration
- Start conservatively: **max 100–150 mm/s**, low accel.  
- Increase once plate swaps are reliable.  
- High gear ratios increase torque but reduce speed; tune jerk/accel to avoid oscillation on the ceiling rail.

## Gripper Force (plate tab pinch)
- Target **~40 N** pinch (≈4 kgf) with TPU pads; easily achieved by a micro NEMA17 + 1:5 drive or a 20–30 kg·cm RC servo.

## Rail Drive
- Moving mass (arm+carriage) target: **≤5–6 kg**.  
- **NEMA17 + GT2 belt** is sufficient; add endstops both ends.  
- Use rubber isolation to limit ceiling vibration.

## Quick Checklist
- [ ] Set link lengths (L1, L2) in a config file.  
- [ ] Choose gear ratios: ~1:30 (shoulder), ~1:20–25 (elbow), ~1:10 (wrist).  
- [ ] Pick closed‑loop drivers for shoulder/elbow.  
- [ ] Validate with a **1 kg test load** at full reach before real tasks.
