# Research notes

Status key: **verified** = we checked a real source. **unverified** = from memory, must check before using.
License is the first thing to check. Our proposed license is Apache-2.0 (see DECISIONS.md), so some licenses (GPL, AGPL) can limit what we can copy in.

## Rust ecosystem
| Tool | What it does | Status | Notes |
|------|--------------|--------|-------|
| cpal | Rust audio I/O (mic/speakers) | verified exists | Supports Android via AAudio (Rust 1.85+, Android 8+). Has a `realtime` feature. Docs give no Android latency numbers: we must measure. |
| UniFFI (Mozilla) | Generates Kotlin/Swift/Python wrappers from Rust | verified exists | Called production-ready by its authors, not yet 1.0. Used in Firefox. |
| tract (Sonos) | Runs ONNX models in Rust | verified exists | Android support not stated in its docs. Test before use. |
| oboe-rs (Rust wrapper for Oboe) | Oboe from Rust | unverified | Check it exists and is maintained. |
| Rust DSP crates (fundsp, dasp, pitch detection crates) | Building blocks for synth and pitch | unverified | Check maintenance and licenses. |

## Audio on Android
| Tool | What it does | Status | Notes |
|------|--------------|--------|-------|
| Oboe (Google) | Low-delay audio on Android, wraps AAudio | verified exists | Google's docs say to request low-latency mode, exclusive sharing, and 48 kHz. Check license (believed Apache-2.0). |
| AAudio | Android's native audio API | verified exists | Oboe uses it on Android 8.1+. |

## Pitch tracking
| Tool | What it does | Status | Notes |
|------|--------------|--------|-------|
| YIN algorithm | Classic, simple pitch detector | unverified | Small enough to write ourselves. Good first choice. |
| pYIN | Improved YIN, smoother | unverified | Also in librosa (Python). |
| aubio | C library with pitch detection | unverified | Believed GPL: may limit us. Check. |
| librosa (Python) | Audio analysis in Python | unverified | Good for experiments only. |

## Making sound (synth)
| Tool | What it does | Status | Notes |
|------|--------------|--------|-------|
| Faust | Write synths in a small language, compile to C++ | unverified | Check license of generated code. |
| FluidSynth | Plays instruments from SoundFont files | unverified | Check license; lets us do "cello" sounds. |
| Pure Data / libpd | Visual audio patching | unverified | Fast for experiments. |
| Our own simple synth | Sine/saw/square wave + envelope | n/a | Start here. About 50 lines. |

## Sound recognition
| Tool | What it does | Status | Notes |
|------|--------------|--------|-------|
| YAMNet | Pre-trained model, 500+ sound classes | unverified | Runs with TensorFlow Lite. Check license and model size. |
| TensorFlow Lite / LiteRT | Run small models on phones | unverified | Check current name and Android support. |

## Heart rate / watches (later)
| Tool | What it does | Status | Notes |
|------|--------------|--------|-------|
| Gadgetbridge | Android app that talks to many watches | verified exists | Android only. HRV support depends on device. Believed AGPL: do not copy code. |
| Standard Bluetooth Heart Rate profile | Many chest straps/bands send live HR this way | unverified | Likely the easiest first source. |

## Things from the old README to treat carefully
- "OpenDSP": exists, but it's a Raspberry Pi/PC audio distro, not a phone library.
- "SoundXRouter": **could not find it.** Don't use until we find a real source.
- JUCE: real and popular, but its license is dual (open source copyleft or paid). Check before choosing.
- Neural Amp Modeler: real project, useful as inspiration for neural audio in real time.

## Questions to research next
1. What's the real round-trip delay on the actual test phone with wired earbuds?
2. How does Android let an app use the mic and output audio at the same time in the background?
3. Which license do our must-have libraries use?
4. How do other apps on Android apply effects to audio from other apps (system-wide)? What are the limits?
