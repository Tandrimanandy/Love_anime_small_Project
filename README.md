<div align="center">

# Love Video Generator

**An interactive particle-animation studio for creating personalized romantic videos in the browser.**

Built with React, TypeScript, Vite, HTML5 Canvas, and the Web Audio API.

</div>

---

## Functions Used in the Code

A quick reference to the main functions and browser APIs that power each part of the project.

<table>
<tr>
<td width="50%" valign="top">

**Particle Rendering Engine**
<sub>`src/components/VideoCanvas.tsx`</sub>

<ul>
<li><code>sampleTextPoints()</code> converts slide text into particle target points</li>
<li><code>sampleHeartPoints()</code> generates the heart-shaped point set using the parametric heart curve</li>
<li><code>triggerSlideTransition()</code> re-targets particles when a scene changes</li>
<li><code>reinitializeParticles()</code> resets the particle system</li>
<li><code>setupMatrixRain()</code> builds the digital-rain background streams</li>
<li><code>getTraceXAtY()</code> interpolates the path of each rain trace</li>
<li><code>drawTinyHeart()</code> draws heart glyphs on the canvas</li>
<li><code>resizeCanvas()</code> keeps the canvas responsive to window size</li>
<li><code>render()</code> runs the main animation loop through <code>requestAnimationFrame</code></li>
</ul>

</td>
<td width="50%" valign="top">

**Playback and Recording Controls**
<sub>`src/components/VideoCanvas.tsx`</sub>

<ul>
<li><code>play()</code> and <code>pause()</code> control playback state</li>
<li><code>restart()</code> resets the timeline and particles</li>
<li><code>seekToSlide()</code> jumps to a specific scene</li>
<li><code>startRecording()</code> and <code>stopRecording()</code> control video capture</li>
<li><code>startCanvasRecording()</code> uses <code>canvas.captureStream()</code> with <code>MediaRecorder</code></li>
<li><code>stopCanvasRecording()</code> finalizes the WebM file and triggers the download</li>
<li><code>useImperativeHandle()</code> exposes these methods to the parent component</li>
</ul>

</td>
</tr>
<tr>
<td width="50%" valign="top">

**User Interaction**
<sub>`src/components/VideoCanvas.tsx`</sub>

<ul>
<li><code>handleMouseMove()</code> tracks the pointer for the repel and attract force</li>
<li><code>handleMouseLeave()</code> clears the pointer position</li>
<li><code>handleCanvasClick()</code> spawns hearts and word bursts on click</li>
</ul>

</td>
<td width="50%" valign="top">

**Procedural Audio Synthesizer**
<sub>`src/utils/audio.ts`</sub>

<ul>
<li><code>initCtx()</code> creates and resumes the <code>AudioContext</code></li>
<li><code>playTick()</code> plays the countdown tick</li>
<li><code>playHeartbeat()</code> plays the double-thump heartbeat</li>
<li><code>playTransitionChord()</code> plays the chime between scenes</li>
<li><code>playSparkle()</code> and <code>playEnvelopeOpen()</code> play the intro sound effects</li>
<li><code>playMusicBoxNote()</code> renders a single music-box note</li>
<li><code>startBackgroundMusic()</code> and <code>stopBackgroundMusic()</code> manage the looping arpeggio</li>
<li><code>isBgmPlaying()</code> reports background music state</li>
</ul>

</td>
</tr>
<tr>
<td width="50%" valign="top">

**Application Shell and State**
<sub>`src/App.tsx`</sub>

<ul>
<li><code>handlePlay()</code>, <code>handlePause()</code>, <code>handleRestart()</code> drive playback</li>
<li><code>handleStartRecord()</code> and <code>handleStopRecord()</code> drive recording</li>
<li><code>handleSeek()</code> and <code>handleTimelineUpdate()</code> keep the timeline in sync</li>
<li><code>handleOpenEnvelope()</code> runs the envelope intro sequence</li>
<li><code>applyMessagePreset()</code> loads message presets (Bengali, anniversary, retro)</li>
<li><code>useState()</code>, <code>useRef()</code>, <code>useEffect()</code> manage state and audio synchronization</li>
</ul>

</td>
<td width="50%" valign="top">

**Customization Panel**
<sub>`src/components/Controls.tsx`</sub>

