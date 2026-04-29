# PPT Skill

A Claude Code Skill for creating presentation-grade decks. Install it, then just talk — Claude guides you through topic selection, outlining, visual system, generation, verification, and export.

## How to Use

### 1. Install

Place the entire directory in your project, or use a symlink:

```bash
# Option A: copy into project
cp -r ppt-skill /path/to/your-project/.claude/skills/ppt-skill

# Option B: symlink (recommended, reuse across projects)
ln -s /path/to/ppt-skill /path/to/your-project/.claude/skills/ppt-skill
```

### 2. Generate by conversation

After installation, describe your presentation in plain language inside Claude Code. Claude will follow the workflow defined in SKILL.md and guide you through each step.

**Example conversation:**

```
You: Help me create a 30-minute presentation on AI Agents for a tech team

Claude: Sure, let me clarify a few things first:
1. What's the setting? (internal tech talk / conference / demo day)
2. Do you have existing materials? (docs, articles, old decks)
3. Which visual style? I have 5 preset themes to choose from
...

You: Internal tech talk, I have a Notion doc, let's go with Indigo Porcelain

Claude: Got it. I'll read your doc, draft an outline for your approval, then start generating.
```

Claude follows this pipeline:

```
Clarify inputs → Choose architecture → Build visual system → Generate content → Verify → Export
```

No coding required — just answer questions and confirm proposals.

### 3. Export

After generation, export to multiple formats as needed:

```bash
# Verify (multi-viewport screenshots + console error detection)
python3 scripts/verify.py my-deck/index.html --viewports 1920x1080,375x667

# PDF (vector text)
node scripts/export_deck_pdf.mjs --slides my-deck/slides --out my-deck/deck.pdf

# Editable PPTX (double-click to edit in PowerPoint/WPS)
node scripts/export_deck_pptx.mjs --slides my-deck/slides --out my-deck/deck.pptx

# Presentation video MP4 (requires global Playwright + ffmpeg)
NODE_PATH=$(npm root -g) node scripts/render-video.js my-deck/index.html --duration=30

# Convert MP4 to 60fps / GIF
bash scripts/convert-formats.sh my-deck/index.mp4 960

# Add BGM to video
bash scripts/add-music.sh my-deck/index.mp4 --mood=tech
```

> Dependencies (install as needed):
> - PDF/PPTX/verification: `pip install playwright && playwright install chromium` and `npm install playwright pdf-lib pptxgenjs sharp`
> - Video recording: `npm install -g playwright && playwright install chromium`, plus ffmpeg

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
- **Presentation audio**: 3 scene-based BGM tracks + 34 SFX presets, auto-mixing support
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
│   ├── examples/                          # Example projects
│   └── audio/
│       ├── bgm/                          # 3 scene-based BGM tracks (tech / tutorial / educational)
│       └── sfx/                          # 34 sound effects (8 categories)
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

## License

This is a merged derived project:

- Single-file magazine template, animation system, layouts, themes and checklists from `guizang-ppt-skill` (MIT License)
- Multi-file deck architecture, export scripts, verification scripts, audio assets and design methodology from `huashu-design` (Personal Use License)

Personal learning and creative use is permitted. For enterprise, team, commercial delivery or paid service use, you must comply with the upstream `huashu-design` licensing terms. See `LICENSE`.
