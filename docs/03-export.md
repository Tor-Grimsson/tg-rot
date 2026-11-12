---
title: TG Rót — export
type: playbook
status: active
updated: 2026-11-12
description: Glyphs exports the shipping TGRotVF.ttf directly — Regular default from the 3 × 3 master grid, no build step.
audience: internal
aliases:
  - tg-rot-export
tags:
  - project/kol-foundry
  - domain/typography
---

# TG Rót — export

Since 2026-11-12 Glyphs exports the shipping font directly. The source has nine masters (Thin, Regular, Black × Condensed, Normal, Extended) with `Variable Font Origin` on Regular, so the default style is **Regular / Normal** (wght 400, wdth 100) straight out of Glyphs. The old `build.sh` step that rebased the default and the `export/raw/` folder are retired in `_tmp/2026-11-12-build-scripts/` and `_tmp/2026-11-12-raw-export/`.

```
glyphs/TGRot-Roman.glyphspackage ──Glyphs File › Export › Variable Font──▶ export/TGRotVF.ttf
glyphs/TGRot-Italic.glyphspackage ──Glyphs File › Export › Variable Font──▶ export/TGRotItalicVF.ttf
```

## 0. Prerequisites

- Every master and instance carries its userspace weight (100–900) and width (64–172) in Glyphs' axis settings. A new master or instance needs them set, or the export stops with "Instance is outside of the interpolation space".

## 1. Export

In Glyphs, File › Export › Variable Font, into `export/`. Overwrite freely.

## 2. Verification

- fvar default `wdth 100 / wght 400`, named Regular; OS/2 weight 400, width 5.
- 35 named instances, no duplicates.
