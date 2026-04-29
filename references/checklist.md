# 质量检查清单

## P0-0: 类名强制预检（动手写 slide 之前必须完成）

在写任何 slide 代码之前：

1. **先 Read `assets/templates/single-file-magazine.html`**（至少读到 `<style>` 块末尾）
2. **对照 `layouts.md` 的 Pre-flight 列表**，确认你要用的每个类都在 `<style>` 里存在
3. 如果某个类缺失：**在 template.html 的 `<style>` 里补上**，不要在每个 slide 里 inline 重写
4. **template.html 是唯一的类名来源**——不要发明新类名，如需自定义用 `style="..."` inline

常见容易遗漏的类（必须预先确认存在）：
`h-hero` / `h-xl` / `h-sub` / `h-md` / `lead` / `kicker` / `meta-row` / `stat-card` / `stat-label` / `stat-nb` / `stat-unit` / `stat-note` / `pipeline-section` / `pipeline-label` / `pipeline` / `step` / `step-nb` / `step-title` / `step-desc` / `grid-2-7-5` / `grid-2-6-6` / `grid-2-8-4` / `grid-3-3` / `grid-6` / `grid-3` / `grid-4` / `frame` / `frame-img` / `img-cap` / `callout` / `callout-src` / `chrome` / `foot`

## P0: 交付前必须通过

- 模板类名已校验：`layouts.md` 中使用的类都存在于模板 CSS。
- 每页都明确主题：`hero dark`、`hero light`、`light` 或 `dark`。
- 没有连续 3 页以上同主题。
- 8 页以上 deck 至少有 1 页 `hero dark` 和 1 页 `hero light`。
- 不用 emoji 做图标，使用 Lucide 或文字符号。
- 大标题使用衬线字体，正文使用非衬线字体，元数据使用等宽字体。
- 中文大标题没有一字一行，长标题已手工断行。
- 图片顶部和左右没有被裁切。
- 图片路径是相对路径，例如 `images/03-dashboard.png`。
- `chrome` 和 `kicker` 没有写同一句话或互相翻译。

## P1: 排版节奏

- 一页只有一个核心信息。
- 正文最小 24px，投影页优先 28-36px。
- 数据页、图片页、引用页、正文页有节奏轮换。
- 一个 deck 不超过 4-5 种布局。
- 页码格式统一，例如 `05 / 18`。
- 英文术语和中文术语全篇统一。

## P2: 图片和视觉

- 图片使用标准比例：16:9、16:10、4:3、3:2、1:1。
- 图片网格使用固定高度，不用奇怪的原图 `aspect-ratio`。
- 不给图片加厚边框或强阴影。
- hero 页 WebGL 或背景视觉不影响文字可读性。
- light 页面没有被深色背景蒙灰。

## P3: 导出和验证

- HTML 已用浏览器打开检查。
- 已运行 `scripts/verify.py` 并检查 console / page errors。
- 如果导出 PDF，已打开 PDF 检查页数和文字。
- 如果导出 PPTX，已确认文字可双击编辑。
- 如果导出视频，已检查开头无黑屏、结尾不突兀。
- 如果加音频，SFX 和视觉 beat 对齐，BGM 不盖住 SFX。

## 动效自检（使用 Motion One 动效时必须检查）

- 每个需要入场动画的元素都已加 `data-anim` 属性。
- hero 页不加 `data-animate`（自动用 `hero` recipe）。
- 大引用页用 `data-animate="quote"`，每句用 `data-anim="line"`。
- 左右对比页用 `data-animate="directional"`，左列 `data-anim="left"`、右列 `data-anim="right"`。
- 流水线页用 `data-animate="pipeline"`，每步 `data-anim="step"`。
- `data-anim` 只加在叶子元素上，不加在容器（`.grid-6` / `.frame`）上。
- `assets/motion.min.js` 文件存在（离线兜底）。
- 浏览器控制台无 motion 相关报错。
