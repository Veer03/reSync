# reSync

**An open-source audio engine that turns the sounds around you into music.**

> Status: day zero. Nothing works yet. We build in small layers and write down what we learn.

## The idea (simple version)

Most headphones try to *block* the world. reSync tries to *play with* it.

A siren goes by. Instead of just hearing a harsh noise, the app hears its pitch and plays a matching note (a cello, a synth) that fits the key of the music you are already listening to.

## What reSync is

- A **software engine**, not a hardware product.
- Built as a **library first**, so it can be added to any app, any feature, or later any device.
- **Private by design:** all audio is processed on your device. Nothing is uploaded.
- **Open source**, built in public, one small layer at a time.

## What reSync is NOT (yet)

- Not a noise-cancelling replacement.
- Not a hardware gadget.
- Not a finished product. See `docs/ROADMAP.md` for the layers.

## How it will be built

```
 microphone → [ listen ] → [ understand ] → [ make music ] → headphones
                 pitch        what sound?     notes in key
```

Layers, in order:

1. **Pitch → note.** Hear a pitch, play a note in a musical key.
2. **Sound types.** Recognize siren, voice, drill, etc.
3. **Mixer screen.** Choose what the music reacts to.
4. **Body signals.** Heart rate shapes the music (later).
5. **Ship as a library** other apps can use.

## Tech choices

| Part | Choice | Why |
|------|--------|-----|
| Engine | Rust | Fast, and the compiler catches memory bugs. One codebase for Android, iOS, Windows. |
| Bridge | UniFFI | Auto-generates Kotlin and Swift wrappers for the Rust engine. |
| Android app | Kotlin | Standard for Android. |
| Sketching | Python | Quick throwaway experiments on a laptop. |
| Later | Swift (iOS) | After Android works. |

Details and reasons: `docs/DECISIONS.md`.

## Repo map (will grow slowly)

```
README.md
AGENTS.md          # context for AI coding tools
docs/
  GOALS.md         # what we are building right now
  ROADMAP.md       # the layers, in order
  RESEARCH.md      # open-source tools we are studying
  DECISIONS.md     # choices we made and why
prototype/         # Python sketches (first code goes here)
core/              # Rust engine (added in Layer 2)
```

New folders are added only when we need them.

## Contributing

Not open for contributions yet. Right now we are learning and prototyping. Watch this repo.

## License

Apache-2.0. See `LICENSE` and `docs/DECISIONS.md`.
