# Watch Timegrapher

A single-file web app that measures mechanical watch accuracy using your phone's microphone or uploaded audio recordings. Reports rate in seconds/day (s/d) with an uncertainty, beat error, and amplitude.

**[Open the app](https://gdy.github.io/Timegrapher)**

## How to use

### Live microphone
1. Open in Safari (iOS) or any desktop browser
2. Pick the watch's beat rate (and its lift angle, if you want amplitude)
3. Place the watch caseback against your phone's microphone
4. Tap **Start Microphone** — results appear after 5 seconds and keep refining over the most recent 30 seconds

### Audio file upload
1. Record 15–30 seconds of your watch ticking (voice memo, etc.)
2. Tap **Upload Audio** and select one or more files
3. Results appear with rate, beat error, and amplitude

## Features

- Rate with a quoted uncertainty (typically ±0.2–0.4 s/d from a 15–30 s phone recording)
- Beat error and amplitude measured from the averaged tick/tock pattern
- Timing trace like a bench timegrapher: one dot per beat, tick and tock as two lines
- Warns when the beat pattern doesn't fit the selected beat rate, and names the rate it does fit
- Ignores bumps, handling noise and stretches with no watch on the mic
- Multi-file upload for comparing watches, with a copy-paste friendly results log
- Works on iOS Safari, Chrome, Firefox, and desktop browsers
- No server, no dependencies — everything runs client-side in a single HTML file

## Supported beat rates

- 18,000 BPH (2.5 Hz)
- 21,600 BPH (3 Hz)
- 25,200 BPH (3.5 Hz)
- **28,800 BPH (4 Hz)** — default
- 36,000 BPH (5 Hz)

## Tips for accurate readings

- Place the caseback flat against the microphone — direct contact gives the best signal
- Keep the watch still: position changes shift the rate, and the reading averages over them
- Longer recordings give a tighter rate; amplitude needs a reasonably strong signal and shows `--` when the faint first sound of each beat can't be picked out
- Amplitude depends on the lift angle setting. Most movements are 50–52°, but some differ by enough to matter, so look up your calibre
- Beat error is the standard timegrapher figure: half the difference between the tick-to-tock and tock-to-tick intervals
- The quoted ± covers the measurement only. The phone's own audio clock is typically good to a few seconds per day, which no recording length can improve

## Tech

Single HTML file using the Web Audio API. A phone recording is too noisy to time ticks one by one, so the energy envelope of the tick band (above 2 kHz) is folded at the watch's period: hundreds of beats stack into one clean average beat pattern. A search over period finds the fold that is sharpest; tracking that pattern's phase through the recording and fitting a robust line gives the rate and its uncertainty. The averaged pattern shows the escapement's separate sounds, so beat error comes from the offset between the tick and tock patterns, and amplitude from the time between the first sound (unlocking) and the last (drop) together with the lift angle.