<ul>
<li><code>setConfigValue()</code> updates any single configuration value</li>
<li><code>applyPreset()</code> applies a color theme from <code>PRESET_THEMES</code></li>
<li><code>addSlide()</code> and <code>deleteSlide()</code> manage the scene list</li>
<li><code>updateSlideText()</code> and <code>updateSlideDuration()</code> edit individual scenes</li>
</ul>

</td>
</tr>
<tr>
<td width="50%" valign="top">

**Data Model and Themes**
<sub>`src/types.ts`</sub>

<ul>
<li><code>Slide</code> interface for a single text scene</li>
<li><code>VideoConfig</code> interface for all animation settings</li>
<li><code>PRESET_THEMES</code> object containing five color themes</li>
</ul>

</td>
<td width="50%" valign="top">

**Standalone Fallback**
<sub>`index.html`</sub>

<ul>
<li><code>initStandaloneApp()</code> bootstraps the no-build version</li>
<li><code>tick()</code> runs the fallback animation loop</li>
<li><code>sampleTextPoints()</code> and <code>sampleHeartPoints()</code> mirror the React engine</li>
<li><code>triggerSlideTransition()</code> handles scene changes</li>
<li><code>initAudio()</code>, <code>playTick()</code>, <code>playHeartbeat()</code>, <code>playTransitionChord()</code>, <code>playSparkle()</code> provide audio</li>
</ul>

