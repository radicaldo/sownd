# sownd roadmap

This is a practical, buildable roadmap that gets to a compelling demo quickly while keeping a clean path to “serious” engine work.

## Phase 0 — Spec + scaffolding (days)
- Lock graph JSON format + versioning
- Choose UI graph framework and IPC
- Establish repo layout and contribution conventions

## Phase 1 — Patchbay MVP (weeks)
- Graph editor (palette, inspector, cables, undo/redo)
- Transport + deterministic event scheduling
- Basic audio output (one synth + gain/meter + master)
- MIDI in/out routing
- Local Hub API: REST + WebSocket event stream

## Phase 2 — Automation + companion mode (weeks)
- Actions/bindings/feedback model
- Control surface pages (buttons/faders)
- Nodes for HTTP/WS/OSC triggers and outputs
- “Satellite” clients for remote control

## Phase 3 — Recording + looping + clips (weeks)
- Recorder node (buses to file)
- Loop node (record/quantize/loop)
- Scene/clip launcher

## Phase 4 — AI assist (weeks)
- Offline ASR for commands (Whisper family)
- Local LLM authoring (Ollama) for patterns and graph patches
- Guardrails: schema validation + preview/diff + safe apply

## Phase 5 — Beatboxing/humming to tracks (R&D)
- Audio→features→events pipelines (onsets, pitch, classification)
- MIDI export + sample mapping + groove templates
- Optional separation-first workflows (stems)
