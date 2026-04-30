# 工作流

## 1. 先确认交付格式

HTML 是源文件。PDF、PPTX、MP4、GIF 都从 HTML 衍生。

开始制作前先判断输入是否充分。只有用户已经明确受众/场景、时长或页数、可直接转成 slide 的大纲、交付格式、视觉方向和素材使用方式时，才能跳过澄清。

以下信息不构成充分输入：原始文档、产品介绍、网页链接、旧资料、"深色/科技感/高级/简洁"这类模糊风格词，或"全自动/你看着办"这类授权式表达。澄清是需求对齐，不是权限确认；缺少关键信息时，即使用户要求直接做，也要先问最影响结构的 1-3 个问题。

先问用户要什么：

- 只要 HTML：视觉自由度最高。
- HTML + PDF：视觉保真，适合演讲、存档、群发。
- HTML + 可编辑 PPTX：从第一行 HTML 就遵守 `editable-pptx.md`，牺牲渐变、web component、复杂 SVG。
- HTML + MP4/GIF：按 `audio.md` 规划 SFX / BGM，导出视频后合成声音。

## 2. 先定大纲

没有大纲时，用叙事弧搭骨架：

```text
Hook -> Context -> Core -> Shift -> Takeaway
```

页数建议：

- 15 分钟：8-12 页。
- 30 分钟：16-22 页。
- 45 分钟：24-30 页。

## 3. 选择架构

- `single-file-magazine.html`：10 页以内，强杂志风，单 HTML 交付。
- `deck_index.html`：10 页以上，长讲座、课程、报告、多人并行。
- `deck_stage.js`：小型 deck，且需要 web component 外壳或跨页共享状态。

## 4. 先做 2 页 showcase

Deck 大于等于 5 页时，不要直接批量写完。先做视觉差异最大的两页，例如封面 + 内容页、封面 + 产品页、数据页 + 结论页。确认字体、颜色、页眉、密度、图片处理和节奏后，再批量生成剩余页面。

## 5. 批量生成

生成时按这个顺序：

1. 写主题节奏表：每页是 `hero dark`、`hero light`、`light` 还是 `dark`。
2. 选布局：优先从 `layouts.md` 复制骨架。
3. 填文案：一页一个核心信息，辅助点 3-4 个以内。
4. 放图片：相对路径，标准比例，顶部和左右不能裁切。
5. 写页眉页脚：chrome 是栏目标签，kicker 是本页钩子。

## 6. 验证和导出

每次交付前至少做：

```bash
python3 scripts/verify.py path/to/index.html --viewports 1920x1080,375x667
```

再按目标格式导出：

```bash
node scripts/export_deck_pdf.mjs --slides ./slides --out deck.pdf
node scripts/export_deck_pptx.mjs --slides ./slides --out deck.pptx
node scripts/render-video.js ./index.html --duration=30
```
