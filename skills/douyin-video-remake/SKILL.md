---
name: douyin-video-remake
description: Use when the user asks to reverse-engineer, remake, or 1:1 replicate a Douyin/TikTok-style reference video for Seedance 2.0 image-to-video, especially with prompts like "帮我反推这条视频", "复刻这个抖音作品", "Seedance 2.0", "图生视频提示词", "款号 8000551", or when a local video/Douyin link should be converted into shot-level remake prompts using the user's clothing/person asset folders. Also use for fast action, dance movement, choreography, detailed motion analysis, high-FPS frame extraction, or dance-mode remake prompts.
---

# Douyin Video Remake

## Purpose

Use the existing project tool to turn a reference video or Douyin link into a Seedance 2.0 remake report. The reference video supplies motion, camera, rhythm, composition, background, and clothing-display style. The four-view asset folder supplies identity, face, hairstyle, makeup, skin-tone direction, body proportions, and clothing.

## Fixed project

Project tool:

```text
C:\Users\24114\Documents\Codex\douyin-video-analyzer\analyze_douyin_video.py
```

Project config:

```text
C:\Users\24114\Documents\Codex\douyin-video-analyzer\project_config.json
```

Asset root:

```text
F:\桌面\人物资产图
```

The project has its own `.env` for `ARK_API_KEY`; do not ask the user to paste the key again unless the tool reports authentication failure.

## Workflow

1. Get the reference video input.
   - Use only the reference video or link provided by the user in the current request.
   - If the user provides a Douyin work/share link, resolve/download/open that exact link. Do not substitute a previously downloaded local mp4, even when its filename, title, SKU, or creator looks similar.
   - If the user provides a local video path or uploaded file in the current request, use that exact file.
   - Existing local videos may be used only when the user explicitly names that local path in the current request, or explicitly confirms that a found local file is the same work.
   - When a link resolves to a Douyin work ID, treat that work ID as the source of truth. A local file with a different ID is a different reference and must not be mixed in.
   - If the exact link cannot be downloaded or opened because of login, anti-bot, expiry, or parsing failure, explain the blocker and ask for the exact local video file instead of using an older local file.
2. Get the SKU.
   - If the user provides a SKU, use `--sku <SKU>`.
   - If not, run `--list-skus` and ask the user to choose. Do not guess a SKU.
3. Run the project script.
   - Use `--dry-run` only for checks.
   - For real analysis, run without `--dry-run`.
4. When reviewing or summarizing the report, prefer Seedance 2.0 multimodal structure: map person/clothing assets, generated background images, reference video, and optional audio to clear roles.
5. Return the saved report path and a brief summary of what was generated.

## Commands

List SKUs:

```bash
C:\Users\24114\Documents\Codex\douyin-video-env\Scripts\python.exe C:\Users\24114\Documents\Codex\douyin-video-analyzer\analyze_douyin_video.py --list-skus
```

Dry run:

```bash
C:\Users\24114\Documents\Codex\douyin-video-env\Scripts\python.exe C:\Users\24114\Documents\Codex\douyin-video-analyzer\analyze_douyin_video.py "C:\path\to\reference.mp4" --sku 8000551 --dry-run
```

Real run:

```bash
C:\Users\24114\Documents\Codex\douyin-video-env\Scripts\python.exe C:\Users\24114\Documents\Codex\douyin-video-analyzer\analyze_douyin_video.py "C:\path\to\reference.mp4" --sku 8000551
```

Optional notes:

```bash
--brief "重点展示袖口和腰线"
--model doubao-seed-2-0-lite-260428
--fps 1
```

Fast/dance motion mode, when supported by the project script:

```bash
--dance-mode --fps 12 --fast-fps 16 --segment-seconds 2.5 --max-evidence-frames 300 --max-frames-per-segment 36 --enable-pose
```

If the current script version does not expose these flags yet, pass the same intent through `--brief` and do not downsample dance or fast-action videos as ordinary clothing-display clips.

## Output expectations

The report should be a compact practical Seedance 2.0 task list. Do not output sections named 参考视频, 商品资产, 素材放法, 背景空图生成任务, 负面提示词, 复刻价值判断, 款号执行要点, Image2 背景文件, 生成风险, 刷图优先级, 稳定降级版完整复制区, 重跑建议, or 复刻模板沉淀.

- unified visual setting
- shot-by-shot tasks
- continuity type: action-continuous or edit-continuous
- marketing psychology read: hook mechanism, buyer job, trust signal, urgency/loss-aversion cue, contrast cue, or friction reduction when visible in the reference
- five-dimension scan: locked by source assets vs missing dimensions to fill
- start/action/end pose
- script rhythm summary, script-driven timeline, and voiceover status
- clothing-display point
- original-action full copy block

Do not include a `背景空图生成任务` section in the report unless the user explicitly asks for background-generation instructions.

