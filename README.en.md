# PPT Skill

A Claude Code Skill for creating presentation-grade decks. Install it, then just talk — Claude guides you through topic selection, outlining, visual system, generation, verification, and export.

![PPT Skill Overview](assets/project-overview.svg)

## How to Use (3 Steps)

### Step 1: Install the skill into your project

Say your project lives at `~/my-project/`. Just clone this repo into the `.claude/skills/` directory inside your project:

```bash
cd ~/my-project/
mkdir -p .claude/skills
git clone https://github.com/Wcof/ppt-skill.git .claude/skills/ppt-skill
```

Your project will then look like this:

```
my-project/
├── .claude/
│   └── skills/
│       └── ppt-skill/        ← this repo
│           ├── SKILL.md
│           └── ...
└── ...（your project files）
```

> **Why here?** Claude Code automatically reads skill files from `.claude/skills/` in your project. No extra config needed — Claude picks it up on its own.

> **Want to use it in multiple projects?** Clone once, then symlink:
> ```bash
> git clone https://github.com/Wcof/ppt-skill.git ~/ppt-skill
> mkdir -p ~/my-project/.claude/skills
> ln -s ~/ppt-skill ~/my-project/.claude/skills/ppt-skill
> ```

### Step 2: Open Claude Code and tell it what you want

Open your terminal, `cd` into your project, and start Claude Code:

```bash
cd ~/my-project/
claude
```

Then just describe your presentation in plain language:

```
Help me create a 30-minute presentation on AI Agents for a tech team
```

**Claude will guide you — no commands to memorize.** The conversation goes something like:

```
You: Help me create a 30-minute presentation on AI Agents for a tech team

Claude: Sure, let me clarify a few things first:
1. What's the setting? (internal tech talk / conference / demo day)
2. Do you have existing materials? (docs, articles, old decks)
3. Which visual style? I have 5 preset themes to choose from
...

You: Internal tech talk, I have a Notion doc, let's go with Indigo Porcelain

Claude: Got it. I'll read your doc, draft an outline for your approval.
```

Claude walks you through this pipeline step by step:

```
Ask about your needs → Draft outline (for your approval) → Pick visual style → Generate pages → Quality check → Export
```

**All you do is answer questions and confirm — zero coding required.**

### Step 3: Export to your desired format

After generation, Claude will ask what format you want. You can also run the commands yourself:

```bash
# Verify (check for rendering errors)
python3 scripts/verify.py my-deck/index.html --viewports 1920x1080,375x667

# Export PDF
node scripts/export_deck_pdf.mjs --slides my-deck/slides --out my-deck/deck.pdf

# Export editable PPTX (double-click to edit in PowerPoint / WPS)
node scripts/export_deck_pptx.mjs --slides my-deck/slides --out my-deck/deck.pptx

# Export presentation video MP4
NODE_PATH=$(npm root -g) node scripts/render-video.js my-deck/index.html --duration=30

# Convert MP4 to 60fps or GIF
bash scripts/convert-formats.sh my-deck/index.mp4 960

# Add background music to video
bash scripts/add-music.sh my-deck/index.mp4 --mood=tech
```

> Export requires extra tools (the skill still works without them — you just can't export):
> - PDF / PPTX / verification: `pip install playwright && playwright install chromium` + `npm install playwright pdf-lib pptxgenjs sharp`
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
