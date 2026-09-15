# Fretboard Trainer · 吉他指板训练器

> **A single-file, zero-dependency fretboard practice tool you can open offline by double-clicking.**
> Scale systems, fingering patterns, CAGED, arpeggios, chord progressions, voice leading and
> improvisation material — all inside one HTML file.

![Fretboard Explorer · C major × CAGED five shapes](screenshots/01-fretboard-explorer.png)

*The UI is in Simplified Chinese. This page is a summary for English readers.*

---

## Why this exists

Three things that most method books and practice apps handle poorly:

1. **You know a scale, but lose it the moment you change position.** Usually not a practice problem —
   a *position* is a **vertical** concept: a shape laid out string-by-string from a starting fret,
   not "a horizontal slice of the neck".
2. **You know a scale but not what it sits on.** Scales and harmony drift apart.
3. **Nobody tells you where the hand goes between two adjacent chords** in a progression.

This tool merges all three onto one fretboard:

```
pick a scale → see how it blocks up in 9 fingering systems → see its characteristic chords & arpeggios
             → compute the "minimum hand travel" voicings across a real progression
             → get the improvisation material available in that very position
```

## Quick start

No Node, no build step, no network, no install.

| Way | Steps |
|---|---|
| **Local** (recommended) | Download `index.html` and double-click it. Works offline. |
| **Online** | Open the GitHub Pages link (see the About section). |
| **Clone** | `git clone <this repo>` and open `index.html`. |

Everything is embedded in the file — the page issues **no network requests at all**.
Preferences (key, tuning, theme) go to `localStorage` and never leave your machine.

## The eleven tabs

| Tab | What it does |
|---|---|
| 🎯 **Fretboard Explorer** | Pick scale / key / tuning and highlight it on the neck. Switch between 9 fingering systems, split by position, overlay colour blocks, highlight the scale's characteristic chord arpeggio |
| 🧠 **Practice** | "Find the note" — tap *every* position of a named pitch; "Scale ear training" — identify a mode by ear, drilled in 8 parent-scale families |
| 📚 **Scale Library** | 81 scales / arpeggios in 9 families, each with interval structure, degrees, characteristic chords and usage notes |
| 🧩 **CAGED Chords** | The five positions of a chord on the neck, ordered by **actual lowest fret** so the first shape changes with the key |
| 🧮 **Scale & Harmony** | Seven degrees × five chord-tone extension layers; click any cell to jump to its shape |
| 🎼 **Arpeggio Explorer** | One arpeggio across the five CAGED positions, plus which scales it usually pairs with |
| 🔗 **Progression Trainer** | 456 chord progressions with note-by-note voice leading and recommended fingerings |
| 🎸 **Jam** | 200 backing tracks. The progression is laid out bar by bar, then the **minimum-hand-travel** voicings, then the improvisation material available over each chord |
| 🔍 **Improvisation Lookup** | Given a chord quality and key, list usable scales, arpeggios and substitutions |
| 🎹 **Voicing** | Treat the whole progression as one object and search for the lowest total hand travel; returns several distinct optima |
| 🖐 **2-1-2 Arpeggios** | Arpeggio shapes built on a `2-1-2` notes-per-string alternation, starting from the 6th / 5th / 4th / 3rd string |

## Data

| Item | Count |
|---|---|
| Scales / arpeggios | **81** across **9** families |
| Mode colour profiles | **58** |
| Fingering systems | **10** (3NPS, 4NPS, wide pentatonic, 3-1-3, 2-1-2, 2-1-2 basic, 2NPS, CAGED, position window, unsegmented). **9** are visible at a time — major / minor pentatonic swaps 4NPS for wide pentatonic |
| Tunings | **17** (6-string guitar 10, 7-string 5, 4-string bass 1, 5-string bass 1) |
| Chord qualities | **23** |
| Chord progressions | **456** |
| Backing tracks | **200** |
| String groups | **16** |

All counts are produced by the page's own runtime — they are not marketing copy.

## Engineering notes

- **Single file.** HTML + CSS + JS in one `index.html`, **9,271 lines / 654 KB**. No bundler, no dependency, no CDN.
- **Zero external requests.** No `<link>`, no `fetch`, no `XMLHttpRequest`, no dynamic `import()`.
  The only URL in the file is the SVG namespace identifier, which performs no network access.
- **Sound is synthesised, not sampled.** Web Audio triangle + sawtooth oscillators. The repository
  contains **no audio files**.
- **Fretboards are computed SVG**, not bitmaps — crisp at any zoom, printable.
- **Data is embedded** as plain JS literals; there is no backend.

### The one rule that matters most

"Nearest" on a guitar must be measured in **fret geometry**, not in semitones. The same pitch has several
positions on the neck: `2nd string 5th fret → 1st string open` does not change pitch at all, yet the hand
must travel back from fret 5 to fret 0. Measuring in semitones makes the optimiser pick connections like
"A7 at fret 12 → E7 at fret 7" — close in pitch, half a neck apart in practice. So the cost function is:

```
cost = Σ[ |Δfret| + 0.35 × |Δsemitone − Δfret| ]   ← on one string, fret change == pitch change,
                                                   ← so don't double count; across strings the
                                                   ← extra part is the "string-crossing fee"
     + 1.0 × |displacement of the hand centre|     ← without this term the optimiser picks
                                                   ← "every finger moves a little, the whole
                                                   ← hand jumps around"
     + 3.4 × number of unmatched voices
```

Measured over 100 backing tracks / 1000 adjacent chord pairs: median hand travel **0.5 frets**,
max **2.0 frets**.

## Boundaries

- Targets **6-/7-string guitar and 4-/5-string bass** in 12-TET.
- Voice leading uses fret geometry, not a physiological hand model.
- "Recommended material" is a *usable set* matched from chord quality and mode — not a single right answer.
- Where source material only gave whole-song scale options rather than per-chord ones, the table falls back
  to the whole-song entries and marks them with a dashed badge instead of pretending otherwise.

## License

[MIT](LICENSE).
