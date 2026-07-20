# 新手环境配置

这份文档面向第一次使用 Codex、Skills 或 HyperFrames 的用户。目标是先把本机配置到“能识别 Skill、能读取素材、能打开 Studio 预览”的状态，再开始制作视频。

## 你需要准备什么

### 必须

| 配置 | 用途 | 验证方式 |
| --- | --- | --- |
| Codex 本地工作环境 | 读取视频、运行命令、调用 Skills | 能在桌面端、CLI 或 IDE 中打开本地文件夹 |
| OpenAI/ChatGPT 登录 | 使用 Codex | Codex 中可以正常创建任务 |
| Node.js 22+ | 运行 HyperFrames CLI | `node --version` |
| npm 与 npx | 首次下载并运行 HyperFrames | `npm --version`、`npx --version` |
| FFmpeg 与 FFprobe | 探测、转码和验证音视频 | `ffmpeg -version`、`ffprobe -version` |
| Chrome/Chromium | Studio 检查、截图和渲染 | `npx hyperframes doctor` |
| 本地可写目录 | 保存工程、代理素材和检查结果 | Codex 能在项目目录创建文件 |
| 首次联网 | 从 npm、GitHub 下载 CLI、Skills 和固定版 Chrome | 能访问 npm 与本仓库 |
| 合法素材 | 输入视频、截图、录屏、字体和音效 | 确认拥有或取得使用许可 |

### 不必提前配置

- 不需要 GitHub 账号或 GitHub token：本仓库是公开仓库。
- 不需要 OpenAI API Key：使用 Codex 登录态即可调用本 Skill。
- 不需要 Docker：只有显式使用 `render --docker` 时才需要。
- 不需要 AWS、Google Cloud 或其他云账号：本地预览和渲染不依赖云服务。
- 不需要 NVIDIA GPU、CUDA 或本地 Whisper：已有逐字稿时可以直接使用；需要自动转写时再按实际环境选择方案。
- 不需要准备背景音乐：本 Skill 默认无 BGM。

## 不会配置？先把这段发给 Codex

在支持本地终端的 Codex 中粘贴：

```text
我第一次配置 HyperFrames。请先不要制作或渲染视频，也不要要求我提供任何 token。请检查 Node.js 是否为 22+、npm/npx、FFmpeg/FFprobe、HyperFrames Skills 和 Chrome；列出缺失项，能安全自动安装的就安装，然后运行 npx hyperframes skills check 与 npx hyperframes doctor。最后告诉我是否已经满足 hyperframes-tech-talking-head 的前置条件。
```

Codex 可能会请求运行安装命令、写入 Skills 目录或联网下载浏览器。只批准与上述组件对应的操作，不要粘贴账号密码、API Key 或其他密钥。

## 第 1 步：安装并打开 Codex

Skills 可用于 Codex CLI、IDE 扩展和支持 Skills 的桌面端。视频制作需要本地文件和终端能力，因此不要只在普通网页聊天中粘贴调用词。

官方入口：

