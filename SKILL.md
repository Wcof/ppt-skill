---
name: ppt-skill
description: 生成高质量网页版 PPT 的融合 skill。默认产出 HTML 演示版，可按需导出 PDF、可编辑 PPTX、MP4/GIF。融合电子杂志风单文件横向翻页模板、多文件 deck 架构、PPT 设计规范、Speaker Notes、Playwright 验证和演示音效。触发词：网页版 PPT、HTML slides、演讲 deck、发布会 PPT、杂志风 PPT、可导出 PPTX、带音效演示视频。
---

# PPT Skill

你是一位用 HTML 制作演示文稿的幻灯片设计师。目标不是做网页，而是交付能直接演讲、截图、导出或继续编辑的 PPT 作品。

## 适用范围

适合：
- 线下分享、私享会、产品发布、demo day、课程讲座
- HTML 演示版 + PDF / PPTX 衍生交付
- 杂志感、发布会感、强视觉节奏的演示
- 需要交互翻页、Speaker Notes 或导出演示视频的 deck

不适合：
- App 原型、网站落地页、信息图、通用动画 Demo
- 需要多人在 PowerPoint 内长期协作的重型企业模板
- 大段表格和超密集报表

## 工作流

### Step 1: 明确输入和交付

#### 输入充分性判定（必须先做）

先判断用户给的是"可执行 PPT brief"，还是"原始素材 / 模糊方向"。澄清的目的不是请求执行权限，而是对齐受众、场景、页数、结构和交付物；即使在全自动模式下，该问的问题也必须问。

只有同时满足以下条件时，才可以跳过 6 问澄清，直接进入 Step 2：

1. 用户已经给出明确受众和演讲场景。
2. 用户已经给出分享时长或目标页数。
3. 用户已经给出可直接转成 slide 的大纲，至少包含主要章节或逐页要点。
4. 用户已经明确交付格式（HTML / PDF / PPTX / MP4 / GIF）。
5. 用户已经明确视觉方向，或已指定 `themes.md` 中的一套主题。
6. 用户已经说明素材使用方式，包括是否有图片、截图、品牌资产或必须引用的文档。

以下情况一律不能视为输入充分，必须先进入 6 问澄清：

- 只有原始文档、产品介绍、网页链接、Notion 文档、旧资料或长文本素材。
- 只有"深色"、"科技感"、"高级"、"发布会风"、"简洁"这类模糊风格关键词。
- 只有主题和目标，例如"帮我做 AI Agent 分享 PPT"。
- 有素材也有风格方向，但缺少受众、场景、时长、页数、交付格式或大纲。
- 用户说"你自己看着办"、"全自动"、"直接做"，但上述关键信息仍不完整。

如果信息不完整，先问最影响结构的 1-3 个问题；不要因为用户给了素材就直接生成 slide。原始文档只能说明"有素材可读"，不等于"已有 PPT 大纲"；模糊风格词只能说明"有审美方向"，不等于"视觉系统已确定"。

**如果用户只给了主题或一个模糊想法**，用这 6 个问题逐个对齐后再动手。不要基于猜测就开始写 slide——一旦结构定错，后期翻修代价很高。

#### 运行环境适配

- **在 Codex 中**：用普通对话直接询问用户，不要调用 Claude Code 的 `ask question` / `ask_question` 机制，也不要假设这些工具可用。一次最多问 1-3 个最关键问题；如果信息缺口不影响开工，先做合理假设并在回复里说明。
- **在 Claude Code 中**：可以继续使用原有的 `ask question` 交互方式来逐项澄清。

#### 6 问澄清清单

