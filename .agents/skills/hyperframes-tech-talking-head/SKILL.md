---
name: hyperframes-tech-talking-head
description: Package an existing Chinese talking-head video into a high-end 9:16 mobile technology or AI tutorial with HyperFrames. Use for 科技感口播包装、抖音 AI 教学视频、YouTube 科技开场、截图/B-roll 与口播对齐、屏幕大字、信息卡、callout、分屏、证据特写、流程图、丰富但干净的动效，或继续编辑同类 HyperFrames 工程。Preserve the source speech and burned-in subtitles, optimize screenshots and typography for phone viewing, allow intentional short face coverage, default to no background music, use only sparse timeline-aligned SFX, and stop at Studio preview until render approval.
---

# HyperFrames Tech Talking Head

Turn an existing talking-head clip into a dense, modern technology lesson without making it look like a generic effects template. Treat this skill as a preference and decision layer on top of the installed HyperFrames workflows.

## Load The Base Contracts

1. Read `/hyperframes` first and follow its existing-project or fresh-project branch.
2. For a fresh talking-head package, use `/talking-head-recut`; use `/general-video` only when the source footage itself must be re-edited or remixed.
3. Read `/hyperframes-core` before changing composition HTML, `/hyperframes-keyframes` for seek-safe animation, `/hyperframes-cli` before checks or preview, and `/media-use` before adding media or SFX.
4. This skill's defaults never override an explicit user instruction or an existing confirmed `BRIEF.md` value.

Before designing visuals, read [references/style-system.md](references/style-system.md). Before drafting or revising the timeline, read [references/timeline-playbook.md](references/timeline-playbook.md).

## Defaults

- Canvas: `1080x1920`; preserve source fps, with `60fps` preferred when the source is 60fps.
- Source: keep the original video, speech, and burned-in subtitles clear.
- Captions: do not add a second full subtitle track. Add only keywords, short labels, titles, and callouts.
- Audio: no BGM. Use sparse SFX only when each cue lands on a visible action; keep SFX well under speech.
- Composition: face visibility is not a hard constraint. Short, intentional takeovers may cover it; the detected burned-subtitle band remains a hard safe zone.
- Style: graphite black, cool white, electric blue, cyan, and a small acid-yellow accent; editorial evidence layout rather than decorative HUD chrome.
- Review: build and check the Studio preview first. Never render the final MP4 without explicit approval.

## Workflow

### 1. Resume Or Set Up

- Existing project: read `BRIEF.md`, transcript files, storyboard, media ledger, and current `index.html`; preserve unrelated timing and assets.
- Fresh project: create an independent HyperFrames project. Probe the source with FFprobe and create a browser-friendly H.264 proxy when needed; preserve source duration, fps, speech, and burned subtitles.
- Run the project's pinned-CLI upgrade probe before the first render-affecting command.

### 2. Build The Speech Timeline

- Reuse a trustworthy word/segment transcript when present.
- Otherwise transcribe locally. Prefer the configured CUDA Whisper Chinese `large-v3`; fall back only when it is genuinely unavailable.
- Correct product names and technical terms without changing timestamps.
- Produce semantic beats with exact `start`, `end`, spoken idea, emphasis keywords, and candidate visual treatment.
- Do not invent uncertain spoken content. State uncertainty and request the missing source when the audio cannot establish it.

### 3. Map Assets To Speech

- Inventory screenshots, screen recordings, diagrams, logos, and user reference images.
- Attach each asset only to the line that explains it. Do not front-load later screenshots just to add variety.
- For desktop screenshots on a phone canvas, use the sequence `whole context -> 2.5-3x detail takeover -> 44-58px plain-language callout`.
- Let the screenshot or diagram briefly own the canvas when it carries more information than the face.
- Record source, usage interval, derivative crops, and license/ownership in the media ledger.

### 4. Design The First 15-20 Seconds

- Put the strongest claim first, not setup or process.
- Change composition at least twice: kinetic hook, proof or tool pairing, then the first actionable step.
- Use large keyword typography and one strong evidence image. Do not stack every available effect.
- End on a complete spoken phrase and a cut that can continue into the full tutorial.

### 5. Extend The Full Video

- Give every spoken concept one primary visual job: explain, prove, compare, warn, demonstrate, or summarize.
- Change treatment every `4-8s` when information density is high; use a full or near-full takeover every `10-18s` when a real asset supports it.
- Vary among kinetic titles, split evidence, screenshot closeups, parameter demos, timelines, checklists, code/build pipelines, revision before/after states, and process flows.
- Keep micro-motion alive inside longer holds, but never add motion that does not improve comprehension.
- Use at most a few natural transition families. Avoid repeated whooshes, glitch flashes, particles, cheap HUD frames, and decorative 3D unless explicitly requested.

### 6. Implement Deterministically

- Keep media as direct children of the composition root; keep the visual video muted and mount source audio separately.
- Register exactly one paused, synchronously built master timeline.
- Use seek-safe GSAP transforms, opacity, masks, and finite repeats. Never call media `play()` or use render-time randomness.
- Keep local media frozen in the project. Do not rely on network requests during preview or render.
- Leave BGM absent by default. If the user explicitly requests music later, treat it as a separate approval and update `BRIEF.md` plus the media ledger.

### 7. Verify And Hand Off

- Run `hyperframes check` through the project's wrapper after edits.
- Sample the hook, every chapter boundary, every screenshot takeover, every SFX cue, and the closing thesis.
- Inspect at phone scale: burned subtitles readable, screenshot text replaced by legible callouts, no accidental overlap, no blank media, no white flash, no audio desync.
- Confirm source speech remains the dominant audio; SFX should be short and normally peak at least `12dB` below speech peaks.
- Keep `render_approved: false`, open or reuse Studio preview, and ask for revise-or-render approval.

## Invocation Examples

```text
$hyperframes-tech-talking-head 把这条带字幕的口播视频做成 9:16 高级 AI 教学视频，先做前 20 秒。
$hyperframes-tech-talking-head 继续在现有 HyperFrames 工程上做完整视频，截图跟口播走，不加音乐。
$hyperframes-tech-talking-head 把截图放大到手机能看清，允许短暂遮脸，但不要挡原字幕。
```
