# sownd security model (v0.1)

## Goals

- Keep realtime engine stable and safe.
- Make automation powerful without letting it become arbitrary remote code execution.
- Provide clear permissions for nodes (developer-first, not “mystery behavior”).

## Key rules

1) Realtime nodes never do network/filesystem.
2) Automation nodes declare capabilities (permissions).
3) LLM output is treated as untrusted input.

## Capabilities (examples)

- `network.http`
- `network.websocket`
- `network.osc`
- `filesystem.read`
- `filesystem.write`
- `device.midi`
- `device.microphone`

Nodes must declare required capabilities. The runtime can prompt/deny.

## LLM safety

- LLM only generates:
  - graph patches (JSON)
  - pattern snippets (text)
- All patches must validate against schemas.
- Apply flow is always: propose → diff/preview → user confirm → apply.
- Keep an audit log of prompts and applied patches.

## Network safety

- Hub API requires auth by default in non-local mode.
- Provide a read-only mode for dashboards.
- Rate limit event-producing endpoints.
