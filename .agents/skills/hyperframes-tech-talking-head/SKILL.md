---
name: hyperframes-tech-talking-head
description: Package or revise an existing talking-head video with HyperFrames in a user-selected aspect ratio, platform format, visual style, pacing, media treatment, subtitle policy, and audio plan. Use for 口播视频包装、科技/知识/杂志/极简等风格、抖音/小红书/YouTube 比例、截图或 B-roll 随口播、信息卡、callout、分屏、流程图和动效增强。Always begin each new invocation with a requirements interview and an explicit Requirements Receipt confirmation; never inspect media, generate a plan, edit a project, or start rendering on the first response. Preserve confirmed requirements through Studio review and require separate final-render approval.
---

# HyperFrames Talking-Head Packaging

Customize an existing talking-head clip only after its requirements are explicit. Treat this skill as an intake and decision layer on top of the installed HyperFrames workflows.

## Hard Intake Gate

Apply this gate on every new invocation of the skill. Do not repeat it after a Requirements Receipt has already been confirmed in the same task.

1. Make the first response questions only. Do not call tools, inspect files, transcribe media, propose a finished timeline, create assets, edit a project, start Studio, or render.
2. Read [references/requirements-intake.md](references/requirements-intake.md) and ask only unanswered fields, grouped into at most six concise questions.
3. If the user's initial request already answers every field, restate it as a Requirements Receipt and ask for confirmation. Still do not begin work in that response.
4. After the user's answer, ask a short follow-up only for missing fields that would materially change the result.
5. Present one Requirements Receipt separating `Confirmed` from `Recommended/Inferred`. Include scope, source, destination, aspect, fps, style, intensity, subtitles, assets, face/safe zones, audio, review flow, and final deliverable.
6. Ask: `请确认是否按以上需求开始制作？` Wait for an explicit confirmation such as `确认`、`开始`、`按这个做`.
7. Only explicit confirmation opens the execution gate. Silence, `继续`, an uploaded file, or a partial answer does not count as confirmation.

Read-only technical probing is allowed before confirmation only when the user explicitly asks Codex to inspect a file in order to answer an intake question. Report the probe result, update the receipt, and keep the execution gate closed.

## Load Base Contracts After Confirmation

1. Read `/hyperframes` and follow its existing-project or fresh-project branch.
2. For a fresh talking-head package, use `/talking-head-recut`; use `/general-video` when the footage itself must be re-edited or remixed.
3. Read `/hyperframes-core` before changing composition HTML, `/hyperframes-keyframes` for seek-safe animation, `/hyperframes-cli` before checks or preview, and `/media-use` before adding media or audio.
4. Treat the confirmed Requirements Receipt as authoritative. Write it into `BRIEF.md`; do not silently restore this skill's previous 9:16 technology choices.

Read [references/style-system.md](references/style-system.md) only when the confirmed style is technology/AI or the user explicitly selects that preset. Read [references/timeline-playbook.md](references/timeline-playbook.md) before drafting or revising a timeline, then adapt it to the confirmed style, ratio, and pacing.

## No Automatic Creative Defaults

- Do not assume `9:16`, `1080x1920`, `60fps`, technology styling, dark colors, face coverage, no BGM, SFX, or a `15-20s` scope.
- Recommend a value when useful, explain why it fits the destination, and place it under `Recommended/Inferred` until the user confirms it.
- Preserve source speech and existing burned-in subtitles unless the receipt explicitly says otherwise.
- Do not add a second full subtitle track when the source already contains readable subtitles unless the user asks for replacement captions.
- Never render the final MP4 without a separate explicit approval after Studio review.

## Execution Workflow

### 1. Resume Or Set Up

- Existing project: read `BRIEF.md`, transcript files, storyboard, media ledger, and `index.html`; preserve unrelated work.
- Fresh project: create an independent HyperFrames project. Probe the source with FFprobe and create a browser-friendly proxy only when needed.
- Run the project's pinned-CLI upgrade probe before the first render-affecting command.

### 2. Build The Speech Timeline

- Reuse a trustworthy word/segment transcript when present.
- Otherwise transcribe locally with the best configured model appropriate to the confirmed language.
- Correct product names and technical terms without changing timestamps.
- Produce semantic beats with exact timing, spoken idea, emphasis keywords, and candidate visual job.
- State uncertainty instead of inventing unclear speech.

### 3. Map Assets To Speech

- Inventory only confirmed screenshots, screen recordings, diagrams, logos, data, and permitted searched/generated media.
- Attach each asset to the line that explains it. Do not front-load later evidence for variety.
- Adapt crops, callout size, and takeover duration to the confirmed canvas and viewing device.
- Record source, usage interval, derivative crops, and rights in the media ledger.

### 4. Design And Build

- Make every spoken concept perform one visual job: explain, prove, compare, warn, demonstrate, or summarize.
- Use the confirmed style and intensity; do not import the technology palette into magazine, corporate, playful, documentary, or other styles.
- Keep media as direct children of the composition root, mount source audio separately, and register one seek-safe paused master timeline.
- Use deterministic motion, local frozen media, finite repeats, and no render-time randomness or manual media playback.
- Treat any later request for BGM, external assets, paid generation, or changed aspect as a requirement change: update the receipt and reconfirm before applying it.

### 5. Verify And Hand Off

- Run `hyperframes check` through the project's wrapper after edits.
- Sample the hook, every scene boundary, every evidence takeover, every audio cue, and the closing frame.
- Inspect readability, subtitle policy, confirmed safe zones, intentional face coverage, asset clarity, audio dominance, and seek determinism at the target viewing size.
- Keep `render_approved: false`, open or reuse Studio preview, and ask whether to revise or render.

## Invocation Examples

```text
$hyperframes-tech-talking-head 我有一条口播视频，先问清楚需求再开始制作。
$hyperframes-tech-talking-head 继续包装这个视频；比例、风格和动效强度都先向我确认。
$hyperframes-tech-talking-head 这次可能不是科技风，请先完成需求访谈。
```
