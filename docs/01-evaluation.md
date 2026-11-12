---
title: TG Rót Roman — evaluation
type: audit
status: active
updated: 2026-11-12
description: First pipeline look at the Roman since June 2026. Covers variable-font standards, weight steps, vertical metrics, sidebearings across the width axis, the copied kerning, coverage and loose ends.
aliases:
  - tg-rot-evaluation
tags:
  - project/kol-foundry
  - domain/typography
sources:
  - typefaces/tg-rot/glyphs/TGRot-Roman.glyphspackage
  - typefaces/tg-rot/export/TGRotVF.ttf
related:
  - "[[02-plan|plan]]"
  - "[[03-export|export]]"
---

# TG Rót Roman — evaluation

## 2026-11-12 — first pipeline look since June 2026

Read live through the Glyphs MCP and from the shipping `export/TGRotVF.ttf` (exported 2026-06-13, after the source's last change). Nothing in the font was changed. The Roman was saved today as `TGRot-Roman.glyphspackage`, and the old `tg-rot-roman.glyphs` is in `_tmp/2026-11-12-glyphs-file/`. The Italic (`tg-rot-italic.glyphs`) is still a single file: an unslanted June copy of the Roman, so it is rebuilt from the finished Roman rather than evaluated on its own.

**Font:** variable, wdth 64–172 × wght 100–900, four corner masters (Thin `B394…`, Black `C9E3…`, Thin Extended `m005`, Black Extended `5DCF…`; Thin and Black sit at the Condensed end). UPM 2048. Cap height 1400, x-height 1048, ascender 1840, descender −512, italic angle 0. 274 glyphs, 264 exporting (the rest are `_` component parts, `tail.q`, the slash marks), 244 encoded. Features: `aalt ccmp locl case zero ss01` (all automatic), plus `kern mark mkmk`. Instances: one variable (`TGRotVF`) and 35 statics, 5 widths × 7 weights. Same file is in `tg-collection/tg-rot/`.

### 1. Where it stands

A Weight × Width grotesque with most of Western European already in: A–Z, a–z, all the Icelandic letters, À–Ý with grave, circumflex, tilde, ring and dieresis, Ç Ñ Ø Œ ß ẞ, Ŵ Ẃ Ẁ Ẅ Ŷ Ỳ, one figure set with a slashed zero, core punctuation, arrows and math, and `ss01` for single-storey `a g`. Its spacing is keyed throughout (172 glyphs carry metrics keys). But its kerning was copied, its sidebearings ignore the width axis, and the vertical metrics clip below the baseline.

### 2. Variable-font standards (ARCHITECTURE §6)

Done in June, by a different route from Gullhamrar and Málrómur.

| | Now | Status |
|---|---|---|
| Axis Location | on all 4 masters and 35 instances (wght classes, wdth %) | ✅ |
| Default style | `Variable Font Origin` = Thin (Condensed corner); `scripts/build.sh` rebases the export to Regular / Normal | ✅ but needs the build step |
| Instance names | `SemiCondensed` but `Semi Expanded` (with a space) | one spelling |

Gullhamrar and Málrómur got a Regular master so Glyphs exports the right default with no script. Rót's default sits in the middle of both axes, so a Regular master there would be a fifth, centre master. Keeping `build.sh` is the smaller step.

### 3. Weight steps

H stems at the seven weights (Normal width): 31 · 53 · 90 · 120 · 137 · 161 · 220, so the steps are +22 **+37** +30 **+17** +24 **+59**. Light→Regular jumps, Medium and SemiBold sit close, and Black jumps furthest. The instances sit at design 100 / 192 / 350 / 475 / 550 / 650 / 900.

### 4. Vertical metrics

Typo and hhea are 1800 / −360 / gap 100, win is 1800 / 360, and Use Typo Metrics is on.

- **Descenders clip.** `winDescent` is 360, but g j y reach −384, ß −379, @ −464 (Black Condensed), © ® −435, ∫ −470. Windows cuts all of them.
- Above the cap height nothing but √ (1840) passes 1800; the accented capitals stay under.
- The win values have to cover the real extremes once the new glyphs are in.

### 5. Sidebearings

LSB / RSB are **identical in every corner** of the design space:

| Glyph | Thin Cond. | Black Cond. | Regular | Thin Ext. | Black Ext. |
|---|---|---|---|---|---|
| H | 96 / 96 | 96 / 96 | 96 / 96 | 96 / 96 | 96 / 96 |
| O | 64 / 64 | 64 / 64 | 64 / 64 | 64 / 64 | 64 / 64 |
| n | 40 / 40 | 40 / 40 | 40 / 40 | 40 / 40 | 40 / 40 |
| o | 64 / 64 | 64 / 64 | 64 / 64 | 64 / 64 | 64 / 64 |
| E | 96 / 60 | 96 / 60 | 96 / 60 | 96 / 60 | 96 / 60 |
| v | 24 / 24 | 24 / 24 | 24 / 24 | 24 / 24 | 24 / 24 |
| H advance | 560 | 712 | 924 | 1452 | 1792 |

- **The width axis doesn't touch spacing.** H is 560 wide in Thin Condensed and 1792 in Black Extended, with the same 96 either side. Expanded will set tight and Condensed loose. Proof before deciding how much each corner moves.
- **Caps and lowercase disagree on rounds.** O (64) gets less than H (96), as usual for a grotesque. In the lowercase it's the reverse: o (64) gets more than n (40).

### 6. Kerning

- **The kerning was copied** in June from the retired `TG Root Italic.glyphs` (`kol-steal-kerning.py`, same family, ×1.0). That makes 257 class pairs, identical in all four masters, so Condensed and Extended get the same values at a third and three times the width. ARCHITECTURE §7: it gets replaced by kerning measured from Rót's own outlines.
- **Holes:** T·o and Y·o have no value, while T·a has −94.
- **Groupless:** all punctuation (period, comma, quotes, guillemets, dashes, brackets, slash…), the symbols and the spacing accents. The letters and figures are grouped.

### 7. Missing

**Windows-1252 (22):** Š š Ž ž (need a caron mark; the rest composes), soft hyphen, `¤ ¥ ¦ ª º ¯ ² ³ ¹ µ ¼ ½ ¾ ƒ † ‡`. Nothing from ASCII is missing.

### 8. Harmony and loose ends

- **Dashes:** the hyphen is a fixed 680 wide in every width and goes from 120 to 320 thick. The en dash (801–841 wide) and em dash (1240) are 40 → 82 thick, so they're far lighter than the hyphen and sit on a different centre. None of the three follows the width axis.
- **Tags:** the spacing accents and `idotless`/`jdotless` are orange, the `.tight` marks brown, the `ss01` set yellow, `y` magenta. His meaning is unknown.
- Font metadata has designer "Tór Grímsson" and URL `kolkrabbi.io`, but no copyright, license, manufacturer or vendor ID (`UKWN`). Version 1.000. Dylgjur's placeholders apply.
- The file was last exported from Glyphs 3.4.1. `build.sh` points at fontTools in `~/.local/pipx/venvs/fonttools/`, which is on the iMac only. On the MBP fontTools is at `~/.local/share/uv/tools/fonttools/`.

### 9. Suggested order

1. **Standards:** keep `build.sh`, fix the `Semi Expanded` spelling, decide the weight steps.
2. **Spacing:** sidebearings that follow the width axis, the lowercase round/straight relation, the dashes.
3. **Kerning:** clear the copied kerning, group the punctuation, then measure pairs per master.
4. **Punctuation and symbols:** soft hyphen and the 18 missing symbols.
5. **Western European:** caron mark, Š š Ž ž.
6. **Vertical metrics and metadata:** win values set to the real extremes, copyright and license.
7. **Italic:** slant the finished Roman (the June procedure), then export both.
