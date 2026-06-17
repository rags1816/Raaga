# AI Features Guide — Raaga Studio Pro v5

## Setup

1. Open the app → click **⚙ Admin** button (top right)
2. Enter your API key under Claude or Gemini
3. Select active model (Claude or Gemini)
4. Toggle on the features you want
5. Click **🤖 AI Hub** tab to use them

## API Key Security

Keys are stored **only in browser localStorage**. They never appear in the
source code. Safe to share the HTML file publicly — it contains zero secrets.

```
Admin Panel → localStorage → API calls → AI provider
     ↑
   Runtime only. Never in source.
```

## Supported AI Providers

### Claude (Anthropic)
- Model: `claude-sonnet-4-6`
- Get key: console.anthropic.com
- Key format: `sk-ant-api03-...`

### Gemini (Google)
- Model: `gemini-2.0-flash-exp`
- Get key: aistudio.google.com
- Key format: `AIzaSy...`

Both providers support all 11 features. Claude tends to give richer musical
explanations; Gemini is faster for quick lookups.

---

## Feature Reference

### 🧘 AI Guru Chat
**What it does:** Full conversational AI music teacher. Remembers context
within the session (conversation history sent with each message).

**Best for:** Open-ended questions, learning theory, understanding raagas,
asking about technique, historical context.

**Example prompts:**
- "What is the difference between Yaman and Yaman Kalyan?"
- "How do I practice meend on harmonium?"
- "Explain the concept of vadi and samvadi"

---

### 🔍 Raaga Identifier
**What it does:** Takes a note sequence (e.g. `S R G m P D N`) or a
description and identifies the raaga with full explanation.

**Input formats accepted:**
- Swara sequence: `S R G M P D N`
- Description: "uses komal Re and komal Dha, evening raaga, melancholic"
- Mixed: "starts with S G M P, avoids Re and Ga"

---

### 🕰 Raaga Historian
**What it does:** Deep dive into any raaga — origin, scale, emotional
quality, famous compositions, musicians, and similar raagas.

**Input:** Just the raaga name (e.g. "Bhairav", "Darbari Kanada")

---

### 📜 Lyrics Translator & Explainer
**What it does:** Translates and explains bandish, bhajan, thumri, or
ghazal lyrics from Hindi, Sanskrit, Braj Bhasha, or Urdu.

**Output includes:** Line-by-line translation, poetic imagery, theme
identification, deity/beloved addressed, and suggested raaga if identifiable.

---

### 🎵 AI Bandish Composer
**What it does:** Generates original compositions for a chosen raaga and taal.

**Parameters:**
- Raaga (13 options)
- Taal (Teental, Keherwa, Dadra, Rupak, Jhaptal, Ektaal)
- Tempo (Vilambit / Madhya / Drut)
- Theme (Devotional / Nature / Romantic / Patriotic)

**Output:** Sthayi + Antara with swaras, Hindi lyrics, English meaning,
and performance tips.

---

### 📋 Personalised Lesson Plan
**What it does:** Reads your current XP and rank from the app, then
generates a structured practice plan for the day.

**Parameters:** Available time (15 min to 90 min), focus area.

**Output:** Timed warm-up → main practice → cool-down, with specific
raagas, alankar patterns, and listening recommendations.

---

### 📊 Session Feedback
**What it does:** Tracks every note you play during practice. After
your session, AI analyses the note sequence and gives feedback.

**Tracking:** The app automatically records all notes played across all tabs.
Select which raaga you were practising to get more specific feedback.

**Output:** Accuracy score, raaga conformance analysis, strengths, one
key improvement area, and next session recommendation.

---

### 🎓 Raaga Tutor (Real-time)
**What it does:** As you play notes on the keyboard, checks each note
against the selected raaga's allowed notes and shows live colour feedback.

**Colours:**
- 🟢 Green = correct note for this raaga
- 🔴 Red = forbidden note (vadi/samvadi violation)
- 🟡 Yellow = neutral (not specifically in or out)

**Built-in raaga rules:** Yaman, Bhairav, Bhairavi, Khamaj, Bilawal, Malkauns.
More raagas can be added to the `RAAGA_RULES` object in the source.

---

### 🏛 Gharana Style Analyser
**What it does:** Describes your playing style or note sequences with
ornaments, and AI identifies which gharana it most resembles.

**Gharanas covered:** Jaipur-Atrauli, Kirana, Agra, Gwalior, Patiala,
Bhendibazaar, Mewati, Rampur-Sahaswan.

---

### 🎤 Live Pitch Detector
**What it does:** Uses your microphone (Web Audio API + autocorrelation
FFT) to detect the exact frequency you're singing and maps it to the
nearest swara in real time.

**Display:** Swara name, Hz frequency, cents deviation from perfect pitch,
and a visual tuning indicator (green = in tune, amber = slightly off, red = out).

**No AI required** — this feature uses only Web Audio API math. Works
without an API key.

**Browser requirement:** Chrome or Edge. Requires microphone permission.

---

### 🎙 Sing-Along Judge
**What it does:** Shows a random target note. You sing it. The app
scores your pitch accuracy continuously.

**Scoring:** Based on cents deviation from the target frequency.
< 10 cents = excellent, < 25 cents = good, > 50 cents = needs work.

**No AI required** — pure Web Audio pitch detection. Works without an API key.

---

## Technical details

### API call structure (Claude)
```javascript
POST https://api.anthropic.com/v1/messages
Headers:
  x-api-key: {your_key}
  anthropic-version: 2023-06-01
  anthropic-dangerous-direct-browser-access: true
Body:
  model: claude-sonnet-4-6
  max_tokens: 1024
  system: {feature-specific system prompt}
  messages: [{role: user, content: prompt}]
```

### API call structure (Gemini)
```javascript
POST https://generativelanguage.googleapis.com/v1beta/models/
     gemini-2.0-flash-exp:generateContent?key={your_key}
Body:
  contents: [{parts: [{text: systemPrompt + prompt}]}]
```

### Pitch detection algorithm
Uses autocorrelation on a 4096-sample FFT buffer from `getUserMedia`.
The `autoCorrelate()` function finds the fundamental frequency by finding
the lag with maximum correlation. Frequency is then matched to the nearest
swara in `SWARA_FREQS[]` using logarithmic distance (cents).
