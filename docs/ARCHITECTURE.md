# sownd architecture (achievable)

## North-star

A developer-first audio automation platform that feels like a DAW-adjacent patchbay:

- Graph-based routing for audio + events + MIDI + OSC + HTTP/WebSocket
- Runs locally or as a network hub
- Extensible node/plugin model
- Realtime-safe where it matters, observable everywhere

## Design rules (non-negotiable)

1. **Two worlds**
   - **Realtime world**: audio + sample-accurate scheduling. No blocking, no I/O, bounded allocations.
   - **Automation world**: HTTP, file I/O, LLM calls, device discovery, macros, retries.
2. **Typed ports** and **JSON-serializable state** for every node.
3. **LLM proposes, compiler validates**: LLM output must be schema-valid and previewable.
4. **One graph spec** shared by UI, local runner, and hub.

## Components

### 1) UI app
Desktop-first (recommended): Tauri shell hosting a web UI.

UI responsibilities:
- Node graph editor + inspector
- Control surface pages (buttons/faders/meters)
- Project management (save/load, assets)
- Observability views (event log, node stats, jitter meters)

### 2) Realtime engine
The realtime engine owns audio rendering and tightly scheduled musical events.

Implementation options:
- **MVP**: Web Audio + AudioWorklet (inside the app WebView)
- **Upgrade**: native audio sidecar (Rust/C++), UI talks over IPC/WebSocket/gRPC

Realtime responsibilities:
- Audio graph processing (DSP nodes)
- Event scheduling with deterministic timing
- Realtime-safe bridge from automation → realtime

### 3) Automation engine (ETL/orchestration)
Runs asynchronous nodes and long-running tasks.

Responsibilities:
- HTTP/WS/OSC integrations
- file operations, asset indexing
- recording management
- LLM + ASR/TTS service calls
- retries, rate limits, credentials
- structured event log and metrics

### 4) Hub (network runtime)
The hub hosts graphs and exposes APIs so sownd can act like a network appliance.

Responsibilities:
- Graph deployment/run/stop
- client sessions, auth, permissions
- shared transport/clock (optional)
- device/satellite registry

## Data model

- **Project**: graphs + assets + presets + bindings
- **Graph**: nodes + edges + transport config
- **Node**: type + params + runtime state + UI state
- **Edge**: typed connection from port → port

## “Companion mode” model

- **Actions**: invokable operations (trigger scene, toggle node, set param)
- **Bindings**: map input (MIDI/OSC/UI button/HTTP) → action
- **Feedback**: state updates (LED color/label/meter)

## Why this works

- Realtime stays deterministic and small.
- Automation stays powerful without breaking audio.
- The graph spec becomes the product surface: saveable, shareable, API-run.
