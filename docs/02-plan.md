---
title: TG Rót — plan
type: plan
status: draft
updated: 2026-11-12
description: Seven workstreams that take the Roman from the 2026-11-12 evaluation to a standard, kerned Western European release, then rebuild the Italic as its slant.
aliases:
  - tg-rot-plan
tags:
  - project/kol-foundry
  - domain/typography
phases:
  - W1 standards
  - W2 spacing
  - W3 kerning
  - W4 punctuation and symbols
  - W5 Western European letters
  - W6 vertical metrics and metadata
  - W7 italic
related:
  - "[[01-evaluation|evaluation]]"
  - "[[03-export|export]]"
---

# Plan — TG Rót

**Raised:** 2026-11-12, from [[01-evaluation|the 2026-11-12 evaluation]]. Follows `docs/operations/02-family-pipeline.md` step 2. Point verbatim, 2026-11-12: *"we are redoing rot, like every other typeface we follow the playbook."*
**Status:** approved 2026-11-12. W1–W7 built and saved 2026-11-12. Exported (both VFs + WOFF2), collected, proofs printed, family files in place. Next: git + GitHub (his commands).
**Laws carried:** the work is done through the Glyphs MCP on `glyphs/TGRot-Roman.glyphspackage`. Nothing is saved without his word, and every edit is previewed first. From W1 on there are nine masters (3 × 3), edited together. Kerning is measured from the font's own outlines, never copied (ARCHITECTURE §7). His drawings are never replaced. Any change to an outline is checked in a render before it is shown.
**How a phase closes:** the measurable acceptance line comes first and is read back through the MCP, or from the exported font with fontTools. Then he looks at the result in Glyphs.

---

## W1 — Standards

- A 3 × 3 master grid, set up so Glyphs exports the right default itself and `scripts/build.sh` and the `export/raw/` step retire to `_tmp/` (his word, 2026-11-12: *"fix the font so we dont have to shitmix the correct file through dist"*). A Regular centre master alone was tried first and broke the edges: with the default in the middle, the corners only count where both axes move, so Regular Condensed came out at full Regular width (H 924 instead of 607). — ✅ built and saved 2026-11-12:
  - Nine masters: Thin/Regular/Black × Condensed/Normal/Extended. The five new ones are interpolated from the corners (`addAsMaster` on the static instances), rounded, with Axis Location and the corners' 257 kerning pairs. Corner masters renamed `Thin Condensed` / `Black Condensed`.
  - `Variable Font Origin` = Regular.
  - Test export (scratchpad): fvar default wdth 100 / wght 400 named Regular, OS/2 400/5, 35 unique instances. Against the June `TGRotVF.ttf` at all 35 instances, every glyph's advance and bounds match within 2 units, except Î at Regular Extended (accent 13 units left). Î's accent is placed by hand in each master and its width doesn't follow I; it goes into W2.
- The `Semi Expanded` instances renamed `SemiExpanded`. — ✅ saved 2026-11-12
- `build.sh`, `set-axis-location.py` and `export/raw/` retired to `_tmp/`; `03-export.md` rewritten for the direct export. — ✅ 2026-11-12
- Weight steps (his word: *"just get it done"*): Thin, Regular and Black stay put; Light, Medium, SemiBold and Bold move to design 225 / 488 / 625 / 761 in all five widths. H stems at Normal width now 31 · 60 · 90 · 123 · 156 · 188 · 221 (steps 29–33, were +22 +37 +30 +17 +24 +59). Thin/Regular/Black advances match the June export within 1 unit. — ✅ saved 2026-11-12
- Glyphs 4 gotcha met on the way: setting an instance's `axes` from a script zeroed its userspace values and the export failed; every master and instance now has its userspace weight/width set explicitly (the old `Axis Location` parameters are gone).
- **Acceptance:** the plain Glyphs export (no script) has fvar default 400/100 named Regular, OS/2 400/5; 35 instance names in one spelling; stem steps within ±5 of each other.

## W2 — Spacing — ✅ built and saved 2026-11-12

