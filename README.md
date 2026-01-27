# fs-simpwave

A simple waveform synthesizer for [FunctionServer](https://functionserver.com). Classic subtractive synthesis with ADSR envelope and lowpass filter.

## Features

- **4 Waveforms**: Sine, triangle, sawtooth, and square
- **ADSR Envelope**: Attack, decay, sustain, release controls
- **Lowpass Filter**: Cutoff frequency and resonance
- **Sub Oscillator**: One octave down for bass reinforcement
- **Detune**: Subtle pitch variation for thickness
- **MIDI Input**: Receives notes from Joy, Deepwave Gold, or any MIDI source
- **MIDI Playback**: Load and play .mid files
- **Visual Feedback**: Real-time waveform display

## Installation

### As FunctionServer System App

Copy `simpwave.js` to the FunctionServer `core/apps/` directory.

### Standalone

```javascript
// Load in FunctionServer
import { Simpwave } from 'fs-simpwave';
```

## MIDI Channel

Simpwave registers as `simpwave` on both:
- `window._algoChannels` (legacy)
- `ALGO.pubsub` (recommended)

### Sending Notes

```javascript
// Via pubsub
ALGO.pubsub.publish('simpwave', {
  type: 'noteOn',
  note: 60,
  velocity: 100,
  duration: 0.4
});

// Via _algoChannels
window._algoChannels['simpwave'].callback({
  type: 'noteOn',
  note: 60,
  velocity: 100
});
```

## Parameters

### Envelope (ADSR)

| Parameter | Range | Default | Description |
|-----------|-------|---------|-------------|
| Attack | 1-1000ms | 10ms | Time to reach peak |
| Decay | 1-1000ms | 100ms | Time to reach sustain |
| Sustain | 0-100% | 70% | Sustained level |
| Release | 1-1000ms | 200ms | Fade out time |

### Filter & Mix

| Parameter | Range | Default | Description |
|-----------|-------|---------|-------------|
| Cutoff | 100-8000Hz | 2000Hz | Filter frequency |
| Resonance | 0-20 | 1 | Filter emphasis |
| Sub | 0-100% | 30% | Sub oscillator level |
| Detune | 0-50 cents | 5ct | Pitch variation |

## Waveforms

| Waveform | Icon | Character |
|----------|------|-----------|
| Sine | 〜 | Pure, mellow |
| Triangle | △ | Soft, flute-like |
| Sawtooth | ⩘ | Bright, buzzy |
| Square | ⊓ | Hollow, clarinet-like |

## Integration with Joy

Simpwave is the default synth for Joy's second lane. Route notes by selecting the SW lane in Joy's session view.

## License

MIT

## Acknowledgments

- Built for [FunctionServer](https://functionserver.com)
- Works with [Joy](https://github.com/williamsharkey/fs-joy) pad controller
- Built with [Claude Code](https://claude.ai/code)
