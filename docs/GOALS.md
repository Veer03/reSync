# Goals

## The big dream (long term)
Make people's everyday sounds feel good. The world around you becomes part of your music instead of something you fight.

## What reSync is
A **software engine** (a library) that any app or feature can use:
- a music app
- a headphone companion app
- a game
- a wellness or focus app
- a plugin for audio tools

We also build one small **demo app** (Android first) so people can try it.

## Right now (v1): the smallest real version

> The phone microphone hears a sound with a clear pitch (a whistle, a siren, a horn). The app plays a musical note that follows it, locked to a musical key, mixed over the music. Everything runs on the device.

### v1 success checklist
- [ ] Whistle into the mic and hear a synth note follow the pitch (laptop, Python)
- [ ] Notes snap to a chosen scale (like C major) so they always sound musical
- [ ] Delay measured and written down
- [ ] Same thing running on an Android phone
- [ ] Delay on phone under about 40 ms with wired or phone-speaker output (stretch: 20 ms)

## Not v1 (parked, not forgotten)
- Recognizing sound types (siren, voice, drill)
- Mixer screen
- Heart rate / smartwatch
- iOS
- Marketplace, hardware, business ideas
- Removing or replacing real sound perfectly in sync

## Rules we keep
1. On-device only. No cloud. No data leaves the phone.
2. Safety first. Important sounds are never fully hidden.
3. Open source and built in public.
4. Small layers. Each one works before we start the next.
