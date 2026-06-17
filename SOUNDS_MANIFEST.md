# Sounds Manifest — Raaga Studio Pro v5

Documents all WAV sample files required for real instrument playback.

## File naming convention

```
sounds/{instrument}/{instrument}_{octave}_{noteNum}_{swara}_{westernNote}.wav
```

| Field | Values | Notes |
|-------|--------|-------|
| instrument | See table below | Folder name = instrument key |
| octave | 1 or 2 | 1 = Madhya Saptak (C4), 2 = Taar Saptak (C5) |
| noteNum | 01–12 | Zero-padded index |
| swara | Sa r R g G M m P d D n N | Uppercase = Shuddh, lowercase = Komal |
| westernNote | C Cs D Ds E F Fs G Gs A As B | `#` replaced with `s` |

## Swara → file mapping

| noteNum | Swara | Western | Type |
|---------|-------|---------|------|
| 01 | Sa | C | Shuddh |
| 02 | r | Cs | Komal Re |
| 03 | R | D | Shuddh Re |
| 04 | g | Ds | Komal Ga |
| 05 | G | E | Shuddh Ga |
| 06 | M | F | Shuddh Ma |
| 07 | m | Fs | Tivra Ma |
| 08 | P | G | Pa |
| 09 | d | Gs | Komal Dha |
| 10 | D | A | Shuddh Dha |
| 11 | n | As | Komal Ni |
| 12 | N | B | Shuddh Ni |

## Instruments

### Indian Classical (Melodic)

#### sitar/
```
sitar_1_01_Sa_C.wav    sitar_2_01_Sa_C.wav
sitar_1_02_r_Cs.wav    sitar_2_02_r_Cs.wav
sitar_1_03_R_D.wav     sitar_2_03_R_D.wav
sitar_1_04_g_Ds.wav    sitar_2_04_g_Ds.wav
sitar_1_05_G_E.wav     sitar_2_05_G_E.wav
sitar_1_06_M_F.wav     sitar_2_06_M_F.wav
sitar_1_07_m_Fs.wav    sitar_2_07_m_Fs.wav
sitar_1_08_P_G.wav     sitar_2_08_P_G.wav
sitar_1_09_d_Gs.wav    sitar_2_09_d_Gs.wav
sitar_1_10_D_A.wav     sitar_2_10_D_A.wav
sitar_1_11_n_As.wav    sitar_2_11_n_As.wav
sitar_1_12_N_B.wav     sitar_2_12_N_B.wav
```
*(Same 24-file pattern applies to: harmonium, sarod, veena, bansuri, shehnai)*

### Western Melodic
*(Same 24-file pattern: violin, saxophone, trumpet, grand_piano, church_organ)*

### Guitars
*(Same 24-file pattern: acoustic_guitar, electric_guitar)*

### Percussion
Percussion instruments may use a smaller set (fewer chromatic notes needed):
```
tabla_1_01_Sa_C.wav     (and as many notes as recorded)
dholak_1_01_Sa_C.wav
congo_1_01_Sa_C.wav
bongos_1_01_Sa_C.wav
octopad_1_01_Sa_C.wav
```

## Total file count

| Instruments | Octaves | Notes | Files each |
|-------------|---------|-------|------------|
| 13 melodic  | 2       | 12    | 24         |
| 5 percussion| 1–2     | varies| ~12        |

Maximum: 13 × 24 + 5 × 12 = **372 WAV files**
Minimum (octave 1 only): 18 × 12 = **216 WAV files**

The app functions with partial sets — missing files fall back to synthesis.

## Git LFS setup (recommended for GitHub)

WAV files can be large. Use Git LFS to track them:

```bash
# Install Git LFS
git lfs install

# Track all WAV files
git lfs track "sounds/**/*.wav"

# This creates .gitattributes — commit it
git add .gitattributes
git commit -m "chore: add Git LFS tracking for sound files"

# Then add sounds normally
git add sounds/
git commit -m "feat: add instrument WAV samples"
```

## Alternative: External hosting

If sounds are hosted on a CDN, update `getSamplePath()` in the HTML:

```javascript
function getSamplePath(instrument, octave, swara) {
  const BASE = 'https://your-cdn.com/raaga-sounds/'; // change this
  const idx = SAMPLE_SWARAS.indexOf(swara);
  if (idx === -1) return null;
  const noteNum = String(idx + 1).padStart(2, '0');
  const noteName = SAMPLE_NOTES[idx];
  return `${BASE}${instrument}/${instrument}_${octave}_${noteNum}_${swara}_${noteName}.wav`;
}
```
