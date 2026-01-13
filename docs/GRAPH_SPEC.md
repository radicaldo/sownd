# sownd graph spec (v0.1 draft)

This document defines the portable graph format and runtime interfaces.

## Graph JSON

High-level shape:

- `version`: string (e.g., "0.1")
- `transport`: `{ bpm, timeSignature, swing, scene }`
- `nodes`: `Node[]`
- `edges`: `Edge[]`
- `assets`: `Asset[]`

### Node

Required:
- `id`: string (stable UUID)
- `type`: string (e.g., "audio.synth.basic")
- `params`: object (schema-defined)

Optional:
- `state`: object (runtime-managed; should be persistable when safe)
- `ui`: object (position, collapsed, color, etc.)

### Edge

- `id`: string
- `from`: `{ nodeId, port }`
- `to`: `{ nodeId, port }`
- `type`: one of the port types (below)

## Port types

- `audio`: realtime audio stream
- `event`: timestamped musical events (note/cc/automation)
- `midi`: raw MIDI bytes or structured packets
- `control`: parameter/control messages
- `http`: request/response or webhook payloads
- `ws`: websocket messages
- `osc`: OSC messages
- `text`: prompts, transcripts, code
- `blob`: file chunks / binary assets

## Event model

Canonical event envelope:

- `t`: time (transport-relative or sample-time; must be consistent per runtime)
- `kind`: string (e.g., "noteOn", "noteOff", "cc", "param")
- `data`: object
- `source`: `{ nodeId, port }`

Realtime delivery:
- automation → realtime uses a bounded queue
- backpressure policy must be explicit (drop oldest/newest, throttle, etc.)

## Node manifests (plugin metadata)

Each node type ships a manifest:

- `type`: string
- `name`: string
- `version`: semver
- `ports`: `{ inputs: PortDef[], outputs: PortDef[] }`
- `paramsSchema`: JSON Schema
- `capabilities`: e.g., `filesystem`, `network`, `midi`, `microphone`

## Runtime interfaces

### Realtime nodes

- must be deterministic
- no blocking, no network/files
- bounded memory behavior

### Task nodes (automation)

- async execution allowed
- should emit structured logs + progress
- should be restartable/idempotent where possible

## Versioning

- Graph JSON version is required.
- Node manifests are semver and should remain backwards compatible when possible.
- Provide migration tooling for graph versions.
