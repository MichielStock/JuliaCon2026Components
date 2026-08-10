# Visualisation Themes and Guidelines:

NOTE: Make sure that your visualisation submission is a single standalone html file named `index.html` inside `viz_submission/`

## 1. Accent

Your accent comes from your team slug. Compute it, do not pick it:

```
slot = (sum of UTF-8 byte values of the lowercase team slug) mod 6
```

| slot | name | deep | **base** | lift | wash | hairline |
|---|---|---|---|---|---|---|
| 0 | indigo | `#2A177A` | `#4422CC` | `#6B4FE0` | `#EDECFB` | `#D2CBF4` |
| 1 | grape | `#491E77` | `#7A34C4` | `#9B66D3` | `#F1EDFB` | `#DECFF2` |
| 2 | azure | `#11327A` | `#1F55C9` | `#4677DE` | `#EBEFFB` | `#CAD6F3` |
| 3 | cyan | `#074351` | `#0E6E86` | `#1588A5` | `#E9F1F7` | `#C6DCE4` |
| 4 | teal | `#094A39` | `#107A5E` | `#179675` | `#EAF2F4` | `#C7DFDC` |
| 5 | magenta | `#6B1C42` | `#B0306E` | `#CB4F8B` | `#F5EDF5` | `#EACEDF` |

How each stop is used:

- **base** — the hero number, the primary data line, filled marks, the active
  state. This is *the* colour of your submission.
- **lift** — the second series, hover, gradient end. Never for text under 20 units.
- **deep** — gradient start, text on a wash fill, the darkest ink of the accent.
- **wash** — large tinted fills (a plot band, a highlighted row).
- **hairline** — accent-tinted rules and axes.

Gradients run **deep → base → lift**, in that order, and nowhere else. This is
the same ramp the race car's bodywork uses on the slides.

Every base passes 5.1:1 against `#FAFBFF`; every lift passes 3.5:1. Keep it that
way — if you tint, tint the background, not the mark.

---

## 2. Type

Two families, no others.

```html
<link href="https://fonts.googleapis.com/css2?family=Instrument+Sans:wght@400;500;600&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
```

```
sans: 'Instrument Sans', ui-sans-serif, system-ui, sans-serif
mono: 'JetBrains Mono', ui-monospace, 'Courier New', monospace
```

**Every number is mono.** Lap times, temperatures, counts, axis labels, the
hero. No exceptions — this is the single strongest signal that two tiles belong
to the same board.

| role | family | size (dashboard px / tile units) | weight | tracking | colour |
|---|---|---|---|---|---|
| hero number | mono | 44–56 / 52–64 | 500 | −0.02em | accent **base** |
| headline | sans | 28–34 / — | 500 | −0.02em | accent base, with spans in `#1A1330` |
| kicker | mono | 10.5–12 / 15–17 | 500 | 0.16em–0.3em, **uppercase** | accent base |
| body | sans | 13–15 / — | 400 | 0 | `#4A4365` |
| data label | mono | 9.5–11 / 16–18 | 500 | 0.15em, **uppercase** | `#8580A0` |
| axis / tick | mono | 10 / 16 | 400 | 0.02em | `#8580A0` |
| caption | mono | 10–11 / — | 400 | 0.16em, uppercase | `#8580A0` |

At most **six** distinct sizes in one view. Line height 1.45–1.55 for body,
1.1–1.2 for headlines. Units are set one step down and in `#8580A0`:
`4:12.6` + `S`, not `4:12.6 S` at the same weight.

---

## 3. Surface, ink, geometry

| token | value | use |
|---|---|---|
| stage | `#F3F2F7` | the page behind the cards |
| paper | `#FAFBFF` | card and panel fill |
| panel-2 | `#FDFCFF` | a panel nested on paper |
| ink | `#1A1330` | headings, hero labels |
| ink-2 | `#4A4365` | body |
| ink-3 | `#8580A0` | labels, axes, captions |
| hairline | `#D8D3E8` | rules, borders, gridlines |
| hairline-soft | `rgba(216,211,232,0.6)` | rules inside a list |
| chip | `#EFECF8` | inactive badge fill |
| asphalt | `#D3D0DE` `#C2BED3` `#B8B4CB` | track surface, if you draw one |
| tyre | `#0A0714` `#16111F` | tyre rubber, if you draw one |
| silver | `#8580A0` | mechanical linework (suspension, wings) |
| **status: dq** | `#C4574B` | disqualified / failed only |

**Warm red is reserved for status.** It is never an accent, never a series
colour, never decoration. A red mark on this board means something went wrong.

```
radius   panel 14   card 11   chip 7   badge 6   inline code 5
border   1px, or 1.2px on an interactive card — rgba(<accent base>, 0.14) at
         rest, 0.45 when active
shadow   0 10px 34px rgba(20,15,40,0.13)   ← the only shadow. One per card.
grid     8px. Every margin, padding and gap is a multiple of it.
```

Panels are **paper on stage** with an accent-tinted hairline, never a filled
accent block. The board is light; do not invert it.

---

## 4. The parts you must keep

These four make a submission read as part of the board. Reproduce them.

**Kicker line.** Above every headline: mono, uppercase, wide-tracked, accent
base. `07 · COMPETITION`-shaped — a number, a middle dot, a word.

**Hero + unit.** One number is the biggest thing in the view. Mono, accent base,
its unit set small in `#8580A0` beside it.

**Meter.** Where you show a fraction of a budget (energy, grip, temperature
window), use the segment bar: 10 flex segments, 6 units tall, radius 1.5, 3
units apart. Unlit `rgba(26,19,48,0.16)`, lit accent **base**, and the top three
segments `#1A1330` when they light. Do not substitute a percentage ring.

**Footer rule.** Bottom of the dashboard: a `#D8D3E8` top border, then mono
uppercase caption left, mono date right:

```
COMPETITION | <your name or team name >            JULIACON 2026
```

Separators between caption segments are `|` at 55% accent opacity, 10px apart.

---

## 5. Motion

Motion is scarce here and always means something.

- **Reveal:** `opacity 0 → 1`, `translateY(8–14px) → 0`, 0.38–0.9 s ease,
  staggered 80–100 ms. Nothing else animates on load.
- **Inactive → active:** opacity `0.26 → 1`, border `0.14 → 0.45`, 0.38 s ease.
- **Data motion:** if a value moves, one damped signal drives everything derived
  from it — `v += (target − v) * 0.16` per frame, and every mark reads off `v`.
  The slides do this with one scroll velocity driving asphalt, tread, blur and
  the speed readout at once. Coherent, not independently timed.
- **No** looping ambient animation, no bounce, no easing that overshoots.
- Wrap every animation:

```css
@media (prefers-reduced-motion: reduce){ *{animation:none!important;transition:none!important;} }
```