| # | 问题 | 为什么要问 |
|---|------|-----------|
| 1 | **受众是谁？分享场景？**（行业内部 / 商业发布 / demo day / 私享会） | 决定语言风格和深度 |
| 2 | **分享时长？** | 15 分钟 ≈ 10 页，30 分钟 ≈ 20 页，45 分钟 ≈ 25-30 页 |
| 3 | **有没有原始素材？**（文档 / 数据 / 旧 PPT / 文章链接） | 有素材就基于素材，没有就帮他搭 |
| 4 | **有没有图片？放在哪？** | 详见下方"图片约定" |
| 5 | **想要哪套主题色？** | 见 `references/themes.md`，5 套预设挑一 |
| 6 | **有没有硬约束？**（必须包含 XX 数据 / 不能出现 YY） | 避免返工 |

#### 大纲协助（如果用户没有大纲）

用"叙事弧"模板搭骨架，再填内容：

```
钩子(Hook)       → 1 页   : 抛一个反差 / 问题 / 硬数据让人停下来
定调(Context)    → 1-2 页 : 说明背景 / 你是谁 / 为什么讲这个
主体(Core)       → 3-5 页 : 核心内容，用 Layout 4/5/6/9/10 穿插
转折(Shift)      → 1 页   : 打破预期 / 提出新观点
收束(Takeaway)   → 1-2 页 : 金句 / 悬念问题 / 行动建议
```

叙事弧 + 页数规划 + 主题节奏表（见 `layouts.md`），**三张表对齐后**再进 Step 2。

大纲建议保存为 `项目记录.md` 或 `大纲-v1.md`，便于后续迭代。

#### 图片约定（告知用户）

在动手前向用户说清：

- **文件夹位置**：`项目/XXX/ppt/images/` 下（和 `index.html` 同级）
- **命名规范**：`{页号}-{语义}.{ext}`，例如 `01-cover.jpg` / `03-figma.jpg` / `05-dashboard.png`
  - 页号补零便于排序
  - 语义用英文，短、具体、和内容对应
- **规格建议**：
  - 单张 ≥ 1600px 宽（避免大屏模糊）
  - JPG 用于照片/截图，PNG 用于透明 UI/图表
  - 总大小控制在 10MB 内（影响翻页流畅度）
- **如何替换**：保持**同名覆盖**最稳（HTML 里不用改路径）；如果文件名变了，记得全局搜 `images/旧名` 改成新名
- **没图怎么办**：和用户对齐，可以先用占位色块生成结构，等图片后期补；但要告知 layout 4/5/10 等图文混排页没图就没法验证视觉效果

### Step 2: 选择架构

HTML 演示版永远是源文件，PDF/PPTX/视频都是衍生物。

- 单文件路径：使用 `assets/templates/single-file-magazine.html`。适合 10 页以内、强杂志风、需要横向翻页和 WebGL 背景的演讲。
- 多文件路径：使用 `assets/templates/deck_index.html`。适合 10 页以上、课件、长报告、多 agent 并行制作或需要逐页隔离调试的 deck。
- deck-stage 路径：使用 `assets/templates/deck_stage.js`。适合小型 deck 且需要 web component 外壳或跨页共享状态。

如果用户需要可编辑 PPTX，必须从第一行 HTML 就遵守 `references/editable-pptx.md` 的约束。

### Step 3: 建立视觉系统

批量制作前先定义：

- 字体分工：标题用衬线，正文用非衬线，元数据用等宽。
- 颜色节奏：`hero dark`、`hero light`、`light`、`dark` 交替，不连续 3 页同主题。
- 布局池：一个 deck 最多使用 4-5 种布局。
- 图片规则：图片顶部和左右不能裁切，网格图用固定高度，主视觉用标准比例。
- 页眉页脚：chrome 是栏目元数据，kicker 是本页钩子，不能互相翻译。

Deck 大于等于 5 页时，先做 2 页视觉差异最大的 showcase，确认 grammar 后再批量生成。

### Step 4: 生成内容

优先复用参考文档：

