# Prototype (Layer 1)

Goal: whistle into the laptop mic, hear a synth note follow your pitch.

## Files to create (in this order)
1. `01_record_play.py`: record 3 seconds, play it back (tests mic + speakers)
2. `02_pitch_file.py`: find the pitch of a recorded whistle (YIN)
3. `03_live_pitch.py`: print the pitch from the live mic
4. `04_pitch_to_note.py`: snap pitch to a scale and play a synth note
5. `05_latency_test.py`: measure delay and log it in `../docs/DECISIONS.md`

## Setup (when we start)
```
python -m venv .venv
source .venv/bin/activate      # Windows: .venv\Scripts\activate
pip install numpy sounddevice
```

## Tip
Use headphones to avoid the mic hearing the speakers (feedback squeal).
