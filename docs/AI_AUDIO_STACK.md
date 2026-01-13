# AI + audio stack (open source) for sownd

This is a curated list of practical OSS components for voice/text/audio-to-events workflows.

## Speech-to-text (ASR)

- Whisper family
  - whisper.cpp (MIT): https://github.com/ggml-org/whisper.cpp
    - fast, embeddable, works offline, good for desktop apps
  - faster-whisper (MIT): https://github.com/SYSTRAN/faster-whisper
    - efficient Python inference, good for services

Recommended sownd usage:
- Voice commands → intent JSON → actions/bindings (automation world)

## Text-to-speech (TTS)

- Piper (local neural TTS)
  - archived repo: https://github.com/rhasspy/piper
  - development moved (noted in README): https://github.com/OHF-Voice/piper1-gpl

- Coqui TTS (training + models)
  - https://github.com/coqui-ai/TTS

Recommended sownd usage:
- Speak feedback (“armed”, “recording”, “scene 2”) and assistive UX.

## Audio → MIDI / notes

- Basic Pitch (Apache-2.0)
  - https://github.com/spotify/basic-pitch
  - audio-to-MIDI with pitch bends; strong practical default

Recommended sownd usage:
- humming/monophonic lines → MIDI clips
- quick “turn this into notes” workflows

## Beatboxing / tapping → drums (realistic approach)

There is no single universally dominant OSS model that perfectly converts beatboxing into multi-track drums in all conditions.

A buildable pipeline:
1) onset/transient detection (find hit times)
2) classify hit type (kick/snare/hat/other)
3) quantize to transport + groove template
4) map to drum kit + humanize velocity

Start with (1)+(3)+(4) for MVP, add (2) as R&D.

## Source separation (optional but very useful)

- Demucs (MIT; archived upstream with a maintained fork noted)
  - https://github.com/facebookresearch/demucs

Recommended sownd usage:
- separate stems before transcription (vocals vs drums vs bass)

## MIR feature extraction (tempo, beats, onsets)

- Essentia (AGPL-3.0)
  - https://github.com/MTG/essentia

Note on licensing:
- AGPL can be incompatible with some distribution plans; evaluate early.

## Suggested “Audio→Clip” node recipes

- Record mic → VAD → segment → (Basic Pitch) → MIDI clip
- Record beatbox → onset detect → quantize → drum clip
- Record loop → separation → transcribe lead → keep drum stem as audio loop
