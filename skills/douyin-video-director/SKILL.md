---
name: douyin-video-director
description: 抖音/千川/Seedance 视频创意工作流总入口。Use when the user asks for Douyin/TikTok video reverse-engineering, Seedance prompts, image-to-video prompts, fashion/product ad videos, video creative strategy, reference-video remake, or executing image-to-video generation. Routes to douyin-video-remake, seedance-prompt, seedance2-skill, image-to-video, and ad-creative as needed.
---

# Douyin Video Director

## Purpose

Act as the lightweight director for Douyin, Qianchuan, Seedance, and short-form ad video work. Do not replace specialist skills. Decide which specialist skill should handle the task, combine them when useful, and keep the workflow clear.

## Routing

Use this decision table:

| User intent | Primary skill | Notes |
|---|---|---|
| 反推视频、复刻抖音作品、1:1 拆镜头 | `douyin-video-remake` | Needs local video, direct URL, or downloadable Douyin link. If SKU/clothing assets matter, get or list SKU. |
| 女装商品图、千川素材、低 AI 感图生视频提示词 | `seedance-prompt` | Best for clothing identity, fabric, fit, face/eye consistency, natural phone-shot feel, and ad copy. |
| 通用 Seedance 2.0、多模态 `@Image/@Video/@Audio`、短剧、MV、教育、特效、视频延展 | `seedance2-skill` | Best for camera language, reference roles, audio, timed beats, effects, and non-fashion scenarios. |
| 直接生成/执行图生视频、RunComfy、HappyHorse、Wan、Seedance 2.0 Pro | `image-to-video` | Use when the user wants an actual generation run, not just a prompt. |
| 投放创意、广告角度、批量素材方向、文案 Hook | `ad-creative` | Combine with `seedance-prompt` for Qianchuan fashion ads. |
| 用户心理、购买动机、钩子强度、卖点顺序、转化阻力 | `marketing-psychology` | Use before writing hooks or ad copy when the user asks why a creative works, why people buy, or how to improve conversion. |

## Common Workflows

### Reference Video to Seedance Prompt

1. Use only the reference video or link provided by the user in the current request. If the user provides a Douyin link, route that exact link to `douyin-video-remake`; do not substitute a previously downloaded local mp4 based on SKU, title, creator, or similar filename. Existing local videos may be used only when the user explicitly provides that local path or confirms the found file is the same work.
2. Use `douyin-video-remake` to analyze the reference video and create shot-level remake prompts.
3. If the output prompt targets women's clothing or Qianchuan, apply `seedance-prompt` rules for identity, fabric, fit, natural motion, and low-AI feel.
4. If the user provides multiple images/videos/audio, apply `seedance2-skill` role mapping so every `@Image`, `@Video`, and `@Audio` reference has a clear job.

### Product Image to Douyin Ad Video

1. Use `ad-creative` to define the angle, hook, and testing direction if the user asks for creative strategy or multiple versions.
2. Use `marketing-psychology` to choose the persuasion mechanism when conversion matters: social proof, loss aversion, immediate benefit, scarcity, contrast, authority, or reduced regret.
3. Use `seedance-prompt` for the final Seedance image-to-video prompt.
4. Use `image-to-video` only if the user wants to execute generation.

### General Seedance 2.0 Video

1. Use `seedance2-skill` for multimodal structure, camera movement, timing, audio, and style.
2. Before writing prompts, scan which dimensions are already locked by assets and which are blank; only fill the blank dimensions.
3. For complex action, split timing by script/action beats instead of fixed 0-3/3-6/6-9 blocks.
4. If the scene becomes a Douyin clothing/product ad, layer in `seedance-prompt` constraints.
5. If execution is requested, pass the final prompt and assets to `image-to-video`.

## Default Priorities

For Douyin/Qianchuan clothing videos:

```text
人物一致性 > 眼神和脸型一致性 > 人物站位 > 服装logo和细节 > 服装质感 > 真实手机拍摄感 > 动作自然 > 多模态引用明确 > 原片节奏 > 用户心理/广告钩子
```

For general Seedance videos:

```text
素材职责明确 > 五维扫描与素材锁定判断 > 主体/场景清晰 > 剧本驱动时间轴 > 动作可执行 > 镜头不冲突 > 音频/节奏明确 > 风格统一
```

## Multimodal Rules

When the user provides multiple assets:

- Images should lock stable things: person, product, clothing, brand, first frame, last frame, background, or detail.
- Videos should control dynamic things: action, camera path, rhythm, transitions, effects, expressions, or ambient sound.
- Audio should control BGM, beat, voice tone, dialogue style, sound effects, or ambience.
- Never write only "参考 @Video1". Specify exactly what to reference and what not to change.
- Keep media limits in mind: up to 9 images, 3 videos, 3 audio files, 12 files total; reference video/audio should usually be 2-15 seconds.

## Marketing Psychology Layer

When the task is for Douyin/Qianchuan conversion, add a small psychology pass after the visual prompt is stable:

- **JTBD**: name the buyer's real job, such as looking slimmer, saving outfit time, looking polished at work, or reducing styling risk.
- **Immediate benefit**: prefer benefits visible in the first 1-3 seconds.
- **Social proof**: use only if there is real evidence, such as reviews, sales, repeat buyers, or creator-style demonstration.
- **Loss aversion / regret reduction**: frame avoidable pain gently, such as "不显拖沓", "不用担心压身高", "通勤不容易出错".
- **Contrast**: show before/after, loose/tidy, ordinary/polished, static/detail movement when the visual material supports it.
- **Friction check**: keep one primary action, one primary CTA, and one core selling point per short clip.

## Response Style

Be practical and route quickly. If the user asks for execution, do the work. If the task needs a missing video, SKU, product image, or asset role, ask only the minimum question needed. Prefer one clean workflow over listing every possible option.
