# Channel Vocoder

A single-file interactive channel vocoder built with the Web Audio API.

## Overview

A channel vocoder analyses a **modulator** signal (typically voice) by splitting it into frequency bands, extracting the amplitude envelope of each band, and using those envelopes to shape a **carrier** signal (typically a harmonically rich waveform like a sawtooth). The result is the carrier "speaking" with the spectral shape of the modulator — the classic robot voice effect.

## Features

### Vocoder Engine
- 8, 16, 24, or 32 band filter bank with adjustable Q factor
- Per-band: bandpass filter, envelope follower, VCA controlling the corresponding carrier band
- Configurable band spacing (linear or logarithmic)
- Frequency range: 80 Hz to 8 kHz
- Adjustable attack and release times for envelope followers

### Modulator Sources
- **Microphone** — real-time voice input
- **Audio file** — upload any audio file as the modulator

### Carrier Types
- **Sawtooth** — the classic vocoder carrier, harmonically rich
- **Square wave** — hollow, nasal character
- **Pulse wave** — adjustable pulse width for timbral variation
- **White noise** — breathy whisper effect
- **Pink noise** — warmer whisper with rolled-off highs
- **Chord** — multiple detuned sawtooth oscillators with selectable voicing (Major, Minor, 7th, Sus4, 5th)
- **External file** — upload any audio file as the carrier

### Presets
| Preset | Description |
|--------|-------------|
| Robot Voice | Sawtooth carrier, fast envelopes — classic vocoder |
| Whisper | White noise carrier, breathy effect |
| Choir | Chord carrier, slow envelopes — lush pad |
| Talk Box | Square wave carrier, nasal and bold |
| Ambient Pad | Slow envelopes, wide bands, minor chord |
| Crisp Digital | 32 bands, very tight envelopes |
| Pink Haze | Pink noise carrier, warm whisper |
| Pulse Width | Narrow pulse wave carrier |

### Visualisation
- Real-time band-level meters showing envelope follower output per band
- Modulator input spectrum
- Output spectrum
- Output waveform display

### Recording
- Record the vocoder output
- Play back recordings in the browser

## Controls

| Parameter | Range | Description |
|-----------|-------|-------------|
| Bands | 8 / 16 / 24 / 32 | Number of filter bands |
| Spacing | Linear / Log | Frequency distribution of bands |
| Attack | 1–100 ms | Envelope follower attack time |
| Release | 10–500 ms | Envelope follower release time |
| Frequency | 40–440 Hz | Carrier oscillator base frequency |
| Pulse Width | 5–95% | Duty cycle for pulse wave carrier |
| Chord Voicing | Maj / Min / 7th / Sus4 / 5th | Chord intervals for chord carrier |
| Dry/Wet | 0–100% | Blend between original modulator and vocoder output |
| Output Gain | -24 to +12 dB | Master output level |
| Q Factor | 1–20 | Bandpass filter resonance |

## Usage

1. Open `index.html` in a modern browser (Chrome, Firefox, Edge)
2. Click **Start** to initialise the audio engine (grants microphone access)
3. Select a preset or configure parameters manually
4. Speak into your microphone — the vocoder processes your voice in real-time
5. Experiment with different carrier types and envelope settings
6. Use **Record** to capture the output, **Play Rec** to listen back

## Technical Details

- Single HTML file, no build step or dependencies
- Uses Web Audio API: `BiquadFilterNode` (bandpass filters), `GainNode` (VCAs), `AnalyserNode` (visualisation and envelope detection)
- Envelope following computed per-frame using RMS analysis of each band's time-domain data
- Pink noise generated using the Voss-McCartney algorithm
- Pulse wave synthesised via Fourier series (`PeriodicWave`)
- Visual style matches the companion Physical Modelling Synth application

## Browser Requirements

- Modern browser with Web Audio API support
- Microphone access (for voice input)
- Recommended: Chrome or Firefox for best audio performance
