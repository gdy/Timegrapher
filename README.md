# Watch Timegrapher

A single-file web app that measures mechanical watch accuracy using your phone's microphone or uploaded audio recordings. Reports rate in seconds/day (s/d), beat error, and amplitude.

**[Open the app](https://gdy.github.io/Timegrapher)**

## How to use

### Live microphone
1. Open in Safari (iOS) or any desktop browser
2. Place the watch caseback against your phone's microphone
3. Tap **Start Microphone** and wait 10–30 seconds
4. Results update in real time

### Audio file upload
1. Record 15–30 seconds of your watch ticking (voice memo, etc.)
2. Tap **Upload Audio** and select one or more files
3. Results appear with rate, beat error, and tick count

## Features

- Real-time tick detection and rate calculation
- Multi-file upload for comparing multiple watches
- Adaptive thresholding with per-window noise floor estimation
- Hodges-Lehmann estimator for tick-tock bias correction in longer recordings
- Beat error measurement from consecutive interval pairs
- Copy-paste friendly results log
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
- A quiet environment helps, but the adaptive algorithm handles moderate background noise
- Longer recordings (30s) give more stable results
- Compare multiple recordings to confirm consistency

## Tech

Single HTML file using the Web Audio API. High-pass IIR filter at 300 Hz, peak detection with sub-sample energy centroid refinement, iterative median with outlier rejection, windowed analysis with quality-weighted aggregation for longer recordings.