</td>
</tr>
</table>

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Available Scripts](#available-scripts)
- [Usage](#usage)
- [Configuration](#configuration)
- [Color Themes](#color-themes)
- [Recording and Export](#recording-and-export)
- [Browser Support](#browser-support)
- [Known Limitations](#known-limitations)
- [Contributing](#contributing)
- [License](#license)

---

## Overview

Love Video Generator is a client-side web application that turns a short sequence of words into a cinematic particle animation. Thousands of glowing particles form each word, dissolve into the next, and finally assemble into a pulsing heart with a personalized message, all over a digital-rain background and a synthesized soundtrack.

The application runs entirely in the browser. It requires no external services, and all sound is generated in real time with the Web Audio API. Finished animations can be recorded and saved as a WebM video file.

## Features

- Particle text morphing: each slide is rendered as a set of particles that animate into the shape of the word
- Heart finale: particles assemble into a pulsing heart with a main message and a sub-caption
- Digital rain background with four character sets: romantic, binary, code, and standard
- Interactive particles that repel or attract based on cursor position, plus click-triggered hearts and word bursts
- Envelope introduction that starts playback when the viewer opens it
- Five built-in color themes, each with its own background, glow, and rain colors
- Procedural audio: countdown ticks, heartbeat, transition chords, and a looping music-box melody, with no audio files required
- One-click video recording to a downloadable WebM file
- Configurable slide text, slide duration, particle density, glow strength, rain speed, and heartbeat rate
- Standalone fallback page in `index.html` that runs without a build step

## Technology Stack

| Category | Technology |
|---|---|
| Framework | React 19 |
| Language | TypeScript 5.8 |
| Build Tool | Vite 6 |
| Styling | Tailwind CSS 4 |
| Rendering | HTML5 Canvas 2D API |
| Audio | Web Audio API |
| Video Capture | MediaRecorder API and `canvas.captureStream()` |
| Icons | lucide-react |

## Project Structure

```
.
├── index.html                    # Entry page, includes standalone fallback animation
├── package.json                  # Dependencies and scripts
├── vite.config.ts                # Vite and Tailwind configuration
├── tsconfig.json                 # TypeScript configuration
├── metadata.json                 # Application metadata
├── .env.example                  # Example environment variables
└── src/
    ├── main.tsx                  # React entry point
    ├── App.tsx                   # Application shell, state, and envelope intro
    ├── types.ts                  # Slide and VideoConfig types, PRESET_THEMES
    ├── index.css                 # Global styles and font imports
    ├── components/
    │   ├── VideoCanvas.tsx       # Canvas rendering engine and recording
    │   └── Controls.tsx          # Customization panel component
    └── utils/
        └── audio.ts              # Web Audio API synthesizer
```

## Getting Started

### Prerequisites

- Node.js 18 or later
- npm (included with Node.js)

### Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/<your-username>/<repository-name>.git
   cd <repository-name>
   ```

2. Install dependencies:

   ```bash
   npm install
   ```

3. Start the development server:

   ```bash
   npm run dev
   ```

4. Open `http://localhost:3000` in your browser.

## Available Scripts

| Command | Description |
|---|---|
| `npm run dev` | Starts the Vite development server on port 3000 |
| `npm run build` | Creates an optimized production build in `dist/` |
| `npm run preview` | Serves the production build locally |
| `npm run lint` | Runs the TypeScript compiler in type-check mode |
| `npm run clean` | Removes the `dist` folder (requires a Unix-style shell) |

## Usage

1. Open the application in a browser.
2. Click the wax seal on the envelope to begin. Audio playback starts at this point because browsers require a user interaction before sound can play.
3. Watch the countdown, the word sequence, and the heart finale.
4. Move the cursor over the particles to repel them, and click the canvas to release hearts.

## Configuration

Default settings are defined in the `DEFAULT_CONFIG` object in `src/App.tsx` and follow the `VideoConfig` interface in `src/types.ts`.

| Property | Type | Description |
|---|---|---|
| `slides` | `Slide[]` | Ordered list of scenes, each with `text` and `duration` in seconds |
| `heartText` | `string` | Main message shown inside the heart |
| `heartSubText` | `string` | Caption shown beneath the heart |
| `particleCount` | `number` | Maximum number of active particles |
| `particleSize` | `number` | Base particle size in pixels |
| `glowStrength` | `number` | Glow radius in pixels |
| `interactiveForce` | `'repel' \| 'attract' \| 'none'` | Cursor interaction mode |
| `interactiveRadius` | `number` | Cursor influence radius in pixels |
| `heartPulseRate` | `number` | Seconds per heart pulse |
| `matrixDensity` | `number` | Rain stream density, from 0.1 to 1.0 |
| `matrixSpeed` | `number` | Rain fall speed multiplier |
| `matrixChars` | `'binary' \| 'standard' \| 'romantic' \| 'code'` | Rain character set |
| `matrixCharSize` | `number` | Rain character size in pixels |
| `enableSoundEffects` | `boolean` | Master switch for all audio |
| `enableBackgroundMusic` | `boolean` | Toggles the looping music-box melody |
| `enableHeartbeat` | `boolean` | Toggles the heartbeat sound |

To change the message, edit the `slides`, `heartText`, and `heartSubText` values in `DEFAULT_CONFIG`.

Example:

```ts
slides: [
  { id: 's_1', text: '3', duration: 1.0 },
  { id: 's_2', text: '2', duration: 1.0 },
  { id: 's_3', text: '1', duration: 1.0 },
  { id: 's_4', text: 'Happy', duration: 1.8 },
  { id: 's_5', text: 'Birthday', duration: 2.4 },
],
heartText: 'Happy Birthday',
heartSubText: 'With all my love',
```

## Color Themes

Themes are defined in `PRESET_THEMES` in `src/types.ts`.

| Theme | Rain Character Set |
|---|---|
| Pink Magenta (Original) | romantic |
| Crimson Passion | binary |
| Cyber Purple | code |
| Emerald Dream | standard |
| Sunset Gold | romantic |

## Recording and Export

The recording feature captures the canvas at 30 frames per second using `canvas.captureStream()` and `MediaRecorder`. The codec is selected in this order, depending on browser support: VP9, VP8, then the default WebM codec. When recording stops, the file is downloaded automatically as `romantic_particles_<timestamp>.webm`.

The recording contains the canvas video only. Synthesized audio is not embedded in the exported file.

## Browser Support

The application requires a modern browser with support for Canvas 2D, the Web Audio API, and the MediaRecorder API. Recent versions of Chrome, Edge, and Firefox are recommended. Safari support for WebM recording may be limited.

## Known Limitations

- Exported WebM files do not include audio.
- Audio starts only after the first user interaction, due to browser autoplay policies.
- Very high particle counts may reduce frame rate on low-powered devices.
- The `clean` script uses `rm -rf` and will not work in a Windows Command Prompt without a compatible shell.

## Contributing

Contributions are welcome.

1. Fork the repository.
2. Create a feature branch: `git checkout -b feature/your-feature-name`
3. Commit your changes: `git commit -m "Add your feature"`
4. Push to the branch: `git push origin feature/your-feature-name`
5. Open a pull request describing the change.

## License

Distributed under the MIT License. Add a `LICENSE` file to the repository root to make the terms explicit.
