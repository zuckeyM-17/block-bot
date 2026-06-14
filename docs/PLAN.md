# block-bot — Project Plan

> Snapshot of the plan as of 2026-06-14. Living document.

## Goal

Use an FDM 3D printer + open-source robotics + Minecraft to build a niche, defensible business at the intersection of Physical AI × gaming × education.

## Strategy: niche specialty, not BtoB

We rejected:
- Stylish small goods / cable mgmt / storage → red ocean, race to bottom
- Minecraft merch alone → IP grey zone, oversupply from China
- Electronics enclosures alone → maker saturation

We chose:
- **Physical AI × Minecraft.** As of 2026, demand for LeRobot-class robot arms is exploding; supply of community-made accessories, kits, and content is thin. The Minecraft crossover is essentially uncontested.

## Hardware

### SO-ARM101 (LeRobot)

- 6-DOF leader + follower arms, Feetech STS3215 × 12 servos.
- Reach ~45 cm. Usable workspace ~30 cm × 30 cm on a tabletop.
- Payload ~200–500 g depending on gripper.

### Where to buy

- **Recommended:** [Seeed Studio SO-ARM101 Pro Kit (no 3D parts)](https://www.seeedstudio.com/SO-ARM101-Low-Cost-AI-Arm-Kit-Pro-p-6427.html) — $240, ships to Japan ~1 week, reliable.
- Cheaper: [AliExpress listing](https://www.aliexpress.com/item/1005008986168668.html) (use Choice shipping, Feetech/Waveshare official stores).
- Pre-assembled (skip the build): [Seeed Studio assembled kit](https://www.seeedstudio.com/SO-ARM-101-Assembled-Kit-Pro-p-6691.html), ~$400.

### Buying notes

- Japan import tax kicks in above ¥16,666 inc. shipping. Split servo orders to stay under.
- Buy +1 spare servo (a few % DOA rate).
- Prefer AliExpress Choice shipping (tracked, fast refunds).

### Reference repos

- STL: <https://github.com/TheRobotStudio/SO-ARM100>
- LeRobot: <https://github.com/huggingface/lerobot>

## Software architecture

```
Minecraft  ──MOD──▶  WebSocket (JSON)  ──▶  Python bridge  ──▶  LeRobot API  ──▶  SO-ARM101
   ▲                                                                                  │
   │                                                                                  ▼
   └─── Minecraft world updates ◀─── coord transform ◀─── OpenCV (camera) ◀──── physical cubes
```

1. **Minecraft MOD** (Fabric/Forge) — hooks block-place and block-break events, ships JSON over WebSocket.
2. **Python bridge** — coord transform (Minecraft → table), task queue, dispatches pick/place.
3. **SO-ARM101 control** — start with simple IK; later, imitation learning via LeRobot.
4. **Vision (Phase 3)** — OpenCV HSV mask or ArUco for cube identification and bidirectional sync.

## Cubes (first product)

- 3 cm cubes with studs on top (independent dimensions — not LEGO-compatible to avoid patent/legal noise).
- All 16 Minecraft colors via FDM color swap.
- Optional pixel-grain surface texture for the Minecraft feel.
- Sell as a set on BOOTH (¥3,000–5,000); also useful as building blocks for kids without the robot.

## CAD progression

1. **Tinkercad** — first stud cube (30 min, browser, free, commercial-OK).
2. **OpenSCAD** — parametric: one source generates all sizes × colors. Free, OSS, commercial-OK.
3. **FreeCAD** or **Plasticity ($150 one-time)** — for complex SO-ARM101 mods later.
4. **Fusion 360 paid** — only if revenue justifies it.

Fusion 360 Personal is technically non-commercial; avoid it for the business path.

## Camera setup

- Phase 3 entry: USB webcam (e.g. C920) ~50 cm above the table on a desk arm.
- Detection: HSV color mask first (50 lines of OpenCV), upgrade to ArUco for precision, YOLO only if needed.
- LeRobot-standard later: overhead + wrist cameras for imitation learning.

## Phases

### Phase 0 — Setup & ordering (now → ~2 weeks)

1. Order SO-ARM101 Pro Kit from Seeed Studio.
2. Download SO-ARM100 STLs and start FDM printing (~20–30 hr total).
3. Tinkercad: build first 3 cm stud cube.
4. OpenSCAD: parametrize the cube.

### Phase 1 — Assembly & teleop (2 weekends)

1. Assemble leader + follower.
2. Run LeRobot teleop tutorial.
3. Imitation learning demo (1–2 simple tasks).
4. Post a "build" video to YouTube/Twitter.

### Phase 2 — Bridge MVP

1. Fabric/Forge MOD sending place/break events over WebSocket.
2. Python bridge: coord transform + task queue.
3. MVP: 10 identical cubes, single-color, fixed start positions, simple pick & place.

### Phase 3 — Vision & "creeper face" demo

1. Add overhead webcam + OpenCV color mask.
2. Multi-color cube support.
3. Recreate a Minecraft creeper face from the cube set in physical space.
4. Bidirectional sync: real cubes → Minecraft world.

### Phase 4 — Productize

1. List the cube set on BOOTH/Etsy.
2. Publish improved SO-ARM101 STLs to Printables/MakerWorld for backlinks.
3. English video content targeting HuggingFace / LeRobot communities.
4. Education kit (MOD + cubes + curriculum) for programming schools.

## Licensing & legal

- SO-ARM100/101 STLs: Apache 2.0 — modification and commercial use OK, credit required.
- Pre-assembled kits raise technical conformance / liability questions in Japan — start with STL + parts list links, defer pre-assembled sales.
- Avoid Minecraft trademarked terms / textures in product naming. "Voxel cube set" rather than "Minecraft cube set".

## Open questions

- Repo public from day 1, or stage privately first? Default: public, build in public.
- Minecraft MOD framework: Fabric or Forge? Lean Fabric (modern, cleaner API).
- Bridge protocol: WebSocket JSON or something more structured (gRPC)? Default WebSocket for v0.
