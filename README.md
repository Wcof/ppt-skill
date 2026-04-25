# PPT Skill

融合版网页版 PPT skill。它把 `guizang-ppt-skill` 的电子杂志风单文件横向翻页体系，和 `huashu-design` 中与 PPT 直接相关的 deck 架构、导出工具、验证流程和演示音效整合到一个项目中。

## 能做什么

- 生成单文件 HTML 横向翻页 PPT，适合发布会、私享会、个人分享。
- 生成多文件 HTML deck，适合长讲座、课程、报告和并行制作。
- 从 HTML 导出 PDF、可编辑 PPTX、MP4、GIF。
- 为演示视频添加翻页、点击、聚焦、键盘、过渡和品牌落点音效。

## 目录结构

```text
ppt-skill/
├── SKILL.md
├── assets/
│   ├── templates/
│   │   ├── single-file-magazine.html
│   │   ├── deck_index.html
│   │   └── deck_stage.js
│   └── audio/
│       ├── bgm/
│       └── sfx/
├── references/
└── scripts/
```

## 快速开始

单文件杂志风 PPT：

```bash
mkdir -p my-deck/images
cp assets/templates/single-file-magazine.html my-deck/index.html
open my-deck/index.html
```

多文件 deck：

```bash
mkdir -p my-deck/slides my-deck/shared
cp assets/templates/deck_index.html my-deck/index.html
open my-deck/index.html
```

## 导出与验证

```bash
python3 scripts/verify.py my-deck/index.html --viewports 1920x1080,375x667
node scripts/export_deck_pdf.mjs --slides my-deck/slides --out my-deck/deck.pdf
node scripts/export_deck_pptx.mjs --slides my-deck/slides --out my-deck/deck.pptx
node scripts/render-video.js my-deck/index.html --duration=30
bash scripts/convert-formats.sh my-deck/index.mp4 960
```

依赖按需安装：`pip install playwright && playwright install chromium`，以及 `npm install playwright pdf-lib pptxgenjs sharp`。

## 来源与许可

本项目是融合派生项目：

- 单文件杂志风模板、布局、主题和检查清单来自 `guizang-ppt-skill`，原项目 MIT License。
- 多文件 deck、导出脚本、验证脚本和音频资产来自 `huashu-design`，原项目为 Personal Use License。

因此本融合项目按 `LICENSE` 中的组合许可说明使用：个人学习和创作可用；涉及企业、团队、商业交付或付费服务时，需要遵守上游 `huashu-design` 的授权要求。
