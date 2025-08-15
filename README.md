<p align="center">
  <img src="media/armzilla_claw.png" alt="ArmZilla Claw" width="300">
</p>

# ArmZilla

**ArmZilla** is a modular robotic arm project designed for The Lab — capable of:
- Sorting small screws and nuts.
- Removing and replacing 3D printer build plates.
- Following in "Follow Me" mode using a mobile touchscreen.
- Potential 3D printing functionality.
- (And yes… *theoretical* intruder deterrence via “death ray” 😉)

## Goals
- Reuse parts from Ender 3 and CR-10S printers.
- Max payload: ~1kg (suitable for flexible build plates + small prints).
- Modular joints for easy upgrades.
- Integration with The Lab’s LANzilla ecosystem.

## Roadmap
1. **Research & Design**
2. **Mechanical Build**
3. **Electronics & Control**
4. **Software Integration**
5. **Testing & Expansion**

flowchart TD
  %% GENERAL HARDWARE SORTER (ArmZilla + Top Camera + Sized Grid)

  subgraph FEED["Part Feed / Singulation"]
    A1[Dump mixed items onto tray]
    A2[Vibration/conveyor spreads parts<br/>(no touching if possible)]
    A1 --> A2
  end

  subgraph VISION["Vision (Top Camera + Sized Grid)"]
    V0[Trigger frame capture]
    V1[Detect all items in ROI<br/>(contours or tiny YOLO)]
    V2[Measure from grid (mm):<br/>L, D_shank, D_head, head crop]
    V3[Optional side cue (mirror/turntable)]
    V4[Classify per item:<br/>{screw, bolt, nut, washer, unknown}<br/>+ subtype (e.g., M3x10 CSK, M4 nut)]
    V5{Confidence ≥ τ ?}
    V6[Add (pick_point, class) to QUEUE]
    V7[Route to UNKNOWN queue]
    V0 --> V1 --> V2 --> V3 --> V4 --> V5
    V5 -- yes --> V6
    V5 -- no --> V7
  end

  subgraph QUEUE["Pick Queue"]
    Q1[Ordered list of items<br/>(nearest-first or shortest move)]
  end

  subgraph MOTION["Robot Motion (PAROL6)"]
    M0{Queue empty?}
    M1[Pop next item]
    M2[Compute pose: (u,v)->mm->robot XYZ<br/>via homography + hand–eye]
    M3[Move above item (safe Z)]
    M4[Descend & pick<br/>(vacuum or gripper)]
    M5[Lift to safe Z]
    M6[Move to bin for class]
    M7[Release item]
    M8[Return to approach pose]
    M0 -->|no| M1 --> M2 --> M3 --> M4 --> M5 --> M6 --> M7 --> M8 --> M0
  end

  subgraph EXC["Exceptions / Recovery"]
    E1{Pick success?}
    E2[Short retry: nudge tray<br/>or micro re-approach]
    E3[Send to UNKNOWN bin<br/>or re-queue once]
  end

  %% LINKS BETWEEN SUBGRAPHS
  A2 --> V0
  V6 --> Q1
  V7 --> Q1
  Q1 --> M0
  M4 --> E1
  E1 -- yes --> M5
  E1 -- no --> E2 -->|failed| E3 --> M0
  E2 -->|recovered| M5

  %% THROUGHPUT NOTES
  classDef note fill:#f7f7f7,stroke:#bbb,color:#333,font-size:11px;
  N1([Timing targets per item:<br/>Vision 0.2–0.6s • Plan 0.05s<br/>Move→Pick 1.2–2.0s • Place 1.2–2.0s<br/><b>Total 3–8s typical</b>]):::note
  N2([Batch capture once per 3–6 picks;<br/>refresh frame if queue < 2]):::note
  VISION --> N2
  MOTION --> N1
## License
TBD
