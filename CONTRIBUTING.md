# Contributing to Raaga Studio Pro

Thank you for your interest in contributing! This guide covers everything you need.

## Project structure

```
raaga-studio-pro/
├── raaga_studio_v5.html     # The entire app — single self-contained HTML file
├── sounds/                  # WAV sample files (see Sounds section below)
│   ├── sitar/
│   ├── harmonium/
│   ├── bansuri/
│   └── ... (18 instrument folders)
├── README.md
├── CONTRIBUTING.md
├── CHANGELOG.md
├── LICENSE
├── SOUNDS_MANIFEST.md       # Documents all WAV files
├── .gitignore
└── docs/
    ├── keyboard_layout.md
    ├── ai_features.md
    └── raaga_studio_v5_guide.html
```

## Getting started

No build step, no npm install, no server required.

1. Clone the repo
2. Place `raaga_studio_v5.html` and the `sounds/` folder in the same directory
3. Open `raaga_studio_v5.html` in Chrome

That's it.

## How the codebase is organised

The entire app is a single HTML file (~4400 lines). It is structured as:

```
<head>        CSS variables, reset, component styles (~700 lines)
<body>        HTML structure — header, nav, tab sections (~600 lines)
<script>      All JavaScript (~3100 lines)
  ├── Constants and config (SEMITONES, KEYS_*, SONGS, RAAGAS)
  ├── Web Audio synth engine (synthHarmonium, synthSitar etc.)
  ├── Sample playback engine (playHTML5Sample, getSamplePath)
  ├── UI functions (buildKeys, showTab, triggerKey)
  ├── Play-Along engine (paStart, paStop, evaluatePANote)
  ├── Tabla / rhythm engine (playBol, startRhythm)
  ├── XP / scoring system
  ├── Admin panel (showAdminPanel, saveAPIKey, toggleAIFeature)
  └── AI engine (callAI, all 11 feature panels)
```

## Making changes

### Editing the app
Open `raaga_studio_v5.html` in a text editor. Use browser DevTools (F12) for debugging.

### Adding a new instrument
1. Add WAV files to `sounds/{instrument_name}/` following the naming convention:
   `{instrument}_{octave}_{noteNum}_{swara}_{westernNote}.wav`
   Example: `sounds/esraj/esraj_1_01_Sa_C.wav`
2. Add the instrument key to `SAMPLE_INSTRUMENTS` set in the JS
3. Add `<option>` entries to all three instrument `<select>` dropdowns
4. Add a `synthFallback` case mapping to the nearest synth approximation
5. Add to the Admin panel AI features section if relevant

### Adding a new song to the library
Find the `SONGS` array in the JS (search for `const SONGS = [`). Each song follows:
```javascript
{
  title: 'Song Name',
  film: 'Film/Album Name',
  year: 1990,
  raaga: 'Yaman',
  taal: 'keherwa',
  tempo: 120,
  notes: [{s:'S',o:0,d:0.5}, {s:'R',o:0,d:0.5}, ...]
}
```
Where `s` = swara label, `o` = octave offset (-1/0/1), `d` = duration in beats.

### Adding a new AI feature
1. Add the feature ID to `AI_FEATURES` array
2. Add metadata to `AI_FEATURE_META` object
3. Add toggle to the Admin modal HTML
4. Add a `buildXxxPanel()` function returning the panel HTML
5. Add the panel to `loadAIFeaturePanel()` switch
6. Wire the action function to call `callAI()`

## API key security — mandatory rules

- **Never** hardcode an API key anywhere in the source
- **Never** commit a `.env`, `secrets.js`, `config.local.js`, or any file containing keys
- Keys belong only in browser `localStorage` via the Admin Panel at runtime
- The app's security model: keys enter at runtime, never touch the source file
- Run `grep -r "sk-ant\|AIzaSy" .` before every commit to verify no keys leaked

## Sound files

WAV files are large and may exceed GitHub's file size limits (100MB per file, 1GB per repo).

**Options:**
- Use **Git LFS** (Large File Storage) for the `sounds/` directory
- Host sounds on a CDN and update the `getSamplePath()` base URL
- Add `sounds/` to `.gitignore` and document the download separately

**Naming convention:**
```
{instrument}_{octave}_{noteNum}_{swara}_{westernNote}.wav
sitar_1_08_P_G.wav   → Sitar, Madhya Saptak, Pa = G4
harmonium_2_01_Sa_C.wav → Harmonium, Taar Saptak, Sa = C5
```
Note: `#` is replaced with `s` in filenames (C# → Cs, F# → Fs).

## Reporting bugs

Please include:
- Browser and version (Chrome/Edge/Firefox)
- Operating system
- Which tab / feature was active
- Console errors (F12 → Console tab)
- Steps to reproduce

## Code style

- Vanilla JavaScript only — no frameworks, no npm
- Keep the app self-contained in a single HTML file
- Prefer clarity over cleverness
- Add comments for non-obvious logic, especially audio/music theory code
- Test in Chrome first (primary supported browser), then Edge

## Pull request checklist

- [ ] No API keys in any file
- [ ] App opens without errors in Chrome
- [ ] All three saptaks play correctly
- [ ] Play-Along works for at least one song
- [ ] Admin panel opens and closes
- [ ] AI features work if a key is present (or gracefully fail without one)
- [ ] README updated if new features added
- [ ] CHANGELOG.md entry added
