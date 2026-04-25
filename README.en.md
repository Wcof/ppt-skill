# PPT Skill

A merged HTML presentation skill. It combines the editorial single-file deck system from `guizang-ppt-skill` with the PPT-specific architecture, export scripts, verification flow, and presentation audio assets from `huashu-design`.

## Features

- Single-file magazine-style HTML decks for talks and launches.
- Multi-file HTML decks for long lectures, reports, and parallel slide work.
- HTML-first workflow with PDF, editable PPTX, MP4, and GIF exports.
- Optional presentation sound design with page transitions, clicks, focus cues, typing, and logo reveal effects.

## Structure

```text
ppt-skill/
├── SKILL.md
├── assets/templates/
├── assets/audio/
├── references/
└── scripts/
```

## Commands

```bash
python3 scripts/verify.py my-deck/index.html --viewports 1920x1080,375x667
node scripts/export_deck_pdf.mjs --slides my-deck/slides --out my-deck/deck.pdf
node scripts/export_deck_pptx.mjs --slides my-deck/slides --out my-deck/deck.pptx
node scripts/render-video.js my-deck/index.html --duration=30
bash scripts/convert-formats.sh my-deck/index.mp4 960
```

Install dependencies as needed: `pip install playwright && playwright install chromium`, and `npm install playwright pdf-lib pptxgenjs sharp`.

## License

This is a derived merge of two upstream projects. The magazine deck materials come from `guizang-ppt-skill` under MIT. The deck tooling and audio assets come from `huashu-design` under its Personal Use License. See `LICENSE` before commercial or organizational use.
