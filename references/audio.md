# 演示音频

音频只用于导出演示视频或需要声音反馈的 HTML demo。普通演讲 PPT 默认不加音频，避免现场播放不可控。

## 资产位置

```text
assets/audio/
├── bgm/
│   ├── bgm-tech.mp3
│   ├── bgm-tutorial.mp3
│   └── bgm-educational.mp3
└── sfx/
    ├── keyboard/
    ├── ui/
    ├── transition/
    ├── container/
    ├── feedback/
    ├── progress/
    ├── impact/
    └── terminal/
```

## 双轨原则

演示视频音频分两层：

- SFX：标记视觉 beat，例如翻页、点击、聚焦、打字、logo reveal。
- BGM：情绪底，不抢 SFX。

推荐参数：

- BGM 音量：0.40-0.50。
- SFX 音量：0.80-1.00。
- `amix normalize=0`。
- BGM fade-in 0.3s，fade-out 1.5s。

## BGM 选择

- 产品发布 / 技术演示：`bgm-tech.mp3`。
- 教程讲解 / 工具使用：`bgm-tutorial.mp3`。
- 教育学习 / 原理解释：`bgm-educational.mp3`。
- 10 秒以内短片可以不加 BGM，只保留关键 SFX。

## SFX 快速索引

- 打字输入：`keyboard/type.mp3`、`keyboard/type-fast.mp3`、`keyboard/enter.mp3`、`keyboard/space-tap.mp3`、`keyboard/delete-key.mp3`。
- 翻页和切换：`transition/swipe-horizontal.mp3`、`transition/whoosh-fast.mp3`、`transition/whoosh.mp3`、`transition/dissolve.mp3`、`transition/slide-in.mp3`。
- 点击和聚焦：`ui/click.mp3`、`ui/click-soft.mp3`、`ui/focus.mp3`、`ui/hover-subtle.mp3`、`ui/tap-finger.mp3`、`ui/toggle-on.mp3`。
- 卡片和容器：`container/card-snap.mp3`、`container/card-flip.mp3`、`container/modal-open.mp3`、`container/stack-collapse.mp3`。
- 完成反馈：`feedback/success-chime.mp3`、`feedback/achievement.mp3`、`feedback/error-tone.mp3`、`feedback/notification-pop.mp3`。
- 进度：`progress/complete-done.mp3`、`progress/loading-tick.mp3`、`progress/generate-start.mp3`。
- 品牌落点：`impact/logo-reveal.mp3`、`impact/logo-reveal-v2.mp3`、`impact/brand-stamp.mp3`、`impact/drop-thud.mp3`。
- 终端演示：`terminal/command-execute.mp3`、`terminal/output-appear.mp3`、`terminal/cursor-blink.mp3`。

## 合成模板

### 快捷方式（推荐）

使用 `scripts/add-music.sh` 自动混合 BGM：

```bash
# 使用预设 mood（tech / tutorial / educational）
bash scripts/add-music.sh ./video.mp4 --mood=tech
# 使用自定义 BGM 文件
bash scripts/add-music.sh ./video.mp4 --music=./my-bgm.mp3
```

脚本会自动：裁剪 BGM 到视频时长、0.3s fade-in、1.0s fade-out、输出到 `./video-scored.mp4`。

### 手动 ffmpeg

视频 + SFX + BGM：

```bash
ffmpeg -y -i video.mp4 -i sfx-track.mp3 -i assets/audio/bgm/bgm-tech.mp3 \
  -filter_complex "\
[2:a]atrim=0:25,afade=in:st=0:d=0.3,afade=out:st=23.5:d=1.5,lowpass=f=4000,volume=0.45[bgm];\
[1:a]highpass=f=800,volume=1.0[sfx];\
[bgm][sfx]amix=inputs=2:duration=first:normalize=0[a]" \
  -map 0:v -map "[a]" -c:v copy -c:a aac -b:a 192k final.mp4
```

## 检查清单

- SFX 是否只打关键 beat，没有铺满每个动画？
- BGM 是否比 SFX 低约 6-8 dB？
- Logo reveal 前后是否留出 0.2s 空隙？
- 关闭 BGM 单听 SFX 是否仍有节奏？
- 关闭 SFX 单听 BGM 是否不突兀？
