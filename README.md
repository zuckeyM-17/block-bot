# block-bot

**Physical AI × Minecraft.** A real robot arm builds in the real world what you build in Minecraft, and vice versa.

> Building in public. Follow the journey.

## What is this

- **SO-ARM101** robot arm (Hugging Face LeRobot) controlled by Minecraft world events.
- **Minecraft MOD** (Fabric/Forge) hooks block place/break and streams them over WebSocket.
- **Python bridge** translates Minecraft coords → real-table coords → LeRobot pick & place commands.
- **3D-printed color cubes** (16 Minecraft colors, ~3cm with studs) as the physical voxels.
- **Camera + OpenCV** (HSV color masks / ArUco markers) for vision and bidirectional sync.

## Why

There's a gap. Physical AI research (HuggingFace LeRobot, MineDojo, Voyager) is exploding, and Minecraft is the world's most-used learning environment. But almost nobody is bridging **tabletop physical robots × Minecraft**. block-bot fills that gap as an open-source playground and a productized cube set.

## Roadmap

- **Phase 0** — Order SO-ARM101, learn CAD, print frames, design v0 cube.
- **Phase 1** — Assemble arm, teleop, first imitation-learning demo.
- **Phase 2** — Minecraft MOD ↔ Python ↔ SO-ARM101 bridge MVP (pick & place).
- **Phase 3** — Camera + color recognition, "build a creeper face" demo.
- **Phase 4** — Productize: color cube set on BOOTH/Etsy, improved STL on Printables/MakerWorld.

Full plan: [`docs/PLAN.md`](docs/PLAN.md). Track progress in [Issues](https://github.com/zuckeyM-17/block-bot/issues) and [Milestones](https://github.com/zuckeyM-17/block-bot/milestones).

## Stack

| Layer | Tech |
|---|---|
| Robot | SO-ARM101 (Feetech STS3215 × 12, ~$240 from Seeed Studio) |
| Robot software | Hugging Face LeRobot |
| Minecraft MOD | Fabric or Forge (Java/Kotlin) |
| Bridge | Python + WebSocket |
| CAD | Tinkercad → OpenSCAD → FreeCAD/Plasticity |
| Vision | OpenCV (HSV masks, ArUco) |
| 3D Print | FDM |

## Status

🚧 Phase 0. Hardware not yet ordered. Following along is the most fun part — star/watch this repo.

## License

MIT for code. STL files: Apache 2.0 inherited from upstream [TheRobotStudio/SO-ARM100](https://github.com/TheRobotStudio/SO-ARM100) where derivative.
