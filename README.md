# Feishu Morty TTS Skill

一个 OpenClaw skill，使用火山引擎 TTS 将文本转换为语音，并发送到飞书。

## 功能特性

- 支持单聊和群聊
- 使用火山引擎 TTS（支持音色克隆）
- 自动将音频转换为飞书支持的 Opus 格式

## 前置要求

- 飞书机器人应用（App ID, App Secret）
- 火山引擎 API Key 和已克隆的音色
- OpenClaw 环境
- ffmpeg 和 ffprobe

## 安装

### 1. 作为 OpenClaw Skill 安装

将此目录复制到 OpenClaw 的 skills 目录：

```bash
cp -r feishu-morty-tts ~/.openclaw/skills/
```

### 2. 配置环境变量

```bash
export FEISHU_APP_ID="你的飞书AppID"
export FEISHU_APP_SECRET="你的飞书AppSecret"
export FEISHU_CHAT_ID="user:你的用户OpenID"  # 或 chat:群聊ID
export VOLC_API_KEY="你的火山引擎APIKey"
export VOLC_VOICE_TYPE="你的音色ID"
```

### 3. 或使用配置文件

创建 `~/.volcengine_key`：

```json
{
  "api_key": "你的火山引擎APIKey"
}
```

## 使用方法

### 命令行使用

```bash
# 发送到默认聊天
python feishu_tts.py "你好，这是一条语音消息"

# 发送到指定群聊
python feishu_tts.py -c "chat:oc_xxxxx" "群聊消息"

# 发送到指定单聊
python feishu_tts.py -c "user:ou_xxxxx" "单聊消息"
```

### 聊天 ID 格式

| 格式 | 类型 |
|-----|------|
| `user:ou_xxxxx` | 单聊（Open ID） |
| `chat:oc_xxxxx` | 群聊（Chat ID） |

## 作为 OpenClaw Skill 使用

在 OpenClaw 对话中，直接让它发送语音消息即可。

## 文件说明

- `feishu_tts.py` - 主脚本
- `SKILL.md` - OpenClaw Skill 说明
- `package.json` - Skill 元数据
- `README.md` - 本文件

## License

MIT
