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

## The thirteen tabs

| Tab | What it does |
|---|---|
| 🎯 **Fretboard Explorer** | Pick scale / key / tuning and highlight it on the neck. Switch between 9 fingering systems, split by position, overlay colour blocks, highlight the scale's characteristic chord arpeggio |
| 🧠 **Practice** | Six drills: find-the-note, scale fill-in, note name by ear, interval by ear, mode by ear, and **staff sight reading** — the prompt is notated on a staff with key signature and rhythm, and you tap the notes in order on the neck. The staff follows the tuning; see the next section |
| 📚 **Scale Library** | 82 scales / arpeggios in 9 families, each with interval structure, degrees, characteristic chords and usage notes |
| 🧩 **CAGED Chords** | The five positions of a chord on the neck, ordered by **actual lowest fret** so the first shape changes with the key |
| 🧮 **Scale & Harmony** | Seven degrees × five chord-tone extension layers; click any cell to jump to its shape |
| 🎼 **Arpeggio Explorer** | One arpeggio across the five CAGED positions, plus which scales it usually pairs with |
| 🔗 **Progression Trainer** | 456 chord progressions with note-by-note voice leading and recommended fingerings |
| 🎸 **Jam** | 200 backing tracks. The progression is laid out bar by bar, then the **minimum-hand-travel** voicings, then the improvisation material available over each chord |
| 🔍 **Improvisation Lookup** | Given a chord quality and key, list usable scales, arpeggios and substitutions |
| 🎹 **Voicing** | Treat the whole progression as one object and search for the lowest total hand travel; returns several distinct optima |
| 🖐 **2-1-2 Arpeggios** | Arpeggio shapes built on a `2-1-2` notes-per-string alternation, starting from the 6th / 5th / 4th / 3rd string |
| 🎯 **Chord Lookup** | The other direction: tap notes on the neck (3 or more) to **name the chord**; tap exactly two notes and it names their **interval** and checks whether they form a power chord (`X5`). Coarse / degree-aware / diatonic modes; a non-root bass becomes a slash chord; when nothing fits, it falls back to the five trichord families (root removed, six notes split into two groups of three) |
| 🎼 **Scale Lookup** | Tap notes on the neck (5 or more) to **find the scale**. All 82 scales × 12 tonics = 984 readings, layered by "how many notes you are still missing". Every reading of the same pitch-class set is listed side by side — which is why a seven-note scale can only ever be pinned down to its **parent-scale group** |

## Read the staff, find it on the neck: staff sight reading

The **sixth drill** in Practice. The prompt is not text but a real **staff excerpt**: key signature and
rhythm included — note values, stems, flags, dots, rests and a final barline are all notated properly.
Read it, then tap the matching notes **in order** on the neck.

| Sight reading · guitar (treble staff) | Sight reading · 4-string bass (bass staff) |
|---|---|
| ![treble staff](screenshots/08-sight-reading-guitar-staff.png) | ![bass staff](screenshots/09-sight-reading-bass-clef.png) |

- **The staff follows the tuning.** Guitar (including all open tunings) → **treble staff**;
  4-string EADG / 5-string BEADG bass → **bass staff** (F clef). No switch to flip: changing tuning
  within the same family keeps the current question, **crossing families deals a new one**.
- **Notated per instrument convention.** Guitar sounds an octave below the written pitch; bass is
  written an octave up in the same spirit (low E sounds E1, written on the ledger line below the bass
  staff). The note-name hint shows the **written** names.
- **The question is always playable.** Notes are chosen only from scale tones inside the currently
  tappable range. For bass the range is clipped to **at most three ledger lines**
  (roughly sounding A0–G3) — running the full 24 frets would drag out seven or eight ledger lines.
- **Tap once, every position of that pitch lights up** (ring colour per pitch class, the same 12-colour
  set as the chord lookup), so you see every place that note lives on the neck.
- **Judging is octave-exact.** The written pitch is what you must tap: the same pitch in another
  position counts (open 1st string and 5th fret 2nd string are both E4), another octave does not.
  All correct → next question and a point; any wrong → those notes get a red cross, minus 6, and you
  stay on the question to undo and resubmit.
- **Reading aids**: **▶ play the prompt** (sounds the written pitches in order; rests take time but stay
  silent) and **☐ show note names** under the staff.
- A live answer row records what you tapped, with **↶ undo** and **clear**; note count per question is
  yours to pick (3–12, default 5).

## Data

| Item | Count |
|---|---|
| Scales / arpeggios | **82** across **9** families |
| Mode colour profiles | **59** |
| Fingering systems | **10** (3NPS, 4NPS, wide, 3-1-3, 2-1-2, 2-1-2 basic, 2NPS, CAGED, position window, unsegmented). **9** are visible at a time — all **12** scales of the pentatonic / blues family swap 4NPS for the wide form (every scale tone inside one 7-fret position window) |
| Tunings | **17** (6-string guitar 10, 7-string 5, 4-string bass 1, 5-string bass 1) |
| Chord qualities | **23** |
| Chord progressions | **456** |
| Backing tracks | **200** |
| String groups | **16** |
| Chord qualities for note-tapping | **46** (wider than the 23 used by the improvisation lookup: sixth chords, 9th / 11th / 13th, altered dominants, and every no-5 / no-3 form) |
| Scale readings for note-tapping | **984** (82 scales × 12 tonics; readings whose pitch classes collapse are excluded) |

All counts are produced by the page's own runtime — they are not marketing copy.

## Engineering notes

- **Single file.** HTML + CSS + JS in one `index.html`, **12,439 lines / 833 KB**. No bundler, no dependency, no CDN.
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
