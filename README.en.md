# PPT Skill

A Claude Code Skill for creating presentation-grade decks. Install it, then just talk to Claude — no coding required.

![PPT Skill Overview](assets/project-overview.svg)

## How to Use

### Step 1: Install into your project (1 minute)

Open your terminal, `cd` into the project where you want to make a presentation, then run:

```bash
mkdir -p .claude/skills
git clone https://github.com/Wcof/ppt-skill.git .claude/skills/ppt-skill
```

> Don't use git? Go to the GitHub page, click "Code → Download ZIP", and extract it to `.claude/skills/ppt-skill`.

Your project will look like this:

```
your-project/
├── .claude/
│   └── skills/
│       └── ppt-skill/        ← this repo
│           ├── SKILL.md
│           └── ...
└── ...（your existing files）
```

**Why here?** Claude Code automatically reads skill files from `.claude/skills/` in your project. No config needed — Claude picks it up on its own.

### Step 2: Tell Claude what presentation you want

Start Claude Code in the same project directory:

```bash
claude
```

Then just describe what you need in plain language:

```
Help me create a 30-minute presentation on AI Agents for a tech team
```

**Claude will ask you questions, draft an outline, and generate the slides — you just answer and confirm.** The conversation goes like:

```
You: Help me create a 30-minute presentation on AI Agents for a tech team

Claude: Sure, let me clarify a few things first:
1. What's the setting? (internal tech talk / conference / demo day)
2. Do you have existing materials? (docs, articles, old decks)
3. Which visual style? I have 5 preset themes to choose from

You: Internal tech talk, I have a Notion doc, let's go with Indigo Porcelain

Claude: Got it. I'll read your doc, draft an outline for your approval, then start generating.
```

Claude walks you through the full pipeline:

```
Ask about your needs → Draft outline (for your approval) → Pick visual style → Generate pages → Quality check → Export
```

**All you do is answer questions and confirm — zero coding required.**

### Step 3: Export

When your deck is ready, just tell Claude what format you want:

- `Export as PDF`
- `Export as an editable PPTX`
- `Export as a presentation video`
- `Add background music to the video`

Claude runs the commands for you. You can also run them yourself later — see the `scripts/` directory.

> Some export features (PDF, PPTX, video) need extra tools installed. If you don't need exports, you can skip this entirely — the generation itself has zero dependencies.

## What It Can Do

| Capability | Description |
|------------|-------------|
| **Magazine visuals** | WebGL animated backgrounds, 5 entrance animations, 10 page layouts, 5 preset themes |
| **Multiple export formats** | PDF, editable PPTX (double-click to edit in PowerPoint/WPS), MP4, GIF |
| **Presentation audio** | 3 background music tracks + 34 sound effects, auto-mixed into video |
| **Auto quality check** | Multi-viewport screenshot verification, rendering error detection, anti-AI-slop design checklist |
| **Flexible architecture** | Single-file horizontal scroll for ≤10 pages, multi-file splicing for 10+ pages |

## Advanced: Directory Structure

```text
ppt-skill/
├── SKILL.md                              # Core skill definition (what Claude reads)
├── assets/
│   ├── templates/                         # HTML templates (single-file / multi-file / web component)
│   ├── motion.min.js                      # Animation library (offline fallback)
│   ├── examples/                          # Example projects
│   └── audio/                             # BGM + sound effects
├── references/                            # Design specs (layouts, components, themes, checklists)
└── scripts/                               # Export + verification scripts
```

## License

This is a merged derived project:

- Single-file magazine template, animation system, layouts, themes and checklists from `guizang-ppt-skill` (MIT License)
- Multi-file deck architecture, export scripts, verification scripts, audio assets and design methodology from `huashu-design` (Personal Use License)

Personal learning and creative use is permitted. For enterprise, team, commercial delivery or paid service use, you must comply with the upstream `huashu-design` licensing terms. See `LICENSE`.