- **Rule, measured from SF Pro (display size) on this Mac:** going narrower, sidebearings shrink with the advance; going wider they stay nearly flat (H 140 → 136); Black is a little tighter than Thin. Rót had one fixed value per glyph in every master, so Condensed set loose.
- **Built:** the 36 fixed-number spacing keys (H O V B E n o a v s f k j, the figures, period, plus, &, £) moved from glyph level to each master: Condensed × that master's own Condensed/Normal advance ratio (≈0.6–0.67), Extended × 1.05, Black × 0.88. Everything keyed to them followed.
- **Lowercase rounds:** o (and a's bowl side) had more room than n (64 vs 40), the reverse of the caps. Now n 62, o/a 42: the caps' own round/straight ratio (O/H = 0.667) at the same total. Proof: `nnonnoonn` reads even.
- **Composites:** 539 accented master layers kept their old widths after the respacing; Glyphs' `updateMetrics` plus a width-from-base pass fixed all of them.
- **Corrected 2026-11-12 (his catch, ë):** that pass also ran Glyphs' alignment on `dieresiscomb`, which is two `dotaccentcomb` components, and stacked the second dot on the first. Restored: June's dot positions in the four corner masters, the other five interpolated, auto-alignment off on both dots. Checked against the June export at four locations; every other part-built glyph was diffed against June and had only moved as a whole (h k r i Q Ð Ø ø ? 0).
- **Î:** its circumflex is drawn at 90% width (his design), which made Glyphs flatten it to outlines and leave the accent 50–65 units left. Now the scaled accent is centred on I and its width equals I's in all nine masters; checked in the export at five locations (centre within 1 unit).
- **Dashes:** en and em dash take the hyphen's thickness and height in every master (they were 40–82 thick against the hyphen's 120–320). Hyphen length follows width (× √ of the H width ratio): 502 Condensed Thin → 845 Extended. En dash = hyphen × 1.256 (Regular's ratio); em dash unchanged.
- **Acceptance:** H/O/n/o sidebearings differ between Condensed and Extended masters ✅; the three dashes share one centre and thickness in every master ✅; every accented letter's width equals its base in the export except Ï (+20 each side by design) ✅.

## W3 — Kerning — ✅ built and saved 2026-11-12

- **Copied kerning cleared:** the June steal (257 class pairs, the same in every master) is gone; backup with the measuring script and its output in `_tmp/2026-11-12-kerning-backup/`.
- **Groups:** C/Ç and c/ç got their own right groups (they shared O/o's, though their right side is open); F and L their own right groups (they shared E's); ß's left side moved from the j group to n; `zero.zero` takes zero's groups. New punctuation groups: period (. , …), colon (: ;), quote (‘ ’ “ ” ' "), quotebase (‚ „), hyphen (- – —), guillemets.
- **Measured from Rót's own outlines, per master** (Dylgjur's method, ARCHITECTURE §7): white space between the shapes line by line, weighted to the middle, compared with the font's rhythm (HH caps, nn lowercase, Hn mixed) at that master; × 0.55, × 0.3 when a round side is involved; collision guard ⅓ of the HH gap; ceiling one HH gap; straight-against-stem capped at −20; T/V/Y/F/P/quote onto n follow their value onto o. Not kerned: lowercase→capital, punctuation→punctuation, positive values.
- **Result:** 1,113 pairs in every master (273 explicit zeros fill cross-master gaps), all class-to-class. Regular samples: T·A −200, A·V −140, T·o −80, Y·o −80, O·A −35, A·H −20, 7·4 −175. Thin Condensed: T·A −115, A·V −70. Black Extended: T·A −185, A·V −185.
- **Acceptance:** audit clean — 0 glyph-level pairs, 0 stale group keys, every letter and figure grouped ✅; T·o and Y·o kerned ✅; Condensed and Extended values differ ✅.
- **Check by eye:** the ceiling pairs (L·T, P/F/T/V·period, quote·A, r·period, hyphen·T at −200 Regular) may want to go tighter or looser; round-against-diagonal (O·A −35) is where measurement and eye disagree most; Condensed Thin punctuation sets very tight.

## W4 — Punctuation and symbols — ✅ built and saved 2026-11-12

- **nbspace (U+00A0), added 2026-11-12 (his catch):** the source had only `space`; Glyphs had been mapping U+00A0 onto it at export. Now its own empty glyph, width keyed to space (`=space`) in every master, like Dylgjur. Kept unsaved — he was editing in Glyphs at the time.
- **Built from existing parts:** soft hyphen (the hyphen; hyphen kerning group), ¦ (two cut-down bars), ¯ (a bar at accent height, 0.6 of the hyphen's thickness).
- **ƒ, rebuilt 2026-11-12 (his correction: *"not just an f"*):** f + the dotless j's descender and hook, j's stem aligned on f's stem in every master, both slanted 10° about the baseline (the family's italic angle); f's sidebearings; descender lands at j's depth (−376 to −384). Built from components, so it follows any change to f or j. Not tagged.
- **µ, rebuilt 2026-11-12 (his correction: *"mu is not just an u"*):** u + the dotless i's stem moved down to p's descender depth (−360), on u's left stem in every master; u's width and kerning groups. Built from components. Not tagged.
- **Estimates, tagged light blue for him to draw** (component-built so they render, but not designs): ª º (a/o at 60 %, top on the cap height), ¹ ² ³ (figures at 60 %), ¼ ½ ¾ (figures at 50 % around the slash), ¥ (Y + =), † (plus stretched), ‡ (two pluses), ¤ (o).

## W5 — Western European letters — ✅ built and saved 2026-11-12

- `caroncomb` and `caroncomb.case`: the circumflex marks flipped vertically, with their anchors. S, Z, s and z had no `top` anchor; added (centred, at O/o's accent height).
- Š š Ž ž composed on anchors in all nine masters; they take S/s/Z/z's kerning groups.
- **Acceptance:** Windows-1252 complete in the export (287 glyphs, nothing missing) ✅.

## W6 — Vertical metrics and metadata — ✅ built and saved 2026-11-12

- **winAscent / winDescent 1840 / 470** on all nine masters (were 1800 / 360): the real extremes, √ at the top (Thin Condensed) and ∫ at the bottom (Black Condensed); g j y @ © no longer clip on Windows. Typo and hhea keep their line spacing (1800 / −360 / 100).
- † and ‡ estimates refitted to cap height first (the first build reached 2154).
- **Metadata:** copyright "Copyright 2026 Tór Grímsson", licence "This Font Software is licensed under the SIL Open Font License, Version 1.1.", manufacturer Kolkrabbi, manufacturer URL https://kolkrabbi.io. Licence URL and vendor ID not set (the API refused the URL; the sibling families carry neither).
- **Acceptance:** read back from the export — name IDs 0, 8, 11, 13 present; win 1840/470; fvar default 400/100 Regular; OS/2 400/5 ✅.

## W7 — Italic — ✅ built and saved 2026-11-12

- The `TGRot-Italic.glyphspackage` saved from the June italic (4 masters, 274 glyphs, none of W1–W6) is parked with `tg-rot-italic.glyphs` in `_tmp/2026-11-12-june-italic/`. The Italic is now a copy of the finished Roman.
- **Slant:** every outline and anchor sheared 10° around half the x-height, advance widths unchanged. Auto-aligned accents follow their sheared anchors, so nothing slants twice. 38 glyphs built from flipped, rotated or stretched parts (n m u r p q d V 9, brackets, guillemets, the caron, † ‡ ¦, Î) are plain outlines in the Italic only; the Roman keeps its part-built letters. ƒ drops its own 10° shear, since f and j are now slanted underneath it.
- Italic angle 10 on all nine masters; the 35 styles renamed "… Italic" (Regular → Italic), flagged italic and style-linked to the Roman; the variable font is `TGRotItalicVF`.
- **Kerning:** measured on the Italic's own outlines (1,067 pairs in every master, audit clean), not inherited from the Roman, because the slant moves the gaps (T·o −55 Italic vs −80 Roman at Regular).
- **Acceptance:** export reads style Italic, italic angle −10, italic bit set, Regular default; proof at three styles clean.

## W3 addendum — kerning guards (2026-11-12, found on the Italic proof)

- Lowercase against high or low marks (quotes, „) barely share a height, so the first measurement kerned them on almost nothing (y·” −135 in Condensed Thin; the quote slid into the letter). Two guards added to the measurement: the ⅓-HH collision gap is checked over the full height of both shapes, and shapes that share less than 20 % of their height may not overlap sideways. Roman re-measured and rewritten (1,113 pairs, audit clean); Condensed Thin y·” −135 → −70, ‘·o −110 → −80; Regular unchanged where it already cleared. Script and outputs in `_tmp/2026-11-12-kerning-backup/`.

## Pre-export — metrics sync check (playbook § 3)

- **Roman — ✅ 2026-11-12:** Update Metrics moved 47 master layers in 8 glyphs, all toward their keys: i (stem 22 units off-centre, 84/40 → 62/62 like h), zero.zero, guillemetright, plus, approxequal, quotedbl (made symmetric like their key glyphs), OE (right side follows E), endash Thin (follows period). Kept as corrections and saved; a second pass moves nothing.
- **Italic — synced 2026-11-12, saving left to him:** the same glyphs moved (58 master layers: i, zero.zero, guillemetright, plus, approxequal, greaterequal, quotedbl, OE, endash). Measured along the 10° angle the values match the Roman exactly, which confirms the shear around half the x-height kept the keys valid. Kept in Glyphs, not saved, because the Italic also held his own unsaved edits.
- **Kerning — ✅ 2026-11-12:** both styles re-measured after the sync; 0 pairs changed (only » represents a group among the moved glyphs, and its pairs sit at the guards either way). Kerning stands; next is the export.

## Export and proofs — 2026-11-12

- 70 static OTFs (35 Roman, 35 Italic; Remove overlaps, Autohint) next to the two VFs, as Gullhamrar ships. Missed in the first export and added after he noticed it; now a playbook rule (§ 3).
- `proof-family` reprinted with a full page per named style (charset, kerning, spacing, text), masters marked: 95 pages. The first print checked charset, kerning and spacing only at the masters.

Open items: [[OPEN|OPEN.md]].
