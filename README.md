# Agnes AI Skill（跨 Agent 工具通用）

遵循 [Agent Skills](https://agentskills.io) 开放规范的图片与视频生成技能，可在 **Trae、Claude Code、Cursor、Codex、Roo Code** 等所有兼容工具中使用。支持文生图、图生图、文生视频、图生视频等多种模式。

## ✨ 功能特性

- 🖼️ **文生图** — 根据文本描述生成高清图片
- 🎨 **图生图** — 基于参考图片进行风格转换和再创作
- 🎬 **文生视频** — 从文本直接生成视频，支持音画同步
- 🖼️➡️🎥 **图生视频** — 让静态图片动起来
- 🌐 **双站支持** — 自动适配中国站和国际站
- ⚡ **即开即用** — 配置 API Key 后直接用自然语言调用

## 支持的模型

| 任务类型 | 模型名称 | 说明 |
|---|---|---|
| 文生图、图生图 | `agnes-image-2.1-flash` | 高清图片生成，支持复杂构图 |
| 图片编辑、多图合成 | `agnes-image-2.0-flash` | 图像编辑与风格转换 |
| 文生视频、图生视频 | `agnes-video-v2.0` | 视频生成，支持原生音画同步 |

## 📦 安装

本 Skill 遵循 [Agent Skills](https://agentskills.io) 开放规范，可在所有兼容的 AI Agent 工具中使用。

### 方法一：AI 自动安装（推荐 ⭐）

将以下内容复制并发给你正在使用的 AI Agent（Trae / Claude Code / Cursor 等），AI 会自动下载并安装：

```
请帮我下载并安装这个 skill：https://github.com/Buffaiai/agnes-ai-skill
```

### 方法二：手动安装（全局生效）

各工具扫描的 skills 目录不同，按下表放置（将文件夹重命名为 `agnes-ai`）：

| 工具 | 全局 skills 目录（macOS / Linux） |
|---|---|
| Codex / Cursor / Roo Code 等 | `~/.agents/skills/agnes-ai` |
| Claude Code / Claude.app | `~/.claude/skills/agnes-ai` |
| Trae（中国版） | `~/.trae-cn/skills/agnes-ai` |
| Trae（国际版） | `~/.trae/skills/agnes-ai` |

**一键安装（macOS / Linux）**：以 `~/.agents` 为唯一真源，软链接到各工具目录，一次配置所有工具通用：

```bash
git clone https://github.com/Buffaiai/agnes-ai-skill.git /tmp/agnes-ai-skill
mkdir -p ~/.agents/skills
cp -r /tmp/agnes-ai-skill ~/.agents/skills/agnes-ai
# 软链接到其他工具（可选，共享同一份文件避免重复维护）
mkdir -p ~/.claude/skills ~/.trae-cn/skills ~/.trae/skills
ln -sf ../../.agents/skills/agnes-ai ~/.claude/skills/agnes-ai
ln -sf ../../.agents/skills/agnes-ai ~/.trae-cn/skills/agnes-ai
ln -sf ../../.agents/skills/agnes-ai ~/.trae/skills/agnes-ai
```

### 方法三：仅在当前项目生效（项目级）

在项目根目录下创建对应工具的项目级 skills 目录：

```bash
# Codex / Cursor / Roo Code 等
mkdir -p .agents/skills && cp -r agnes-ai-skill .agents/skills/agnes-ai

# Claude Code
mkdir -p .claude/skills && cp -r agnes-ai-skill .claude/skills/agnes-ai

# Trae
mkdir -p .trae/skills && cp -r agnes-ai-skill .trae/skills/agnes-ai
```

安装后重启对应工具即可生效。

## 🔑 配置 API Key

### 1. 获取 API Key

1. 访问 [Agnes AI 中国站](https://agnes-ai.cn)（推荐国内用户）或 [国际站](https://agnes-ai.com) 注册账号
2. 进入控制台，创建 API Key 并复制

> Agnes AI 目前提供永久免费额度，无需绑定信用卡。

### 2. 设置环境变量

```bash
# 中国站（推荐）
export AGNES_CN_API_KEY="your-api-key-here"

# 国际站
export AGNES_API_KEY="your-api-key-here"
```

建议将上述命令添加到你的 shell 配置文件（`~/.zshrc` 或 `~/.bashrc`）中，以便永久生效。

## 🚀 使用方式

配置好 API Key 后，在 Trae 中直接用自然语言描述即可：

### 文生图

```
用 Agnes 生成一张赛博朋克风格的城市夜景图，霓虹灯，雨天，高清
```

### 图生图

```
用 Agnes 把这张图片改成宫崎骏风格
```

### 文生视频

```
用 Agnes 生成一段 5 秒的海浪拍打沙滩的视频，720P
```

### 图生视频

```
用 Agnes 让这张图片动起来，生成 5 秒视频
```

更多示例请查看 [examples/](./examples/) 目录。

## 📁 目录结构

```
agnes-ai-skill/
├── SKILL.md              # 技能核心文件（必须）
├── README.md             # 项目说明
├── LICENSE               # 开源协议
└── examples/             # 使用示例
    ├── text-to-image.md
    ├── image-to-image.md
    └── text-to-video.md
```

## ⚠️ 注意事项

- 中国站和国际站的 API Key 不通用，需分别注册
- 视频生成耗时较长（通常 30 秒 - 3 分钟），请耐心等待
- **不要将 API Key 提交到公开代码仓库**
- 图片生成是同步接口，视频生成是异步接口

## 🔗 相关链接

- [Agnes AI 官网](https://agnes-ai.com)
- [Agnes AI 中国站](https://agnes-ai.cn)
- [Agnes AI 官方文档](https://wiki.agnes-ai.com/zh-Hans/docs/overview)
- [Agent Skills 开放规范](https://agentskills.io) — 本技能遵循的跨工具标准
- [Trae 官网](https://trae.ai)

## 📄 许可证

MIT License