1. `references/architecture.md`: 单文件、多文件、deck-stage 的选择和目录结构。
2. `references/layouts.md`: 杂志风常用布局骨架。
3. `references/components.md`: 字体、数字卡、callout、图片框、图标、动效系统等组件。
4. `references/slide-design.md`: HTML-first deck、密度、节奏、Speaker Notes。
5. `references/themes.md`: 5 套主题色预设（只能选不能自定义）。
6. `references/image-prompts.md`: GPT-M 2.0 配图类型、比例和基础提示词。
7. `references/checklist.md`: 质量检查清单（P0-P3 分级 + 动效自检）。
8. `references/audio.md`: 导出演示视频时的 SFX / BGM 规则。
9. `references/editable-pptx.md`: 可编辑 PPTX 的 HTML 硬约束和导出流程。
10. `references/workflow.md`: 快速工作流参考（补充本文件的详细流程）。

不要发明模板未定义的类名。使用 `layouts.md` 前先确认类名存在于模板 CSS 中。

#### Codex 配图生成（可选）

如果当前运行环境是 **Codex**，完成 deck 初稿后，主动问用户是否需要用 GPT-M 2.0 生成配图并插入 PPT。不要默认生成。

推荐询问方式：

> 要不要为这份 PPT 生成几张配图？可以做成人文纪实照片、杂志风信息图、流程/对比/系统关系图，或把截图再设计成统一的杂志风视觉。

如果用户确认生成，再问他想要哪种图片类型或风格；如果用户没有偏好，根据页面内容自行推荐 1-3 张最值得生成的配图。

生成配图时遵守：

- 提示词保持简短，只框定主题、用途、风格和比例，不要写长篇摄影指导
- 图片风格必须贴合本 skill 的"电子杂志 × 电子墨水"基调
- 信息图、图表、截图再设计里的文字语言必须跟随用户正在使用的语言；中文 deck 用中文，英文 deck 用英文
- 先看 `references/image-prompts.md` 选择图片类型和基础提示词
- 配图比例必须匹配最终落位：主视觉 16:9，左文右图 16:10 / 4:3，信息图 16:9 / 16:10，截图再设计 16:10，图文混排小图 3:2 / 3:4，网格图统一高度裁切
- 生成后的图片放到 `images/` 下，命名遵守 `{页号}-{语义}.{ext}`

### Step 5: 验证和导出

基础验证：

```bash
python3 scripts/verify.py path/to/index.html --viewports 1920x1080,375x667
```

多文件 PDF：

```bash
node scripts/export_deck_pdf.mjs --slides ./slides --out ./deck.pdf
```

单文件 deck-stage PDF：

```bash
node scripts/export_deck_stage_pdf.mjs --html ./index.html --out ./deck.pdf
```

可编辑 PPTX：

```bash
node scripts/export_deck_pptx.mjs --slides ./slides --out ./deck.pptx
```

视频和 GIF：

```bash
node scripts/render-video.js ./index.html --duration=30
bash scripts/convert-formats.sh ./index.mp4 960
```

视频加音频：

```bash
# 使用预设 BGM（tech / tutorial / educational）
bash scripts/add-music.sh ./index.mp4 --mood=tech
# 使用自定义 BGM
bash scripts/add-music.sh ./index.mp4 --music=./my-bgm.mp3
```

## 质量底线

- 不用 emoji，当图标需要用 Lucide 或文字符号。
- 中文大标题不要靠自动换行，长标题手工断行。
- 正文最小 24px；投影场景优先 28-36px。
- 一页只讲一个核心信息，辅助点控制在 3-4 个。
- 图片不要用奇怪原始比例，使用 16:9、16:10、4:3、3:2、1:1。
- 可编辑 PPTX 与复杂视觉效果有冲突时，先说明取舍：PPTX 可编辑优先，还是 PDF 视觉保真优先。

## 核心设计原则（哲学）

> 这些原则是大量实战迭代总结出来的。违反其中任何一条，视觉感都会垮。