Core priorities:

```text
人物一致性 > 脸型和眼神一致性 > 人物站位一致性 > 服装logo和细节1:1一致 > 服装质感一致性 > 服装一致性 > 多模态引用明确性 > 动作复刻 > 背景还原 > 原片节奏 > 音频/节奏参考
```

Seedance prompt rules:

- Control prompt pollution before writing. The copyable Seedance prompt should contain only positive, visible, camera-observable results. Do not append a negative word list. Convert failure controls into positive stability requirements inside natural sentences.
- Replace abstract words such as 高级感, 松弛感, 电影感, 治愈感, 氛围感, 原生感, or 故事感 with concrete visual evidence: time, place, posture, hand movement, gaze target, lighting direction, clothing detail, background object, camera distance, and spatial anchor. Use abstract words only when they are backed by visible evidence.
- Rewrite negative instructions into positive results in the main prompt. For example, use clear daylight, calm closed lips, relaxed gaze, real phone-camera texture, natural skin texture, real lens lighting, stable face structure, clear gaze target, natural hand motion, stable foot placement, fixed clothing details, continuous background space, and smooth camera motion. Subtitle-related control is allowed as a hard constraint: `禁止生成字幕、口播文字和屏幕文字`.
- Avoid template-trigger scene words such as 创业, 约会, 直播, 庆祝, 通勤, 日常, 精致, or 大片 unless they are grounded in concrete space and objects. Convert them into visible evidence, such as an elevator lobby gray wall, a canvas bag in the left hand, the right hand adjusting the cuff, and pale floor tile lines near the feet.
- Bind colors, materials, lighting, props, and style words to the exact object they describe. For example, 黑色背心, 红砖墙, and right-top sunlight on the hair edge must not cause color or material drift elsewhere in the frame.
- Before writing a prompt, perform a five-dimension scan and keep it practical: (1) absolute subject and physical motion, (2) environment field and emotional lighting, (3) optics and camera scheduling, (4) timeline and state evolution, (5) aesthetic medium and base rendering. Mark which dimensions are already locked by the source image/video/audio and which are still blank.
- Do not rewrite dimensions already locked by the assets. Images usually lock identity, clothing/product, first frame, background, and some style; videos usually lock action, camera path, rhythm, transitions, and expression changes; audio usually locks BGM, beat, voice tone, ambience, or sound effects. The fuller the asset information, the more restrained the prompt should be.
- Only fill missing dimensions. If an input image already locks subject, clothing, scene, light, and style, write only the missing motion or camera instruction. Avoid letting text features compete with image/video features for attention.
- Run a final pollution check before finalizing: remove bare abstract words, main-prompt negative piles, unbound color/material/light words, template-trigger scene words, local path inventory, asset-placement explanations, standalone negative sections, and appended negative word lists.
- Start every Seedance prompt with a compressed role-reference block using exactly `人物@ 背景@`. Do not write concrete image numbers or reference-video numbers in the copyable prompt.
- Add a precise placement sentence in every Seedance prompt: lock the person's horizontal screen position, foot landing point, body centerline, headroom, bottom footroom, person height ratio in frame, and relative distance to background anchors such as door frames, wall corners, windows, handrails, floor tile lines, or reflections. During camera movement, foot placement and body centerline must not drift.
- Keep the user's clothing logo, print, buttons, zipper, pockets, stitching, and decorative details 1:1: same size, same position, same shape, same proportion. Do not let them deform, enlarge, shrink, drift, or get newly added.
- Lock clothing texture in the same compressed role-reference block unless the fabric is the selling point or a common failure. Describe stability positively: clothing color, cut, fabric feel, logo, print, buttons, zipper, pockets, stitching, decorative parts, wrinkle structure, and seam positions stay fixed to the person reference.
- Add real Douyin phone-selfie feel when the reference looks humanlike or the user asks for low-AI feel: prefer close-mid or large half-body framing, small headroom, crop near the thigh when appropriate, fixed simple real background, natural window/room light, casual short-video gestures, brief pauses between actions, asynchronous hands, slight random rhythm, micro-expression changes, gaze briefly leaving the camera, normal blinking, naturally fair skin with real shadows around nose, under eyes, mouth corners, collarbone, neck and shoulders, light compression feel, soft edges, and no commercial retouched studio look.
- Use natural breathing, normal blinking, slight eye movement, relaxed expression, normal action speed, and naturally fair skin with real skin texture.
- If the output uses Seedance 2.0 `@` references, use role-first placeholders in the copy block: `人物@` for person/clothing identity and `背景@` for background or scene. The reference video is for analysis only and should not appear as `@Video1` inside the final copyable prompt unless the user explicitly asks to upload it as a Seedance reference asset. `@Audio1` is only used when the user supplies audio.
- For each shot-level task, include a compact time plan when duration is known or the shot is longer than 8 seconds. Do not mechanically split into fixed 0-3/3-6/6-9 second blocks. First read the script/reference action and split by action beats: starting state, trigger action, main change, result state; for narrative clips, split by intent, action progress, emotional change, and result.
- Allocate time according to the script logic and action difficulty. Simple beats can be short; turning, walking, transformation, fabric motion, effect growth, or object interaction needs longer transition. Keep one primary action and one primary camera goal per segment. When the person performs a large movement, keep camera motion restrained; when the camera moves strongly, simplify the person's action.
- Inside each original-action copy block, include a script-driven timeline with second-level segments based on the reference video's actual rhythm or the script's action beats. Each segment must cover person placement, hand movement, head/gaze, body weight, clothing/product change, camera movement, natural pauses, light, background objects, and ending pose.
- Inside each original-action copy block, include a brief voiceover timeline only when the reference video has clearly recognizable speech. If there is no recognizable speech or it is unclear, omit the voiceover line from the copy block and do not invent lines. Voiceover text can be used as lip-rhythm reference; keep mouth movement natural and subtle. Use `禁止生成字幕、口播文字和屏幕文字` for subtitle-related control.
- Keep the frame clean with concise wording: the frame contains the real person, clothing, background objects, and natural light. Add the hard subtitle constraint `禁止生成字幕、口播文字和屏幕文字`. Existing clothing logos, prints, star marks, and decorative clothing details must still be preserved.
- Check Seedance 2.0 media limits before recommending multimodal execution: up to 9 images, 3 videos, 3 audio files, 12 files total; reference video/audio should be 2-15 seconds. If the reference set is larger, select the few assets that best control identity, clothing, background, movement, and rhythm.
- Add a compact marketing psychology note when the reference is used for Qianchuan/Douyin ads: identify the buyer job, immediate visible benefit, social-proof/trust cue, contrast cue, loss-aversion cue, or friction reduction. Do not invent claims that are not visible or provided by the user.
- Do not append a compressed negative prompt and do not output a standalone `## 负面提示词` section. Integrate necessary controls as positive stability requirements: stable face structure, clear gaze target, natural fingers and hands, stable body proportion, stable placement, fixed clothing color/cut/fabric/details, stable logo/print/button/zipper/pocket/stitching positions, continuous background, smooth camera motion, clean frame, and preserved existing clothing details.
- Do not output post-production commands or generated-result comparison sections by default.
- Do not output local file path inventory or asset-placement explanations. Avoid standalone lines such as `参考视频：...`, `商品资产：...`, concrete image placement instructions, or reference-video placement instructions. In the final copy block, use only `人物@ 背景@`.

