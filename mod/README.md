# mod/ — Minecraft MOD

Fabric MOD that hooks block place/break events and emits JSON over WebSocket to the [`bridge/`](../bridge/).

## Status

Empty. Stack decision pending: see [#13 — Decide MOD framework: Fabric vs Forge](https://github.com/zuckeyM-17/block-bot/issues/13).

## Planned

- `BlockPlacedEvent` and `BlockBrokenEvent` listeners.
- WebSocket client → `bridge/` over `ws://localhost:8765`.
- Wire format documented in [`docs/PROTOCOL.md`](../docs/PROTOCOL.md) (not yet written).