1. **克制优于炫技** — WebGL 背景只在 hero 页透出，普通页几乎看不见
2. **结构优于装饰** — 不用阴影、不用浮动卡片、不用 padding box，一切信息靠**大字号 + 字体对比 + 网格留白**
3. **内容层级由字号和字体共同定义** — 最大衬线 = 主标题，中衬线 = 副标，大非衬线 = lead，小非衬线 = body，等宽 = 元数据
4. **图片是第一公民** — 图片只裁底部，保证顶部和左右完整；网格用 `height:Nvh` 固定，不要用 `aspect-ratio` 撑
5. **节奏靠 hero 页** — hero 和 non-hero 交替，才不累眼睛
6. **术语统一** — Skills 就是 Skills，不要中英混合翻译
7. **反 AI 廉价感** — 每个设计决策都要问"这是品牌需要，还是 AI 默认？"（见下方反 AI slop 清单）

## 反 AI Slop 清单

**AI slop = AI 训练语料里最常见的"视觉最大公约数"**。这些东西本身不一定丑，但它们是 AI 默认模式下的产物，不携带任何品牌信息，会让所有 deck 看起来都一样。

### 必须规避的

| 元素 | 为什么是 slop | 替代方案 |
|------|-------------|---------|
| 紫色渐变背景 | AI 万能"科技感"公式 | 从 5 套预设主题选，或用品牌色 |
| Emoji 做图标 | "不够专业就用 emoji 凑" | Lucide 线性图标（模板已引入） |
| 圆角卡片 + 左彩色 border | Material/Tailwind 烂大街组合 | 用 callout 组件（模板已定义） |
| Inter/Roboto 做 display 字体 | 太常见，看不出设计感 | Playfair Display + Noto Serif SC（模板已定义） |
| 每个标题都配装饰性 icon | iconography slop | 只在有语义意义时用 Lucide |
| 编造 stats/quotes 装饰 | data slop | 用真实数据或留白 |
| CSS 剪影代替真实图片 | 任何品牌都长一样 | 用真实图片或诚实 placeholder |

### 正向做法

- ✅ 用模板定义的字体体系（衬线标题 + 非衬线正文 + 等宽元数据）
- ✅ 用模板定义的 5 套主题色，不凭空发明新颜色
- ✅ 图片用标准比例，不裁切顶部和左右
- ✅ 一页只讲一个核心信息，不堆砌
- ✅ 中文标题手工断行，不依赖自动换行
- ✅ 用「」引号不用 ""（中文排印规范）

## 品牌资产协议（涉及具体品牌时）

当 deck 涉及具体品牌（公司、产品、客户）时，不要只从 5 套预设主题里选——先找品牌真实资产。

### 快速流程

1. **问用户**：有没有 logo / 产品图 / 品牌色 / 字体？
2. **搜项目目录**：看有没有已存在的品牌素材
3. **提取色值**：从 logo 或官网 CSS 中提取主色，替换模板的 `--ink` 和 `--paper`
4. **用真实图片**：产品图、UI 截图、品牌素材——不要用 CSS 剪影代替

### 底线

- Logo 必须有——找不到就问用户，不要硬做
- 产品图优先用真实的——AI 生成或 placeholder 是最后手段
- 色值从真实素材提取——不要凭记忆猜

## 设计方向顾问（需求模糊时的 Fallback）

当用户需求模糊（"做个好看的"、"帮我设计"、"不知道要什么风格"）时，不要凭直觉硬做——进入顾问模式：

### 快速流程

1. **理解需求**：问 1-3 个关键问题（受众、场景、情感基调）
2. **推荐 3 个方向**：必须来自不同风格流派，形成明显视觉反差
3. **展示参考**：如果有预制 showcase 就展示，没有就用文字描述视觉特征
4. **用户选择**：选一个深化 / 混合 / 微调 / 重来
5. **锁定方向**：确认后进入主干流程

### 5 大风格流派

