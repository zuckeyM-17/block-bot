# bridge/ — Python bridge

WebSocket server that receives Minecraft events from [`mod/`](../mod/), transforms coords (Minecraft → table), queues pick/place tasks, and dispatches to SO-ARM101 via LeRobot.

## Status

Empty. See [#16 Python bridge: WebSocket server + coord transform](https://github.com/zuckeyM-17/block-bot/issues/16) and [#17 task queue + LeRobot dispatcher](https://github.com/zuckeyM-17/block-bot/issues/17).

## Planned stack

- Python 3.11+
- `uv` for dep management
- `websockets` for the server
- `lerobot` for arm control
- `pytest` + `ruff`
