# Decisions

Format: what we chose, why, and what would change our mind.

## D1: Software and library first, no hardware
- **Why:** hardware is slow, expensive, and risky. A library can be added to any app or feature.
- **Change if:** the software works well and people ask for a device.

## D2: Android first
- **Why:** Android allows low-level audio through Oboe/AAudio, and we can test directly on a phone. iOS limits some things and needs a Mac for builds.
- **Change if:** most of our testers and friends use iPhones.

## D3: Languages (updated: Rust core)
- **Rust for the engine.** Reasons:
  1. The compiler catches memory bugs that crash audio apps. Most code is AI-written, so this safety net matters.
  2. One codebase builds for Android, iOS, Windows, and Linux.
  3. UniFFI (Mozilla) generates Kotlin and Swift wrappers automatically. Its docs call it ready for production, though it isn't 1.0 yet.
  4. A safe library is easier for other apps to trust and embed.
- **Honest downsides of Rust:**
  1. Windows setup needs Microsoft C++ build tools.
  2. Android builds need extra setup (NDK targets).
  3. Most audio examples, Faust output, and TFLite samples are C++, so we'll translate or wrap some.
  4. Rust does not stop us from blocking the audio thread. We must still follow the real-time rules in AGENTS.md.
- **Kotlin for the Android app.** Google's standard.
- **Python for sketching only.** About 100 lines to hear if the idea sounds good, then we port it. It is a sketchpad, not an alternative to Rust.
- **Swift later** for iOS.
- **C++ stays available** as a fallback. Oboe is C++ and may be our device I/O layer on Android.

### Design rule: the engine does no device I/O
- The Rust engine only does math: `process(input_buffer) -> output_buffer`.
- Each platform shell (Android, Windows, iOS) handles mic and speaker.
- Why: testable on WAV files, portable everywhere, and swapping the I/O layer (Oboe vs cpal) is easy if latency is bad.
- cpal supports Android through AAudio, but its docs give no Android latency numbers. Oboe is Google's recommended path. We measure both in Layer 3.
- Neural models (Layer 5): tract (Sonos) loads ONNX models in Rust, but its Android support is not stated in its docs. We test before relying on it. Fallback: TFLite through a C++ shim.

## D4: Change the latency target
- **Old:** under 10 ms round trip.
- **New:** measure first. Aim for under 40 ms on Android with wired or speaker output. Stretch: 20 ms.
- **Why:** Google says 20 ms is the pro-audio requirement and 10 ms is a long-term goal. Average phones were around 39 ms in 2021. Classic Bluetooth is 100-300 ms; LE Audio is about 20-30 ms in one direction.
- **Change if:** our measurements show we can do better.

## D5: Add to the music, don't replace real sound in sync
- **Why:** replacing real sound with no delay is not possible on phones today. If the user's headphones block the world (passive or noise cancelling), we can add music that *reacts* to sounds, and small delay doesn't matter.
- **Change if:** we find a way to make real-sound replacement work.

## D6: Safety floor
- **Rule:** the mixer never allows full silence for critical sounds (sirens, horns, approaching vehicles).
- **Why:** people use headphones while walking and cycling.

## D7: Don't train our own AI yet
- **Why:** use pre-trained models first. Training takes data, time, and money.
- **Change if:** existing models don't meet our needs.

## D8: License (Apache-2.0, accepted for now)
- **Chosen:** Apache-2.0. Anyone, including companies, can use it. Fits the goal of "used everywhere."
- **Alternative:** GPL-3.0. Forks must stay open. More protective, less likely to be adopted by apps.
- **Check:** any library we copy from must be compatible with Apache-2.0. GPL/AGPL code can't be copied in.
- **Status:** accepted 2026-10-10. Revisit before the first public release.

## D9: Latency log
| Date | Setup | Round-trip (ms) | Notes |
|------|-------|-----------------|-------|
| (empty) | | | |
