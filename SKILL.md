---
name: agnes-ai
description: "使用 Agnes AI 生成图片与视频（Agnes AI image & video generation）。支持文生图 text-to-image、图生图 image-to-image（风格转换/图像编辑/多图合成/参考图再创作）、文生视频 text-to-video、图生视频 image-to-video（让静态图片动起来/关键帧动画）。当用户要求生成、绘制、创作图片或视频，做海报、封面、插画、配图、头像、壁纸，或提到 Agnes、生图、画图、做视频、生成视频、让图动起来、text-to-image、image-to-video 等意图时触发加载。"
license: MIT
user-invocable: true
disable-model-invocation: false
metadata:
  version: "1.3.0"
  author: "Buffaiai"
  display-name: "Agnes AI 图片与视频创作助手"
---

# Agnes AI 图片与视频创作助手

通过 Agnes AI API 生成图片与视频内容，支持文生图、图生图、文生视频、图生视频、关键帧动画等多种模式。

## 何时使用本技能

当用户的请求涉及以下任一意图时，加载并使用本技能：

- **生成图片**：文生图（根据文字描述画图）、图生图（基于参考图改风格 / 再创作）
- **生成视频**：文生视频（文字描述生成视频）、图生视频（让静态图片动起来）
- **图片编辑 / 多图合成**：风格转换、图像润色、素材合成
- **提及关键词**：Agnes、生图、画图、画一张、生成图片、做视频、生成视频、图生视频、text-to-image、image-to-video 等

> 本技能可由 AI 自动加载，也可由用户通过斜杠命令 `/agnes-ai` 显式调用。所有智能体（主 Agent / 子智能体）在扫描到相关请求时均可触发。

## 支持的模型

| 任务类型 | 模型名称 | 说明 |
|---|---|---|
| 文生图、图生图 | `agnes-image-2.1-flash` | 高清图片生成，支持复杂构图，最高 4K 输出 |
| 图片编辑、多图合成 | `agnes-image-2.0-flash` | 图像编辑与风格转换 |
| 文生视频、图生视频、关键帧动画 | `agnes-video-v2.0` | 视频生成，支持原生音画同步，720P/1080P |

## 快速开始

### 1. 获取 API Key

访问 [Agnes AI 控制台](https://agnes-ai.com) 或 [中国站](https://agnes-ai.cn) 注册账号，创建 API Key。

### 2. 配置 API Key

支持以下两种方式（任选其一）：

**方式 A：环境变量（推荐）**
```bash
# 中国站
export AGNES_CN_API_KEY="your-api-key-here"

# 国际站
export AGNES_API_KEY="your-api-key-here"
```

**方式 B：对话中提供**
直接在对话中告诉模型你的 API Key，模型会在当前会话中使用。

### 3. 开始使用

用自然语言描述你想要生成的内容即可：

- "用 Agnes 生成一张赛博朋克风格的城市夜景图"
- "用 Agnes 把这张图片改成水彩画风格"
- "用 Agnes 生成一段 5 秒的海浪视频"

## API 配置详情

### Base URL

| 站点 | Base URL | 环境变量 |
|---|---|---|
| 中国站（默认） | `https://api.agnes-ai.cn/v1` | `AGNES_CN_API_KEY` |
| 国际站 | `https://apihub.agnes-ai.com/v1` | `AGNES_API_KEY` |

默认优先使用中国站，若网络请求失败自动尝试国际站。

### 认证方式

使用 Bearer Token 认证，请求头：
```
Authorization: Bearer <YOUR_API_KEY>
```

## 图片生成（同步接口）

### 文生图

**端点**：`POST /images/generations`

**请求体**：
```json
{
  "model": "agnes-image-2.1-flash",
  "prompt": "图片描述文本",
  "n": 1,
  "size": "1024x1024",
  "response_format": "url"
}
```

**支持的尺寸**：
- 正方形：512x512, 768x768, 1024x1024
- 横版：1024x768, 1536x1024
- 竖版：768x1024, 1024x1536

**响应**：返回图片 URL 或 base64 数据。

### 图生图

**端点**：`POST /images/generations`

**请求体**：
```json
{
  "model": "agnes-image-2.1-flash",
  "prompt": "目标风格描述",
  "image": "https://example.com/input.jpg",
  "n": 1,
  "size": "1024x1024",
  "response_format": "url"
}
```

`image` 字段支持传入图片 URL 或 base64 编码的图片数据。

## 视频生成（异步接口）

视频生成采用异步任务模式：先创建任务，再轮询获取结果。

### 创建视频任务

**端点**：`POST /videos/generations`

**文生视频请求体**：
```json
{
  "model": "agnes-video-v2.0",
  "prompt": "视频描述文本",
  "resolution": "720p",
  "duration": 5,
  "fps": 24
}
```

**图生视频请求体**：
```json
{
  "model": "agnes-video-v2.0",
  "prompt": "视频描述文本",
  "image": "https://example.com/input.jpg",
  "resolution": "720p",
  "duration": 5,
  "fps": 24
}
```

**参数说明**：

| 参数 | 类型 | 可选值 | 默认值 | 说明 |
|---|---|---|---|---|
| `resolution` | string | `720p`, `1080p` | `720p` | 视频分辨率 |
| `duration` | number | 5-10 | 5 | 视频时长（秒） |
| `fps` | number | - | 24 | 帧率 |
| `image` | string | - | - | 图生视频的参考图片 URL 或 base64 |

**响应示例**：
```json
{
  "id": "task-xxx",
  "status": "processing",
  "created_at": "2026-01-01T00:00:00Z"
}
```

### 获取视频结果

**端点**：`GET /videos/generations/{task_id}`

**轮询策略**：
- 首次等待 10 秒后开始轮询
- 每次间隔 5 秒
- 最长等待 5 分钟
- 状态为 `succeeded` 时返回视频 URL
- 状态为 `failed` 时返回错误信息

**任务状态**：

| 状态 | 说明 |
|---|---|
| `pending` | 排队中 |
| `processing` | 生成中 |
| `succeeded` | 生成完成 |
| `failed` | 生成失败 |

## 调用流程

1. 检查是否已配置 Agnes API Key（环境变量或用户提供）
2. 若未配置，引导用户去 Agnes AI 官网注册获取
3. 根据用户需求选择图片或视频生成模式
4. 图片生成：直接调用同步接口，返回结果并保存到本地
5. 视频生成：先创建任务，再轮询获取结果，完成后保存到本地
6. 将生成的文件路径以 `computer://` 链接形式返回给用户

## 注意事项

- 中国站和国际站的 API Key 不通用，需分别注册获取
- 视频生成耗时较长（通常 30 秒 - 3 分钟），请耐心等待
- 生成的内容请保存为本地文件供用户下载使用
- **不要在代码或日志中硬编码 API Key**
- 图片生成是同步接口，视频生成是异步接口，调用方式不同
