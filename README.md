# HyperFrames Tech Talking Head

一个面向 Codex 的 HyperFrames 口播视频定制包装 Skill。

它不是一套固定的“科技风模板”，也不会收到视频后立刻开工。每次新任务都会先确认制作范围、发布平台、画幅、风格、动效强度、字幕、素材、安全区、音频和交付方式；只有用户确认《需求确认单》后，才进入制作。

仓库名称保留了最初的 `tech-talking-head`，但当前版本不限于科技或 AI 风格。科技、知识、杂志、极简、企业、纪录片、活泼等方向都可以选择，最终方案以本次确认的需求为准。

> 第一次使用 Codex 或 HyperFrames？先完成 [新手环境配置](docs/setup.md)，再调用本 Skill。

## 它解决什么问题

很多口播包装的失败，不是动效做得不够多，而是开始制作前没有确认清楚：发到哪里、画面比例是什么、原字幕要不要保留、能不能遮脸、截图是否允许全屏、需不需要 BGM，以及最终只看方案还是要交付 MP4。

这个 Skill 把这些决定前置，并在后续制作中持续遵守：

- 为已有口播、访谈、课程或知识视频增加有信息价值的视觉包装。
- 根据抖音、小红书、YouTube 等目标平台选择画幅、分辨率和观看尺度。
- 按用户确认的风格组织标题、信息卡、截图、B-roll、分屏、流程图和动效。
- 将截图、录屏、Logo、图表和数据放到真正解释它们的口播时间点。
- 明确原字幕、新字幕、人物、产品与安全区的保护规则。
- 单独确认原声、BGM、SFX 和最终交付，不把旧项目的偏好偷偷带进新任务。

## 核心流程

```mermaid
flowchart LR
    A["需求访谈"] --> B["需求确认单"]
    B --> C["定制制作与检查"]
    C --> D["Studio 预览"]
    D --> E["单独批准最终渲染"]
```

1. **需求访谈**：第一次回复只询问尚未明确、且会改变结果的问题，最多归并为六组；不会读取素材、修改工程或启动渲染。
2. **需求确认单**：把用户明确回答的内容放在 `Confirmed`，把建议和推断单独列在 `Recommended/Inferred`，等待用户明确确认。
3. **定制制作**：确认后才读取素材、建立口播时间线、映射截图与 B-roll，并按选定画幅、风格和节奏制作。
4. **Studio 预览**：完成 HyperFrames 检查后打开预览，继续修改或进入交付评审。
5. **最终渲染**：即使需求确认单已经通过，也必须在 Studio 审核后再次获得明确批准，才渲染最终 MP4。

## 可以确认哪些内容

| 维度 | 可选内容示例 |
| --- | --- |
| 制作范围 | 全片、前 `15-20s`、指定片段、只出方案、修改已有工程 |
| 发布目标 | 抖音、小红书、YouTube、课程、站内播放器或自定义平台 |
| 画布 | `9:16`、`16:9`、`4:5`、`3:4`、`1:1` 或自定义尺寸 |
| 视觉风格 | 科技/AI、知识、杂志、极简、企业、纪录片、活泼或用户参考风格 |
| 动效强度 | 克制、中等、夸张，以及具体参考视频或图片 |
| 字幕 | 保留烧录字幕、新增字幕、替换字幕或不加第二套字幕 |
| 视觉素材 | 截图、录屏、B-roll、Logo、图表、数据，以及是否允许搜索或生成外部素材 |
| 构图边界 | 是否允许遮脸、全屏接管，以及人物、产品和字幕安全区 |
| 音频 | 原声、BGM、SFX，或完全不增加额外音频 |
| 评审与交付 | 先看方案、先做开头 V1、全片 Studio 预览、最终 MP4 |

## 关键边界

- 不自动假设 `9:16`、科技风、深色画面、`60fps`、无 BGM、需要 SFX 或只做前 `15-20s`。
- 用户信息不足时可以给出适合平台的建议，但建议在确认前不等于需求。
- 默认保留原始口播和已有烧录字幕；用户明确要求时才替换。
- 外部搜索、生成素材、付费服务和素材授权需要明确许可。
- 制作中途新增 BGM、改变画幅或引入外部素材，视为需求变更，需要更新确认单并重新确认。
- `hyperframes check` 通过不等于自动获准渲染，最终 MP4 始终需要单独批准。

## 前置条件

本仓库是 HyperFrames 的需求与决策层，不是独立渲染器。最小环境如下：

| 项目 | 要求 |
| --- | --- |
| Codex | 使用支持 Skills、可访问本地文件和终端的 Codex 桌面端、CLI 或 IDE 扩展 |
| Node.js | `22` 或更高版本，包含 `npm` 和 `npx` |
| FFmpeg | `ffmpeg` 与 `ffprobe` 都能从终端调用 |
| HyperFrames | 安装 `talking-head-recut` 工作流及核心 Skills |
| 浏览器 | Chrome/Chromium；缺失时可由 HyperFrames 下载固定版本 |
| 素材 | 自有或已获授权的视频、截图、录屏、字体和音效 |

GitHub 账号、GitHub token、OpenAI API Key、Docker、云渲染账号、NVIDIA GPU 和 CUDA 都不是本地基础流程的必需条件。完整安装、可选能力和排错方法见 [docs/setup.md](docs/setup.md)。

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
|               |-- requirements-intake.md
|               |-- style-system.md
|               `-- timeline-playbook.md
|-- docs/
|   `-- setup.md
|-- examples/
|   `-- prompts.md
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

安装后新建一个 Codex 任务；如果 Skill 没有出现在选择器中，重启 Codex。然后显式调用：

```text
$hyperframes-tech-talking-head 我有一条口播视频，先问清楚需求再开始制作。
```

第一次回复只出现需求问题是正常行为，不是 Skill 没有执行。回答问题并确认《需求确认单》后，Codex 才会读取素材和开始制作。

## 调用示例

```text
$hyperframes-tech-talking-head 继续包装这个视频；比例、风格和动效强度都先向我确认。
```

```text
$hyperframes-tech-talking-head 这次可能不是科技风，请先完成需求访谈。
```

更多例子见 [examples/prompts.md](examples/prompts.md)。

## 示例与演示素材

仓库只提供调用示例，不包含人物原视频、画面截图、录音、商业素材或渲染成片，以避免传播未授权媒体。使用者应提供自己拥有或获准使用的素材。

## 许可证

代码与 Skill 文档采用 [MIT License](LICENSE)。输入视频、截图、字体、音效和其他媒体仍受各自权利与许可证约束，MIT License 不授予这些第三方素材的使用权。

## 发布与版本

版本遵循语义化版本：

- `MAJOR`：工作流、确认门槛或调用约定存在不兼容变化。
- `MINOR`：新增向后兼容的规则、版式或工作流能力。
- `PATCH`：文档修订、兼容性修复或不改变调用方式的小改进。

- `v2.0.0`：加入强制需求访谈和《需求确认单》，取消固定 9:16 科技风等自动创意默认值。
- `v1.0.1`：增加面向 Codex 新用户的环境配置与排错文档。
- `v1.0.0`：发布最初的 9:16 科技口播包装预设。
