# 🎵 Raaga
### Indian Classical Music Studio

[![Live App](https://img.shields.io/badge/Live%20App-GitHub%20Pages-orange?style=flat-square)](https://yourusername.github.io/raaga/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)
[![No API Key Required](https://img.shields.io/badge/API%20Key-Optional-blue?style=flat-square)](docs/ai_features.md)

> **Live:** `https://yourusername.github.io/raaga/` (replace `yourusername` with your GitHub username)

A browser-based Indian classical music learning app — single HTML file, no server needed.

## Features
- 18 real instrument samples (Sitar, Harmonium, Bansuri, Tabla, Veena, Sarod...)
- 3-octave piano keyboard (Mandra, Madhya, Taar Saptak)
- Full laptop keyboard mapping across all 3 octaves
- 65+ songs play-along library
- Raaga reference, Theory, Academy tabs
- AI features via Admin Panel (Claude / Gemini)

## Setup

### Basic (no AI)
1. Clone the repo or download `index.html`
2. Place it in a folder alongside the `sounds/` directory:
```
Music/
├── index.html              ← open this in Chrome
└── sounds/
    ├── sitar/
    ├── harmonium/
    ├── bansuri/
    └── ... (18 instrument folders)
```
3. Open `index.html` in Chrome

**Or visit the live GitHub Pages URL above — no download needed.**

### With AI features
1. Open the app → click **⚙ Admin** button
2. Enter your API key (Claude or Gemini) in the Admin Panel
3. Toggle on the AI features you want
4. Keys are stored in **browser localStorage only** — never in the file

## 🔐 API Key Security

> **API keys are NEVER stored in the HTML source file.**
> They are entered at runtime via the Admin Panel and stored in browser localStorage only.
> This file is completely safe to commit publicly to GitHub.

**Rules for contributors:**
- Never hardcode any API key into the source
- Never commit a `.env` or `secrets.js` file
- The Admin Panel pattern (localStorage at runtime) is the correct approach

## Laptop Keyboard Layout

| Saptak  | Sa | Re | Ga | Ma | Pa | Dha | Ni | Sa' |
|---------|----|----|----|----|----|----|-----|-----|
| Mandra  | Z  | X  | C  | V  | B  | N  | M  | ,   |
| Madhya  | A  | S  | D  | F  | G  | H  | J  | K   |
| Taar    | I  | O  | L  | 9  | 0  | -  | =  | ]   |

Black keys (komal/tivra): W E T Y U (Madhya), click only for other saptaks

## AI Features (Admin Panel)
| Feature | Description |
|---------|-------------|
| 🎓 AI Raaga Tutor | Checks notes against raaga rules in real time |
| 🧘 AI Guru Chat | Ask anything about Indian classical music |
| 🔍 Raaga Identifier | Play a note sequence — AI names the raaga |
| 🎵 AI Bandish Composer | Generate compositions for any raaga + taal |
| 📋 Lesson Plan | Personalised practice plan from your XP history |
| 📊 Session Feedback | Performance score after practice |
| 🎤 Pitch Detection | Mic-based swara detection while singing |
| 🎵 Sing-Along Judge | Accuracy scoring while singing play-along |
| 🏛 Gharana Analyser | Identify which gharana style your playing resembles |
| 📜 Lyrics Explainer | Translate and explain bandish lyrics |
| 🕰 Raaga Historian | History, context, and famous recordings of any raaga |

## Sounds Folder
The `sounds/` folder contains WAV files per instrument per note:
```
sounds/{instrument}/{instrument}_{octave}_{noteNum}_{swara}_{note}.wav
Example: sounds/sitar/sitar_1_01_Sa_C.wav
```
Octave 1 = Madhya Saptak (C4), Octave 2 = Taar Saptak (C5)

> **Note:** Sound files may be too large for GitHub free tier.
> Consider using Git LFS or hosting sounds separately and updating paths in the HTML.

## License
MIT — free to use, modify, and distribute.