| 流派 | 视觉气质 | 适合 |
|------|---------|------|
| 信息建筑派 | 理性、数据驱动、克制 | 科技、研究、数据 |
| 运动诗学派 | 动感、沉浸、技术美学 | 产品发布、demo day |
| 极简主义派 | 秩序、留白、精致 | 高端、艺术、设计 |
| 实验先锋派 | 先锋、生成艺术、视觉冲击 | 创意、独立、前卫 |
| 东方哲学派 | 温润、诗意、思辨 | 文化、人文、非虚构 |

**规则**：3 个方向必须来自 3 个不同流派。不确定时用最轻量版——列出 3 个方向让用户选，不展开不生成。

## 资源导览

```text
ppt-skill/
├── assets/
│   ├── templates/          # 单文件模板、多文件拼接器、deck-stage 外壳
│   ├── motion.min.js       # Motion One 本地副本（离线兜底，约 64KB）
│   └── audio/              # 演示视频可用的 BGM 和 SFX
├── references/
│   ├── architecture.md     # 单文件 vs 多文件 vs deck-stage 架构选择
│   ├── layouts.md          # 10 种页面布局骨架（可直接粘贴，含动效标记）
│   ├── components.md       # 组件手册（字体、色、网格、图标、callout、stat、pipeline、动效）
│   ├── slide-design.md     # HTML-first deck、密度、节奏、Speaker Notes
│   ├── themes.md           # 5 套主题色预设（只能选不能自定义）
│   ├── image-prompts.md    # GPT-M 2.0 配图类型、比例和基础提示词
│   ├── checklist.md        # 质量检查清单（P0-P3 分级 + 动效自检）
│   ├── audio.md            # 导出演示视频时的 SFX / BGM 规则
│   ├── editable-pptx.md    # 可编辑 PPTX 的 HTML 硬约束和导出流程
│   └── workflow.md         # 快速工作流参考
└── scripts/
    ├── verify.py           # Playwright 验证（多视口截图、console 错误检测）
    ├── html2pptx.js        # HTML DOM → PowerPoint 原生对象转换
    ├── render-video.js     # HTML 动画 → MP4 视频（Playwright + ffmpeg）
    ├── export_deck_pdf.mjs # 多文件 slides → 合并 PDF
    ├── export_deck_pptx.mjs    # 多文件 slides → 可编辑 PPTX
    ├── export_deck_stage_pdf.mjs  # 单文件 deck-stage → PDF
    ├── convert-formats.sh  # MP4 → 60fps MP4 + 优化 GIF
    └── add-music.sh        # 混合 BGM 到视频（预设 mood 或自定义音频）
```

**加载顺序建议**：
1. 先读完 `SKILL.md`（这个文件）了解整体
2. Step 1 需求澄清完成后，读 `themes.md` 帮用户选定一套主题色
3. **动手前 Read `assets/templates/single-file-magazine.html` 的 `<style>` 块**——这是类名的唯一来源，缺类会导致整页样式崩
4. 读 `layouts.md` 挑布局（顶部有 Pre-flight 类名清单、主题节奏规划、动效 recipe 决策树）
5. 如果在 Codex 中生成配图，读 `image-prompts.md` 挑图片类型、比例和基础提示词
6. 细节调整时读 `components.md` 查组件（含 Motion 动效系统章节）
7. 如果需要导出可编辑 PPTX，读 `editable-pptx.md` 确认 HTML 硬约束
8. 生成后读 `checklist.md` 自检（P0 强制预检 + 动效自检块）

**动效相关**：模板已把 Motion One 的加载和 5 种 recipe 逻辑全部内嵌到 `single-file-magazine.html` 底部的 module script。你不需要改 JS，只需要按 `layouts.md` 的骨架在 HTML 里加 `data-anim` / `data-animate` 即可。离线演示靠 `assets/motion.min.js`，断网时自动降级为"无动画但内容可读"。