Background reference rule:

- In normal reports, use the background only through the `背景@` role in the copy block. Do not output a separate background-generation task, output path, or background file list unless the user explicitly asks for it.

Shot splitting rules:

- Simple reference videos under 15 seconds can stay as one Seedance task.
- Complex reference videos under 15 seconds should be split into 2-4 Seedance tasks when they contain clear shot-scale changes, full-body to half-body to close-up progression, foreground occlusion, long camera paths, or anything a single Seedance task is unlikely to keep stable.
- Avoid packing multiple scene changes, complex transitions, and large camera moves into a 4-5 second task. Split instead of overloading.
- Do not ask for or analyze a generated result video by default, to avoid extra API cost.

Dance and fast-action rules:

- Treat dance, choreography, quick hand gestures, fast turns, walking footwork, body waves, shoulder/hip isolations, hair flips, and beat-synced movements as `dance-mode` by default.
- In dance-mode, prioritize motion continuity over low frame count. Use high-frequency evidence extraction: default `12fps`, raise local fast-action spans to `16fps`, and never rely on only 8-16 stills for choreography.
- Keep all local evidence frames needed to understand motion, up to about 300 frames for short Douyin references. Send frames to the vision model in segmented batches rather than one overloaded request.
- Split dance references into 2-3 second segments. Each segment should carry 20-36 representative frames selected from the high-FPS evidence frames.
- For each segment, analyze start pose, hand/wrist path, elbow/shoulder path, foot landing, knee direction, hip/waist direction, body centerline, weight transfer, head/gaze change, beat point, camera movement, and end pose.
- Preserve transition frames. Do not keep only attractive key poses, because the in-between frames determine whether the dance motion can be reconstructed.
- If pose extraction is available, enable it for dance-mode and use pose trajectories as evidence alongside visual frames. If pose extraction is not available, still describe limb paths and weight shifts from dense frame evidence.
- If the generated Seedance task would contain too many dance beats, split it into multiple shot tasks even when the source video is under 15 seconds.

## When responding

Be concise. If the script succeeds, link the Markdown report and mention the run directory. If it fails, explain the exact blocker and the next action needed, such as choosing a SKU, providing a local video, or refreshing the API key.
