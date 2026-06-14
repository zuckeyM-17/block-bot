# block-bot — Claude Code context

## What this is

A Physical AI × Minecraft bridge. A real **SO-ARM101** robot arm picks and places **3D-printed color cubes** in response to Minecraft block-place/break events (and vice versa via camera). Built in public, OSS.

Full plan: [`docs/PLAN.md`](docs/PLAN.md).

## Repo layout

| Path | Stack | Purpose |
|---|---|---|
| `mod/` | Java / Kotlin, Fabric | Minecraft mod. Hooks block events, emits JSON over WebSocket. |
| `bridge/` | Python 3.11+ | WebSocket server, Minecraft↔table coord transform, LeRobot dispatcher. |
| `cad/` | OpenSCAD, STL | Parametric cube design, eventual SO-ARM101 improvements. |
| `docs/` | Markdown | Plan, protocol spec, ADRs. |
| `vision/` | Python (later) | OpenCV color masks, ArUco markers, camera calibration. |

## Conventions

- **Branches:** `feat/<topic>`, `fix/<topic>`, `chore/<topic>`, `docs/<topic>`. Avoid working on `main`.
- **PRs:** open one even for tiny changes, prefer many small PRs over a giant one. Squash-merge.
- **Commits:** imperative subject ("Add WebSocket reconnect"), body explains why if non-obvious.
- **Issues drive work:** every PR should reference an issue (`Refs #12` or `Closes #12`).
- **Milestones = phases:** keep work scoped to the active phase; nice-to-haves go to a later milestone or a `backlog` label.

## Local dev — once code exists

Will fill in as each stack lands. Anticipated:

- **Bridge (Python):** `uv` for deps, `pytest` for tests, `ruff` for lint.
- **Mod (Fabric):** `./gradlew runClient` for dev launch, `./gradlew build` for the jar.
- **CAD (OpenSCAD):** `openscad -o out.stl src.scad` for headless render.

## Don'ts

- **Don't use Minecraft trademarks in product names.** Use "voxel cube set", not "Minecraft cube set". Avoid Mojang-owned textures in marketing imagery.
- **Don't commit secrets.** Especially API keys for future BOOTH/Etsy/Printables automation. Use `.env` (gitignored).
- **Don't push to `main`.** PR workflow only.
- **Don't break the OSS license trail.** SO-ARM100/101 STL derivatives must stay Apache-2.0 with credit; cube originals stay MIT.

## Key references

- LeRobot: <https://github.com/huggingface/lerobot>
- SO-ARM100/101 STL upstream: <https://github.com/TheRobotStudio/SO-ARM100>
- Feetech STS3215 servo: <https://www.feetechrc.com>
- Fabric MOD docs: <https://fabricmc.net/wiki/start>

## Working with Claude Code on this repo

- Read `docs/PLAN.md` once at session start for full context.
- The active phase + open issues on the current milestone are the truthful source of "what to do next" — check via `gh issue list --milestone "Phase N — ..."`.
- Prefer editing existing files over creating new ones (especially in `docs/`).
- For multi-step work, open a draft PR early so progress is visible.
