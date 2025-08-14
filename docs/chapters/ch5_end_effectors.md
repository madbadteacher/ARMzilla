# Chapter 5 – End Effectors

The **end effector** is the “tool” at the end of ArmZilla’s wrist. Choosing and designing the right one is critical to task performance.

## Common Types
1. **Parallel Gripper**
   - Two jaws move in and out in parallel.
   - Best for rigid, regular shapes (plates with grab tabs, small boxes).
   - Can be 3D printed with TPU pads for grip.

2. **Vacuum Cup**
   - Uses suction to lift flat, non-porous surfaces.
   - Ideal for smooth build plates, glass, metal sheets.
   - Needs a small vacuum pump (12V DC) + solenoid valve.

3. **Magnetic Tool**
   - Uses an electromagnet or neodymium magnet.
   - For ferrous parts like screws, nuts, or tools.

4. **Multi-Tool Quick Change**
   - Tool plate with electrical + pneumatic pass-throughs.
   - Allows swapping between gripper, vacuum, or specialty tools.

---

## Gripper Design for ArmZilla
- **Grip force target:** 40 N (~4 kgf) for plate handling.
- **Jaw opening:** ~80–100 mm (fits most build plates).
- **Actuation:** NEMA17 with 1:5 gearbox OR 20–30 kg·cm RC servo.
- **Pads:** TPU 95A printed inserts with textured surface.

---

## Mounting Interface
- **Bolt pattern:** 4 × M4 on 30 mm square.
- **Electrical:** JST-XH for limit switch / sensor feedback.
- **Optional:** Pneumatic line for vacuum tool.

---

## Tool Sensing
- **Limit switch:** Detects fully open/closed state.
- **Current sensing:** Detects gripping force or stall.
- **Camera alignment:** Wrist-mounted camera for fine positioning.

---

## Quick Change Mechanism Ideas
- Magnetic latch with alignment pins.
- Cam-lock lever + electrical connector.
- Spring-loaded bayonet twist-lock.

---

## Future Expansion
- Pen/marker holder for drawing on workpieces.
- Small spindle for engraving or PCB milling.
- Camera/light module for inspection tasks.

---

**Next:** Chapter 6 will cover **Ceiling Rail & Carriage Design** for stable, smooth arm travel.
