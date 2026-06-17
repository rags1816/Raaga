# Changelog

All notable changes to Raaga Studio Pro are documented here.
Format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

---

## [v5.0.0] — 2026-06-17

### Added — Real Instrument Samples
- 18 real WAV sample instruments replacing oscillator-only synthesis
- Sample instruments: Sitar, Sarod, Veena, Bansuri, Shehnai, Harmonium, Violin,
  Saxophone, Trumpet, Grand Piano, Church Organ, Acoustic Guitar, Electric Guitar,
  Tabla, Dholak, Conga, Bongos, Octopad
- HTML5 Audio (`new Audio()`) engine — works on `file://` protocol, all WAV formats
- Synth fallback for every instrument if WAV file missing
- Instrument selectors grouped with ★ Real Sample indicators

### Added — Complete AI Integration
- **AI Hub** tab — dedicated panel for all AI features
- **Admin Panel** — API key management for Claude (Anthropic) and Gemini (Google)
- AI features on/off toggles per feature with purple badge styling
- AI status pill in header showing when features are active
- localStorage-only key storage — zero keys in source code

### Added — 11 AI Features (fully functional)
1. 🧘 **AI Guru Chat** — conversational Indian classical music teacher
2. 🔍 **Raaga Identifier** — identifies raagas from note sequences
3. 🕰 **Raaga Historian** — full history, scale, vadi, famous recordings
4. 📜 **Lyrics Translator** — bandish/bhajan translation and explanation
5. 🎵 **Bandish Composer** — original compositions for any raaga + taal
6. 📋 **Lesson Plan** — personalised practice plan based on XP level
7. 📊 **Session Feedback** — AI scores practice sessions
8. 🎓 **Raaga Tutor** — live note checking against raaga grammar rules
9. 🏛 **Gharana Analyser** — identifies playing style by gharana
10. 🎤 **Pitch Detector** — real-time mic-based swara detection with cents deviation
11. 🎙 **Sing-Along Judge** — accuracy scoring while singing target notes

### Added — Complete Laptop Keyboard Mapping (all 3 octaves)
- Mandra Saptak: `Z X C V B N M ,`
- Madhya Saptak: `A S D F G H J K` (unchanged)
- Taar Saptak:   `I O L 9 0 - = ]`
- All octave keyboards now light up correctly on laptop key press

### Fixed
- Taar Saptak keys now play correctly (octave 2 WAV files used)
- Mandra Saptak plays at correct pitch (0.5× playback rate via AudioBuffer)
- Key highlight DOM IDs fixed (was double-suffixing `_low_low`)
- Zipper noise eliminated — removed setInterval volume stepping
- Reverb default set to 0% (real samples have own recorded room sound)
- `createMediaElementSource` CORS issue resolved — pure `new Audio()` approach
- Tanpura Drone moved from Instruments tab to Practise tab

### Changed
- `playNote()` no longer calls `AC.resume()` for sample instruments
- Admin button added to header (always visible)
- Nav: AI Hub and Admin tabs added at right side

---

## [v4.0.0] — Prior version

### Features at v4
- 13 synthesised instruments (oscillator-based Web Audio API)
- 65+ song Play-Along library
- Raaga reference guide
- XP and rank system (Novice Shishya → Sangeet Ratna)
- Tabla Octopad, Western drum kit
- Tanpura drone synthesiser
- Theory, Academy, Sur & Shruti tabs
- Mobile-responsive keyboard layout
- Listen Mode with 3× repeat
- Raaga Quiz

---

## Versioning

- **v5.x.x** — Real samples + AI features era
- **v4.x.x** — Synth-only, full song library
- **v3.x.x** — Play-Along system introduced
- **v2.x.x** — Multi-instrument support
- **v1.x.x** — Basic keyboard and synth
