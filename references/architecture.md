# Deck 架构

## HTML-first 原则

不管最终交付是 HTML、PDF、PPTX 还是视频，都先做 HTML 演示版。HTML 是唯一源文件，避免后续改稿时多格式手动同步。

## 路径 A: 单文件杂志风

适合：

- 10 页以内。
- 发布会、私享会、个人分享。
- 需要横向翻页、WebGL 背景、强杂志感。

起步：

```bash
mkdir -p my-deck/images
cp assets/templates/single-file-magazine.html my-deck/index.html
open my-deck/index.html
```

核心规则：

- 每页是 `<section class="slide ...">`。
- 主题必须写 `hero dark`、`hero light`、`light` 或 `dark`。
- 使用 `layouts.md` 前，确认模板 CSS 已定义相关类名。

## 路径 B: 多文件 deck

适合：

- 10 页以上。
- 学术讲座、课程、报告、长 deck。
- 多 agent 或多人并行开发。
- 需要逐页隔离 CSS 和单页验证。

结构：

```text
my-deck/
├── index.html
├── shared/
│   └── tokens.css
└── slides/
    ├── 01-cover.html
    ├── 02-agenda.html
    └── 03-problem.html
```

起步：

```bash
mkdir -p my-deck/slides my-deck/shared
cp assets/templates/deck_index.html my-deck/index.html
```

只需要修改 `index.html` 中的 `window.DECK_MANIFEST`：

```js
window.DECK_MANIFEST = [
  { file: "slides/01-cover.html", label: "Cover" },
  { file: "slides/02-agenda.html", label: "Agenda" }
];
```

每张 slide 都应能独立打开：

```bash
open my-deck/slides/01-cover.html
```

## 路径 C: deck-stage

适合小型单文件 deck，或需要 `<deck-stage>` web component 外壳的场景。

```html
<deck-stage>
  <section data-screen-label="01 Cover">...</section>
  <section data-screen-label="02 Problem">...</section>
</deck-stage>
<script src="deck_stage.js"></script>
```

脚本放在 `</deck-stage>` 后，或在 `<head>` 中加 `defer`。不要让 section 自身承担复杂 `display:flex/grid` 规则，布局写到内部 wrapper，避免所有 slide 同时显示。

## 架构选择默认值

- 不确定时，10 页以内用单文件杂志风。
- 10 页以上用多文件 deck。
- 要可编辑 PPTX 时，优先多文件，并按 `editable-pptx.md` 写。
