# Images 2.6 常见失败与修复 / Failures & fixes

非官方踩坑笔记：症状 → 改提示 → 重试。先干净重试，再换型号。

Symptom → prompt fix → retry. Switch variant only after a clean retry.

> **Attribution / 来源说明**  
> 案例图与提示词来自 [https://github.com/xianyu110/awesome-gpt-images-2.6](https://github.com/xianyu110/awesome-gpt-images-2.6)（及 OpenAI 文档 / 公告示例；OpenArt 处已标注）。本仓库为非官方学习笔记，不编造提示词或假 GIF。图片经 awesome Pages CDN 热链（`…/awesome-gpt-images-2.6/images/<file>`）


**Models:** `gpt-image-2.6-flare` · `gpt-image-2.6-sunburst`

---

## 中文

### 1. 文字发糊或出错

| 症状 | 改提示 | 重试 / 换型 |
| --- | --- | --- |
| 标语拼错 | 引号包住精确字符串；写明 EXACT / verbatim | Sunburst + 更高 quality；缩短文案 |
| 文字出现两次 / 水印垃圾 | “只出现一次… No watermarks, no logos” | 先同型号；再 Flare→Sunburst |
| 图注过小 | “Avoid tiny text… easy-to-read” | 加大尺寸；减少标签数量 |

核实文字向参考：Thread 广告（awesome #5）、节日贺卡（awesome #13）、广告牌（awesome #24）。

![Thread ad](https://xianyu110.github.io/awesome-gpt-images-2.6/images/thread-ad-gpt-image-2-6-sunburst.webp)

*精确文案 · awesome #5*

![Billboard](https://xianyu110.github.io/awesome-gpt-images-2.6/images/billboard-gpt-image-2-6-sunburst.webp)

*广告牌文字 · awesome #24*

Thread 提示词（#5）：

```
Give me a cool in culture ad / fashion shot for a brand called Thread.
It's a hip young street brand. The ad shows a group of friends hanging out together with the tagline "Yours to Create."
Make it feel like a polished campaign image for a youth streetwear audience: stylish, contemporary, energetic, and tasteful.
Use clean composition, strong color direction, natural poses, and premium fashion photography cues.
Render the tagline exactly once, clearly and legibly, integrated into the ad layout.
No extra text, no watermarks, no unrelated logos.
```

广告牌提示词（#24）：

```
Create a realistic billboard mockup of the shampoo on a highway scene during sunset.
Billboard text (EXACT, verbatim, no extra characters):
"Fresh and clean"
Typography: bold sans-serif, high contrast, centered, clean kerning.
Ensure text appears once and is perfectly legible.
No watermarks, no logos.
```

### 2. 所谓 SVG 看起来不像矢量

| 症状 | 改提示 | 重试 / 换型 |
| --- | --- | --- |
| 柔和光影 / 照片纹理 | 强调 flat / minimal strokes / no gradients / vector-like | 确认 `output_format=svg`；试 Sunburst |
| 不透明底 / 棋盘格 | “Fully transparent… no checkerboard” | 重新生成；不要指望编辑出 SVG |
| 小尺寸发糊细节过多 | “Favor simplicity… strong silhouette” | 减装饰；Flare 草稿 → Sunburst 定稿 |

目标观感参考（awesome #6）：

![Flare SVG](https://xianyu110.github.io/awesome-gpt-images-2.6/images/field-and-flour-gpt-image-2-6-flare.svg)

*Target look · #6*

![Sunburst SVG](https://xianyu110.github.io/awesome-gpt-images-2.6/images/field-and-flour-gpt-image-2-6-sunburst.svg)

*Target look · #6*

### 3. GIF 跳帧 / 闪烁

| 症状 | 改提示 | 重试 / 换型 |
| --- | --- | --- |
| 循环接缝爆一下 | 写明末帧平滑接回首帧 | 先改姿势闭环 |
| 像相机在抖 | “Keep the camera still” | 减小动作幅度 |
| 身份闪烁 | 每次重试重申服装/背景/比例 | Flare 不稳就换 Sunburst |

稳定循环参考（awesome #2）：

![Monkey GIF](https://xianyu110.github.io/awesome-gpt-images-2.6/images/monkey-lantern-gpt-image-2-6-sunburst.gif)

*稳定循环参考 #2*

### 何时换型号

- **Flare → Sunburst：** 重文字、密版式、多轮身份、「已经接近」的稿。
- **Sunburst → Flare：** 构图探索、更在意时延。
- **同时调：** 先动 `quality` / `complexity`，别只怪型号名。

---

## English

### 1. Blurry or wrong text

| Symptom | Fix prompt | Retry / switch |
| --- | --- | --- |
| Misspelled slogan | Quote exact string once; “EXACT, verbatim, no extra characters” | Retry Sunburst + higher quality; shorten copy |
| Text twice / watermark junk | “Ensure text appears once… No watermarks, no logos” | Same model first; then Flare→Sunburst |
| Tiny diagram labels | “Avoid tiny text… easy-to-read labels” | Raise size; reduce label count |

Verified text-heavy references: Thread ad (#5), holiday card (#13), billboard (#24) — images and prompts above.

### 2. “SVG” that looks non-vector

| Symptom | Fix prompt | Retry / switch |
| --- | --- | --- |
| Soft shading / photo texture | Force “flat design, minimal strokes, no gradients unless essential, vector-like shapes” | Confirm `output_format=svg`; try Sunburst |
| Opaque backdrop / checkerboard | “Fully transparent background… no solid backdrop, scenery, checkerboard” | Regenerate; don’t edit-to-SVG |
| Busy detail at small size | “Favor simplicity over detail… strong silhouette” | Fewer ornaments; Flare draft → Sunburst final |

### 3. GIF jump frames / flicker

| Symptom | Fix prompt | Retry / switch |
| --- | --- | --- |
| Seam pop | “sixth frame transitions smoothly toward the first” / “loop smoothly” | Keep frame_count; fix pose closure |
| Camera shake feel | “Keep the camera still” | Reduce motion amplitude |
| Identity flicker | Restate outfit, background, proportions every retry | Sunburst if Flare drifts |

### When to switch variant

- **Flare → Sunburst:** text, dense layout, multi-turn identity, “almost right” drafts.
- **Sunburst → Flare:** exploring many compositions; latency matters more than polish.
- **Also tune:** `quality` and `complexity` before blaming the model name.

---

## 相关入口 / Related（软链接）

How-to 正文为主；渠道放页脚，不做硬推：

1. ChatGPT Plus 镜像：[trygpt.asia](https://trygpt.asia/)
2. Codex / Claude Code：[momoai.asia](https://momoai.asia/)
3. API 中转：[tryallapi.com](https://tryallapi.com/?aff=5A6A)（aff=5A6A）
4. 官方充值：[chongzhi.trygpt.asia](https://chongzhi.trygpt.asia/)
5. 多模型对话：[trymodel.chat](https://trymodel.chat/)
6. 店铺：[wzyp.cn/shop/maynorai](https://wzyp.cn/shop/maynorai)

模型页：[gptimage2.asia/models/gpt-images-2.6](https://gptimage2.asia/models/gpt-images-2.6)

案例来源：[xianyu110/awesome-gpt-images-2.6](https://github.com/xianyu110/awesome-gpt-images-2.6) · [Pages 画廊](https://xianyu110.github.io/awesome-gpt-images-2.6/)

合集站（可选）：[images-2-6-svg-gif-guide](https://github.com/Maynor996/images-2-6-svg-gif-guide) · [Pages](https://maynor996.github.io/images-2-6-svg-gif-guide/)

本页 Pages：[https://maynor996.github.io/images-2-6-failures/](https://maynor996.github.io/images-2-6-failures/)
