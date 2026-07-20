# HyperFrames Tech Talking Head

一个面向 Codex 的公开 Skill，用 HyperFrames 将现有中文口播素材包装成适合手机观看的 9:16 科技或 AI 教学视频。

它保留原始口播和画面内已有字幕，把截图、证据特写、大字标题、信息卡、流程图和少量音效严格对齐到语义时间线。默认不加背景音乐，并且只完成 Studio 预览；最终渲染必须由用户明确批准。

> 第一次使用 Codex 或 HyperFrames？先按 [新手环境配置](docs/setup.md) 完成安装和自检，再调用本 Skill。

## 这个 Skill 做什么

- 将带字幕的中文口播包装成克制、清晰的科技教学视频。
- 优化桌面截图在手机画布上的可读性，采用“全局上下文 -> 细节放大 -> 通俗标注”的处理。
- 根据口播语义安排截图、分屏、参数演示、时间线、检查清单和流程图。
- 允许有目的的短暂遮脸，但始终保护原字幕区域。
- 默认无 BGM，只使用少量与可见动作同步、明显低于人声的 SFX。
- 使用确定性的 HyperFrames 时间线，并在获得渲染批准前停留在 Studio 预览。

## 前置条件

本仓库提供的是 HyperFrames 工作流的偏好与决策层，不是独立的视频渲染器。最小环境如下：

| 项目 | 要求 |
| --- | --- |
| Codex | 使用支持 Skills、可访问本地文件和终端的 Codex 桌面端、CLI 或 IDE 扩展 |
| Node.js | `22` 或更高版本，包含 `npm` 和 `npx` |
| FFmpeg | `ffmpeg` 与 `ffprobe` 都能从终端调用 |
| HyperFrames | 安装 `talking-head-recut` 工作流及核心 Skills |
| 浏览器 | Chrome/Chromium；缺失时可由 HyperFrames 下载固定版本 |
| 素材 | 自有或已获授权的视频、截图、录屏、字体和音效 |

GitHub 账号、GitHub token、OpenAI API Key、Docker、云渲染账号、NVIDIA GPU 和 CUDA 都不是本 Skill 本地使用的必需条件。完整安装、可选能力和排错方法见 [docs/setup.md](docs/setup.md)。

## 目录结构

```text
.
|-- .agents/
|   `-- skills/
|       `-- hyperframes-tech-talking-head/
|           |-- SKILL.md
|           |-- agents/
|           |   `-- openai.yaml
|           `-- references/
|               |-- style-system.md
|               `-- timeline-playbook.md
|-- examples/
|   `-- prompts.md
|-- docs/
|   `-- setup.md
|-- LICENSE
`-- README.md
```

## 安装

### 1. 安装 HyperFrames 基础工作流

在终端运行：

```bash
npx hyperframes skills update talking-head-recut
npx hyperframes skills check
npx hyperframes doctor
```

如果 `doctor` 报告缺少 Chrome，再运行：

```bash
npx hyperframes browser ensure
```

### 2. 安装本 Skill

在 Codex 对话中粘贴：

```text
$skill-installer 从 https://github.com/HaoAI-Explorer/hyperframes-tech-talking-head/tree/main/.agents/skills/hyperframes-tech-talking-head 安装这个 skill
```

公开仓库安装不需要 GitHub 登录或 token。手工安装时，可把 skill 目录放入项目的 `.agents/skills/hyperframes-tech-talking-head`，或把整个仓库克隆后从仓库目录启动 Codex。

### 3. 开始新任务

安装后新建一个 Codex 任务；如果 Skill 没有出现在选择器中，重启 Codex。然后使用下面的显式调用方式。

## 使用

```text
$hyperframes-tech-talking-head 把这条带字幕的口播视频包装成 9:16 高级科技教学视频
```

继续已有工程时：

```text
$hyperframes-tech-talking-head 继续在现有 HyperFrames 工程上完成整条视频，截图跟口播走，不加音乐
```

默认流程会先分析源视频和逐字稿，建立语义时间线，再映射截图和信息图，完成 HyperFrames 检查并打开 Studio 预览。除非用户明确批准，否则不会渲染最终 MP4。

## 示例与演示素材

[examples/prompts.md](examples/prompts.md) 收录了可直接使用的中文调用示例。仓库不包含人物原视频、画面截图、录音、商业素材或渲染成片，以避免传播未授权媒体；使用者应提供自己拥有或获准使用的素材。

## 许可证

代码与 Skill 文档采用 [MIT License](LICENSE)。输入视频、截图、字体、音效和其他媒体仍受各自权利与许可证约束，MIT License 不授予这些第三方素材的使用权。

## 发布与版本

版本遵循语义化版本：

- `MAJOR`：工作流或调用约定存在不兼容变化。
- `MINOR`：新增向后兼容的规则、版式或工作流能力。
- `PATCH`：文字修订、兼容性修复或不改变调用方式的小改进。

首个公开版本为 `v1.0.0`；`v1.0.1` 增加面向 Codex 新用户的环境配置与排错文档。GitHub Release 的标签与仓库中的可安装内容保持一致。
