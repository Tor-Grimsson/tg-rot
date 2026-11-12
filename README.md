# TG Rót

Weight × width grotesque in Roman and Italic. Both are spaced and kerned from their own outlines and cover Windows-1252.

Read from the shipping fonts `export/TGRotVF.ttf` and `export/TGRotItalicVF.ttf` on 2026-11-12.

| | |
|---|---|
| Family name in the font | `TG Rot`, deliberately without the accent, which isn't safe in font names. TG Rót is the public (working) name. |
| Version | 1.000 (exported with Glyphs 4) |
| Format | Two variable TTFs, Roman and Italic (italic angle 10°); 70 static OTFs, one per style; WOFF2 of the VFs in `export/web/` |
| Glyphs | 288 |
| Masters | 9 per style: Thin, Regular and Black × Condensed, Normal and Extended |
| Default style | Regular / Italic (wght 400, wdth 100) |
| Licence | SIL Open Font License 1.1 (`OFL.txt`) |

## Axes

| Axis | Min | Default | Max |
|---|---|---|---|
| Weight `wght` | 100 | 400 | 900 |
| Width `wdth` | 64 | 100 | 172 |

## Styles — 35 per style (7 weights × 5 widths)

| Weight | Condensed (64) | SemiCondensed (82) | Normal (100) | SemiExpanded (136) | Expanded (172) |
|---|---|---|---|---|---|
| Thin 100 | Thin Condensed | Thin SemiCondensed | Thin | Thin SemiExpanded | Thin Expanded |
| Light 300 | Light Condensed | Light SemiCondensed | Light | Light SemiExpanded | Light Expanded |
| Regular 400 | Regular Condensed | Regular SemiCondensed | Regular | Regular SemiExpanded | Regular Expanded |
| Medium 500 | Medium Condensed | Medium SemiCondensed | Medium | Medium SemiExpanded | Medium Expanded |
| SemiBold 600 | SemiBold Condensed | SemiBold SemiCondensed | SemiBold | SemiBold SemiExpanded | SemiBold Expanded |
| Bold 700 | Bold Condensed | Bold SemiCondensed | Bold | Bold SemiExpanded | Bold Expanded |
| Black 900 | Black Condensed | Black SemiCondensed | Black | Black SemiExpanded | Black Expanded |

The Italic has the same 35 with "Italic" added (Regular → Italic). There are no ExtraLight (200) or ExtraBold (800) styles.

## Files

| Folder | Holds |
|---|---|
| `glyphs/` | `TGRot-Roman.glyphspackage`, `TGRot-Italic.glyphspackage` |
| `export/` | `TGRotVF.ttf`, `TGRotItalicVF.ttf` and 70 static `.otf` (ship straight from Glyphs); `web/` WOFF2 |
| `specimen/` | proofs (not in git; rebuilt with `tools/kol-specimen/make-proof.sh` in kol-foundry) |
| `docs/` | evaluation, plan (W1–W7), export steps |
