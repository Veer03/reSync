# AGENTS.md: instructions for AI coding tools

Read this first. Then read `docs/GOALS.md` and `docs/DECISIONS.md`.

## Project in one line
reSync is an open-source, on-device audio engine. It listens to environmental sound and turns it into music that fits the music the user is playing. Software and library first. No hardware.

## About the human
- Beginner programmer, learning as we go. The AI writes most code.
- Explain things in **simple language**. Define any jargon the first time.
- Be **brutally honest**. If an idea won't work, say so and offer a real alternative.
- Research before claiming something exists. If you can't verify a library, project, or number, say "unverified".
- Ask a clarifying question when a choice matters. Don't guess silently.

## Working rules
1. **Small steps.** One layer at a time (see `docs/ROADMAP.md`). Don't build future layers early.
2. **Make it run first, then make it good.** Every step ends with something the human can run and hear.
3. **Measure latency** (delay from sound in to sound out) at every audio step and write the number in `docs/DECISIONS.md`.
4. **Explain what you changed** in 3-5 plain sentences after each task.
5. **Don't add dependencies silently.** Check the license, add it to `docs/RESEARCH.md`, then use it.
6. **Keep everything on-device.** No cloud calls, no telemetry, no uploading audio. Ever.
7. **Safety rule:** the app must never fully hide important sounds (sirens, horns, approaching vehicles) from someone who may be walking or driving. Build this in from the start.
8. Record each important choice in `docs/DECISIONS.md` (what, why, date).

## Stack
- Engine (`core/`): **Rust**. Pure sound math (pitch tracking, synth, scale snapping). It takes audio buffers in and gives audio buffers out. It does NOT talk to audio devices.
- Bindings: UniFFI generates Kotlin (and later Swift) wrappers from the Rust code.
- Android app: Kotlin + Jetpack Compose. Device audio I/O on Android: Oboe or cpal. Decide in Layer 3 by measuring delay.
- Windows/desktop testing: cpal for mic and speakers.
- Sketching: Python 3 (numpy, sounddevice). Throwaway experiments only, not product code.
- Later: Swift for iOS.

## Current focus
Layer 1: pitch to note, sketched in Python on a laptop. See `docs/ROADMAP.md`.

## Code style
- Simple and readable over clever.
- Comment the "why", not the "what".
- Real-time audio code (Rust): no memory allocation, no locks, no printing inside the audio callback.
- Prefer safe Rust. Any `unsafe` needs a comment explaining why.
- Engine functions must be testable with plain arrays or WAV files, with no device needed.
