# Beat Lab

A single-page tool that analyzes an audio file and returns its **tempo (BPM)** and **musical key** — entirely in the browser, no server or backend required.

Built as a portfolio piece for [NORTHHHERN LABS](https://northhhh-dev.vercel.app), pairing dev skills with music production.

## Features

- 🎧 Drag-and-drop or tap-to-browse audio upload (MP3, WAV, M4A)
- ⏱️ **BPM detection** — energy-envelope onset detection + autocorrelation
- 🎹 **Key detection** — Goertzel-algorithm chroma extraction, matched against Krumhansl-Schmuckler major/minor key profiles
- No uploads, no backend — audio is decoded and analyzed client-side with the Web Audio API and never leaves the device

## How it works

1. **Decode** — the uploaded file is decoded into raw PCM audio via `AudioContext.decodeAudioData`.
2. **Tempo** — the signal is broken into 10ms frames to build an energy envelope; onset strength (frame-to-frame energy increase) is computed, then autocorrelated across a 60–180 BPM lag range to find the dominant beat interval.
3. **Key** — a ~6 second window is analyzed with the Goertzel algorithm at each of the 12 pitch classes across several octaves, producing a chroma vector. That vector is correlated against major and minor key profiles to pick the best-matching key.

## Tech

Plain HTML/CSS/JS — no frameworks, no build step, no dependencies. Fonts pulled from Google Fonts (Big Shoulders Display, JetBrains Mono).

## Usage

Open `beat-lab.html` in any modern browser, or drop it into a static site (e.g. Vercel, Netlify, GitHub Pages) — it works as a standalone file.

## Limitations

Tempo and key detection use lightweight signal-processing heuristics rather than a trained model, so results are estimates — solid for quick reference, not lab-grade precision.

---
Part of the [NORTHHHERN LABS](https://northhhh-dev.vercel.app) portfolio · built by [Northhh](https://x.com/Northhh_zzz)
