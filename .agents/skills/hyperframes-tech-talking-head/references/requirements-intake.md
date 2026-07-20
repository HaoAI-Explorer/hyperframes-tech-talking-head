# Requirements Intake

Use this reference before any tool call or project action. Ask only fields the user has not already answered, using at most six concise questions in the first response.

## First-Response Questions

1. **范围与源文件**：这次是新建项目还是修改已有工程？制作全片、前 `15-20s`、指定片段，还是只出方案？源视频在哪里？
2. **平台与画布**：发布到哪里？需要 `9:16`、`16:9`、`4:5`、`3:4`、`1:1` 或自定义尺寸？是否保留源帧率？
3. **风格与强度**：想要科技、杂志、极简、企业、纪录片、活泼或其他风格？有参考图/视频吗？动效强度要克制、中等还是夸张？
4. **字幕与素材**：原视频是否已有烧录字幕？是否需要新增/替换字幕？有哪些截图、B-roll、Logo、图表或数据？是否允许搜索或生成外部素材？
5. **构图与安全区**：是否允许遮脸或全屏接管？哪些区域不能遮挡？人物、产品、原字幕分别如何保护？
6. **音频与交付**：保留原声吗？需要 BGM、SFX 或都不要？先看方案、先做开头 V1、直接做全片 Studio 预览，还是最终还需要 MP4？

When several subfields are already answered, omit them rather than asking the whole question again. Offer platform-appropriate recommendations, but label them as recommendations until confirmed.

## Conditional Follow-Up

Ask only material unknowns:

- Language and transcription model when source speech cannot establish them.
- Exact duration or cut points when scope is partial.
- Resolution/fps when destination and source disagree.
- Subtitle replacement style when the user requests new captions.
- Asset licensing or paid-provider approval before external generation.
- Review order when the user requests both a storyboard and immediate production.

Do not ask about implementation details Codex can safely determine after confirmation, such as internal DOM IDs, track indices, proxy codec, or easing names.

## Requirements Receipt

Use this shape after the answers:

```text
需求确认单

Confirmed
- 范围/源文件：
- 平台/比例/分辨率/fps：
- 风格/参考/动效强度：
- 字幕/素材/外部素材权限：
- 人物与安全区：
- 原声/BGM/SFX：
- 评审流程/最终交付：

Recommended/Inferred
- ...（写明理由；没有则写“无”）

请确认是否按以上需求开始制作？
```

Do not write `BRIEF.md`, start Studio, or change files until the user explicitly confirms this receipt.
