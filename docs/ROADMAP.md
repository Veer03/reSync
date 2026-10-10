# Roadmap: layer by layer

Each layer has a goal, what we build, and how we know it's done. We don't start the next until the current one works.

## Layer 0: Foundation
- **Goal:** repo set up, we know our tools.
- **Do:** add docs, install Python, test the mic and headphones on the laptop.
- **Done when:** a Python script records 3 seconds from the mic and plays it back.

## Layer 1: Pitch to note (laptop, Python)
- **Goal:** prove the core idea in the easiest place.
- **Do:** track pitch from the mic (YIN algorithm), play a synth note that follows it, snap it to a scale.
- **Done when:** you whistle and hear a musical note follow you, and you can change the key.
- **Also:** write a simple latency test and record the number.

## Layer 2: Make it a real engine (Rust)
- **Goal:** move the working idea into fast, safe code.
- **Do:** rewrite pitch tracking, synth, and scale snapping as a Rust crate in `core/`. It only handles audio buffers, no devices. Test with recorded WAV files. Then add a Windows live-mic demo with cpal.
- **Done when:** the Rust engine gives the same notes as the Python sketch on test files, and the Windows demo runs live.

## Layer 3: Android demo
- **Goal:** run it on a phone.
- **Do:** Kotlin app calls the Rust engine through UniFFI. Try both Oboe and cpal for mic-to-headphone audio. Keep whichever has the lower measured delay.
- **Done when:** whistle into the phone, hear the note, and we know the delay in ms.

## Layer 4: Fit the music
- **Goal:** notes match the song, not just a preset scale.
- **Do:** detect the key/tempo of music playing, or let the user pick. Quantize notes to the beat.
- **Done when:** a siren-like sound becomes a note that sounds right with a sample song.

## Layer 5: Sound types
- **Goal:** know *what* the sound is.
- **Do:** use an existing small sound-classification model. Don't train our own yet.
- **Done when:** the app labels siren, speech, vehicle, drill with reasonable accuracy on test clips.

## Layer 6: Mixer screen
- **Goal:** the user chooses which sounds trigger what.
- **Do:** simple sliders per sound type. Include the **safety floor**: some sounds can't go to zero.
- **Done when:** a friend can use it without help.

## Layer 7: Body signals (optional)
- **Goal:** heart rate shapes the music.
- **Do:** start with live heart rate only (Android, standard Bluetooth heart rate bands). HRV later.
- **Done when:** music tempo/tone shifts smoothly when heart rate changes.

## Layer 8: Package as a library
- **Goal:** other apps can use reSync.
- **Do:** clean interface, docs, examples, an Android library (AAR), maybe a desktop plugin.
- **Done when:** a tiny sample app uses reSync in under 20 lines.

## Layer 9: iOS and more
- Swift wrapper around the same C++ core. Then whatever people ask for.

## Later ideas (not now)
Business model, hardware, partnerships. They only matter after the engine is good.
