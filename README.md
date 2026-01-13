# sownd

AV Production Automation Platform

`sownd` is a developer-first, modular **audio + MIDI + automation + networking** platform.

Think: a software-defined patchbay for music/AV production workflows.

- Drag/drop node graph for routing audio/events/MIDI/HTTP/WebSocket/OSC
- “Companion mode” control surfaces (buttons/faders/pages) with feedback
- Headless runner + Hub APIs so graphs can run locally or on a network node
- LLM-assisted authoring (patterns/patches) with strict validation and preview

## What sownd is (and is not)

**Is:** a programmable audio automation and networking engine with a slick graph UI.

**Not (v1):** a full timeline DAW replacement.

## Core ideas

- **Two worlds:**
	- **Realtime**: audio + sample-accurate scheduling (no blocking/await)
	- **Automation**: HTTP/files/LLM/webhooks/retries (observable, resilient)
- **Everything is a node:** typed ports + JSON-serializable state.
- **LLM proposes, compiler validates:** no direct arbitrary execution.

## Docs

- docs/ARCHITECTURE.md
- docs/GRAPH_SPEC.md
- docs/SOW.md
- docs/AI_AUDIO_STACK.md
- docs/SECURITY_MODEL.md
- ROADMAP.md

## Suggested MVP scope

A compelling MVP can be built around:
- Graph editor + save/load + undo/redo
- Transport (play/stop/BPM) + event scheduler
- 10–12 core nodes (Pattern/Clock/Synth/Sampler/FX/MIDI/HTTP/WS/OSC/Recorder)
- Local Hub API (REST + WebSocket events)

## License

See LICENSE.
