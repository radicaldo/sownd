# sownd SOW (statement of work)

This is a practical scope outline for building sownd in phases.

## Vision

Build a modular audio automation + networking platform with a drag/drop node graph, companion-style control surfaces, and developer-first APIs.

## Deliverables

### D0: Specification + scaffolding
- Graph spec v0.1
- Repo layout and dev scripts
- Minimal UI shell with graph canvas loading a sample graph

### D1: Patchbay MVP
- Graph editor: palette, inspector, connect ports, save/load, undo/redo
- Transport: play/stop, BPM
- Realtime output: synth + gain/meter + master
- MIDI routing: in/out
- Local Hub API: REST + WebSocket events

Acceptance criteria:
- Can build a graph that makes sound, routes MIDI, and persists.
- Playback stable for 30+ minutes with visible jitter metrics.

### D2: Automation + companion mode
- Actions/bindings/feedback model
- Control surface UI (buttons/faders/pages)
- Nodes: HTTP trigger, WebSocket trigger, OSC out, timers/schedulers
- “Satellite” clients can connect and control graphs

Acceptance criteria:
- Any action invokable via API.
- Feedback updates are consistent and debuggable.

### D3: Recording/looping/clips
- Recorder node (bus capture to file)
- Loop node (record → quantize → loop)
- Scene/clip launcher

Acceptance criteria:
- Looping stays in sync with transport.

### D4: AI assist
- Offline ASR for commands
- Local LLM assisted authoring
- Guardrails: schema validation, preview/diff, safe apply

Acceptance criteria:
- AI can’t crash realtime engine.
- All AI operations leave an audit trail.

## Risks and mitigations

- **Realtime stability**: isolate realtime runtime; measure jitter; avoid main-thread load.
- **Cross-platform device I/O**: desktop-first shell; provide fallbacks; document support.
- **Plugin surface sprawl**: keep node types few and composable early.
- **AI hallucinations**: strict schemas + “propose then apply” workflow.
