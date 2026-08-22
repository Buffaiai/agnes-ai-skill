# Agnes AI Skill for Trae

在 Trae 中使用 Agnes AI 的图片和视频生成模型，支持文生图、图生图、文生视频、图生视频等多种模式。

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

### 方法一：AI 自动安装（推荐 ⭐）

将以下内容复制并发给 Trae 中的 AI，AI 会为你自动下载并添加 Skill：

```
请帮我下载并安装这个 skill：https://github.com/Buffaiai/agnes-ai-skill
```

AI 会自动完成下载、安装到 skills 目录，无需手动操作。

### 方法二：全局安装

将整个 `agnes-ai` 文件夹放到 Trae 全局 skills 目录：

```bash
# macOS
cp -r agnes-ai-skill ~/.trae-cn/skills/agnes-ai
```

### 方法三：工作区安装

仅在当前项目中使用：

```bash
# 在你的项目根目录下
mkdir -p .trae/skills
cp -r agnes-ai-skill .trae/skills/agnes-ai
```

安装后重启 Trae 即可生效。

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
- [Trae 官网](https://trae.ai)

## 📄 许可证

MIT License