- [Codex CLI](https://learn.chatgpt.com/docs/codex/cli)
- [Codex IDE 扩展](https://learn.chatgpt.com/docs/codex/ide)
- [ChatGPT 桌面端](https://learn.chatgpt.com/docs/app)
- [Codex Skills 说明](https://learn.chatgpt.com/docs/build-skills.md)

安装后登录 OpenAI/ChatGPT 账号，并在 Codex 中打开一个专门用于视频工程的本地文件夹。路径尽量简短，确保当前用户有读写权限，并预留足够空间存放源视频、代理文件和渲染结果。Studio 使用本机 `localhost` 地址；如果系统防火墙询问是否允许本地 Node.js 服务，请只允许可信的本地网络范围。

## 第 2 步：安装 Node.js 和 FFmpeg

安装 [Node.js](https://nodejs.org/en/download) 22 或更高版本。Node.js 安装包应同时提供 `npm` 和 `npx`。

安装 [FFmpeg](https://ffmpeg.org/download.html)，并确保 `ffmpeg` 与 `ffprobe` 都已加入系统 `PATH`。Windows 用户安装后通常需要重新打开终端或重启 Codex，新的 `PATH` 才会生效。

在终端逐项检查：

```bash
node --version
npm --version
npx --version
ffmpeg -version
ffprobe -version
```

其中 `node --version` 必须是 `v22` 或更高。任何一条显示“找不到命令”，都应先修复安装或 `PATH`，不要继续安装 Skill。

## 第 3 步：安装 HyperFrames 基础 Skills

本仓库只提供科技口播视频的偏好与决策层。实际工程创建、时间线、媒体处理、检查和 Studio 预览由 HyperFrames 基础 Skills 负责。

运行：

```bash
npx hyperframes skills update talking-head-recut
```

这条命令会安装或刷新：

- `talking-head-recut` 口播包装工作流；
- `hyperframes` 入口 Skill；
- `hyperframes-core`、`hyperframes-keyframes`、`hyperframes-cli` 等核心 Skills；
- `media-use` 媒体与音频处理 Skill。

如果以后需要对源视频做重排、重混、重新取景或其他结构性修改，再安装：

```bash
npx hyperframes skills update general-video
```

不要为首次使用一次性安装所有工作流；先安装本 Skill 实际依赖的 `talking-head-recut` 即可。

## 第 4 步：运行环境自检

```bash
npx hyperframes skills check
npx hyperframes doctor
```

`skills check` 用于检查核心 Skills 是否缺失或过期。若失败，重新运行：

```bash
npx hyperframes skills update talking-head-recut
```

`doctor` 会检查 Node.js、FFmpeg、FFprobe、Chrome、CPU、内存和磁盘。第一次运行如果报告缺少浏览器，执行：

```bash
npx hyperframes browser ensure
```

然后再次运行 `npx hyperframes doctor`。Docker 相关警告在本地普通渲染中可以忽略；只有选择 Docker 渲染时才需要处理。

## 第 5 步：安装本 Skill

在 Codex 对话中粘贴下面这句话，不要在普通系统终端中运行：

```text
$skill-installer 从 https://github.com/HaoAI-Explorer/hyperframes-tech-talking-head/tree/main/.agents/skills/hyperframes-tech-talking-head 安装这个 skill
```

Skill Installer 会从公开 GitHub 仓库下载安装。本仓库不需要 GitHub 登录，也不要把 GitHub token、OpenAI token 或其他密钥粘贴给 Codex。

手工安装有两种方式：

1. 项目级：把 `hyperframes-tech-talking-head` 目录放到当前项目的 `.agents/skills/` 中。
2. 仓库级：克隆本仓库，然后从仓库目录或其子目录启动 Codex；Codex 会发现仓库内的 `.agents/skills/`。

优先使用 `$skill-installer`，它可以避免复制错目录层级。正确结构必须是 `hyperframes-tech-talking-head/SKILL.md`，不能多套一层同名目录。

## 第 6 步：让 Codex 重新发现 Skill

安装完成后新建一个 Codex 任务，并显式调用：

```text
$hyperframes-tech-talking-head 把这条带字幕的口播视频包装成 9:16 高级科技教学视频
```

如果找不到 Skill：

1. 确认安装结果中存在 `hyperframes-tech-talking-head/SKILL.md`。
2. 新建任务，不要继续使用安装前已经打开的旧任务。
3. 在 CLI 或 IDE 中输入 `$` 或运行 `/skills`，检查 Skill 是否出现。
4. 仍未出现时，完全退出并重新打开 Codex。

## 第 7 步：准备第一个视频工程

建议把这些文件放进同一个新工程目录：

- 原始口播视频；
- 已烧录字幕的视频版本，或可信逐字稿；
- 与口播内容对应的截图、录屏和图表；
- 素材来源与授权说明。

然后告诉 Codex 素材位置、目标平台、画幅和希望先做前 20 秒还是完整视频。默认设置已经是 `1080x1920`、无 BGM、少量 SFX，并且先打开 Studio 预览，不会未经确认直接渲染最终 MP4。

## 常见问题

### `npx` 或 `node` 找不到

Node.js 没有安装，或新 `PATH` 尚未被当前 Codex/终端进程读取。安装 Node.js 22+ 后重新打开终端和 Codex。

### `ffmpeg` 或 `ffprobe` 找不到

安装完整 FFmpeg 发行版，并把其可执行文件目录加入 `PATH`。只安装某个播放器不等于安装 FFmpeg 命令行工具。

### HyperFrames 提示 Node.js 版本过低

升级到 Node.js 22 或更高版本，再重新运行 `npx hyperframes doctor`。

### `skills check` 报告核心 Skill 缺失或过期

```bash
npx hyperframes skills update talking-head-recut
```

不要根据记忆手工重建缺失的 HyperFrames Skill。

### `doctor` 报告 Chrome 缺失

```bash
npx hyperframes browser ensure
```

HyperFrames 使用固定版本的 Chrome，以减少不同机器之间的画面差异。

### 安装成功但 `$hyperframes-tech-talking-head` 不出现

新建任务或重启 Codex，并确认目录中直接存在 `SKILL.md`。如果目标目录原本已存在，Skill Installer 会停止而不是覆盖；让 Codex先检查旧版本，再决定更新或替换。

### Studio 打不开或检查失败

进入已由 HyperFrames 初始化、包含项目文件的工程目录，再运行：

```bash
npx hyperframes doctor
npx hyperframes check
```

保留完整错误摘要，让 Codex按错误定位。不要跳过 `check` 直接渲染。

### 没有 GPU，能不能用

可以。GPU/CUDA 主要影响某些本地转写方案的速度，不是 HTML 合成、Studio 预览或普通本地渲染的硬性前提。

### 需要 API Key 吗

本 Skill 的本地基础流程不需要 OpenAI API Key。只有你主动选择第三方媒体服务、云渲染、TTS 或其他外部能力时，才按对应服务单独配置凭证；不要把密钥写进项目文件或聊天记录。
