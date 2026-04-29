# PPT Skill

A merged HTML presentation Claude Code Skill. Combines the editorial visual system from `guizang-ppt-skill` with the engineering export capabilities from `huashu-design` to produce presentation decks that can be presented, screenshotted, exported, or further edited.

## Features

### Visual System

- **WebGL dual backgrounds**: Holographic dispersion (dark) + spiral vortex (light), auto-revealed on hero pages
- **Motion One animations**: 5 entrance recipes (cascade / hero / quote / directional / pipeline), offline-capable
- **5 preset themes**: Monocle, Indigo Porcelain, Forest Ink, Kraft Paper, Dune — no custom hex allowed to protect aesthetics
- **Magazine components**: typography system, stat cards, callouts, platform cards, pipelines, image frames, Lucide icons
- **10 page layouts**: cover, act divider, big numbers, quote+image, image grid, pipeline, hero question, big quote, before/after, lead image

### Engineering

- **Three architectures**: single-file horizontal scroll (≤10 pages), multi-file iframe splicing (10+ pages), deck-stage web component
- **Full format export**: PDF (vector text), editable PPTX (double-click edit), MP4 (25/60fps), GIF (palette optimized)
- **Presentation audio**: 3 scene-based BGM tracks + 31 SFX presets, auto-mixing support
- **Playwright verification**: multi-viewport screenshots, console error detection

### Design Methodology

- **Anti-AI Slop checklist**: systematically avoid purple gradients, emoji icons, rounded-corner cards and other AI cheapness
- **Brand asset protocol**: quick asset collection flow when dealing with specific brands
- **Design direction advisor**: recommend 3 differentiated directions from 5 style schools when requirements are vague
- **Visual protagonist diversity**: 10 visual element types to rotate, preventing every page from looking the same
- **Quality checklist**: P0-P3 severity tiers + mandatory class name preflight + animation self-check

## Structure

```text
ppt-skill/
├── SKILL.md                              # Core skill definition (workflow + principles + checklists)
├── README.md / README.en.md
├── LICENSE
├── assets/
│   ├── templates/
│   │   ├── single-file-magazine.html     # Magazine-style single-file template (CSS + WebGL + JS + animations)
│   │   ├── deck_index.html               # Multi-file deck splicer
│   │   └── deck_stage.js                 # <deck-stage> web component
│   ├── motion.min.js                     # Motion One animation library (offline fallback, 64KB)
│   └── audio/
│       ├── bgm/                          # 3 scene-based BGM tracks (tech / tutorial / educational)
│       └── sfx/                          # 31 sound effects (8 categories)
├── references/
│   ├── architecture.md                   # Single-file vs multi-file vs deck-stage architecture
│   ├── layouts.md                        # 10 page layout skeletons (with animation markers)
│   ├── components.md                     # Component handbook (typography, stats, callouts, figures, animations)
│   ├── slide-design.md                   # Design rules (density, rhythm, visual protagonist, Speaker Notes)
│   ├── themes.md                         # 5 preset color themes
│   ├── image-prompts.md                  # GPT-M 2.0 image generation prompts and ratios
│   ├── checklist.md                      # Quality checklist (P0-0 preflight + P0-P3 + animation self-check)
│   ├── audio.md                          # SFX / BGM rules and mixing templates
│   ├── editable-pptx.md                  # Hard constraints for editable PPTX export
│   └── workflow.md                       # Quick workflow reference
└── scripts/
    ├── verify.py                         # Playwright verification
    ├── html2pptx.js                      # HTML DOM → PowerPoint converter
    ├── render-video.js                   # HTML animation → MP4
    ├── export_deck_pdf.mjs               # Multi-file → PDF
    ├── export_deck_pptx.mjs              # Multi-file → editable PPTX
    ├── export_deck_stage_pdf.mjs         # Single-file deck-stage → PDF
    ├── convert-formats.sh                # MP4 → 60fps MP4 + GIF
    └── add-music.sh                      # Mix BGM into video
```

## Quick Start

### Single-file magazine deck

```bash
mkdir -p my-deck/images
cp assets/templates/single-file-magazine.html my-deck/index.html
# For offline animations, copy motion.min.js
mkdir -p my-deck/assets
cp assets/motion.min.js my-deck/assets/
open my-deck/index.html
```

### Multi-file deck

```bash
mkdir -p my-deck/slides my-deck/shared
cp assets/templates/deck_index.html my-deck/index.html
open my-deck/index.html
```

## Export & Verify

```bash
# Verify (multi-viewport screenshots + console error detection)
python3 scripts/verify.py my-deck/index.html --viewports 1920x1080,375x667

# PDF export
node scripts/export_deck_pdf.mjs --slides my-deck/slides --out my-deck/deck.pdf

# Editable PPTX export
node scripts/export_deck_pptx.mjs --slides my-deck/slides --out my-deck/deck.pptx

# Video export
node scripts/render-video.js my-deck/index.html --duration=30
bash scripts/convert-formats.sh my-deck/index.mp4 960

# Add BGM to video
bash scripts/add-music.sh my-deck/index.mp4 --mood=tech
```

Install dependencies as needed:

```bash
pip install playwright && playwright install chromium
npm install playwright pdf-lib pptxgenjs sharp
```

## Workflow Overview

1. **Clarify inputs**: audience, duration, materials, output format, theme, constraints
2. **Choose architecture**: single-file (≤10 pages) / multi-file (10+ pages) / deck-stage
3. **Establish visual system**: font roles, color rhythm, layout pool, image rules
4. **Generate content**: pick skeletons from layouts.md, use components from components.md
5. **Verify & export**: self-check with checklist.md → verify.py → export as needed

See `SKILL.md` for details.

## License

This is a merged derived project:

- Single-file magazine template, animation system, layouts, themes and checklists from `guizang-ppt-skill` (MIT License)
- Multi-file deck architecture, export scripts, verification scripts, audio assets and design methodology from `huashu-design` (Personal Use License)

Personal learning and creative use is permitted. For enterprise, team, commercial delivery or paid service use, you must comply with the upstream `huashu-design` licensing terms. See `LICENSE`.
