---
name: feishu-voice-clone-tts
description: Convert text to speech with Volcengine preset or cloned voices, convert the audio to Opus, and send it to a Feishu user or group through a bot. Use when the user explicitly asks to synthesize and deliver a Feishu voice message, or when configuring or troubleshooting this repository's TTS workflow.
---

# Feishu Voice Clone TTS

使用火山引擎预置或克隆音色合成语音，转为飞书要求的 Opus 格式，再通过飞书机器人发送到单聊或群聊。

## 守住发送边界

- 把发送消息视为外部副作用。除非当前请求已经明确给出文本和接收方，否则执行前先确认二者。
- 不要在输出、日志或案例中展示 App Secret、API Key、访问令牌或完整配置文件。
- 用户只要求试听、配置或排错时，不要调用飞书发送接口。
- 只有脚本返回成功结果时才能声称消息已发送；失败时给出脱敏后的阶段和错误信息。

## 检查前置条件

执行前确认：

- Python 3 已安装，并已运行 `python3 -m pip install -r requirements.txt`。
- `ffmpeg` 和 `ffprobe` 均可执行。
- 飞书机器人具备上传文件和发送消息所需权限。
- 已配置 `FEISHU_APP_ID`、`FEISHU_APP_SECRET`、`VOLC_API_KEY` 和 `VOLC_VOICE_TYPE`。
- 已通过 `FEISHU_CHAT_ID` 或命令行 `-c` 提供接收方。

接收方格式：

- `user:ou_xxx`：按用户 Open ID 发送单聊。
- `chat:oc_xxx`：按 Chat ID 发送群聊。

## 执行工作流

1. 确认发送文本、接收方和使用的音色 ID。
2. 检查依赖与环境变量，不输出变量值。
3. 调用 `feishu_tts.py`。脚本依次完成语音合成、Opus 转码、飞书文件上传和消息发送。
4. 根据脚本退出码报告结果。失败时说明失败发生在合成、转码、鉴权、上传还是发送阶段。

发送到默认接收方：

```bash
python3 feishu_tts.py "你好，这是一条语音消息"
```

发送到指定群聊或单聊：

```bash
python3 feishu_tts.py -c "chat:oc_xxx" "群聊消息"
python3 feishu_tts.py -c "user:ou_xxx" "单聊消息"
```

## 配置音色

- 预置音色：在火山引擎语音合成控制台选择音色并将其 ID 写入 `VOLC_VOICE_TYPE`。
- 克隆音色：先在声音复刻控制台完成授权和克隆，再使用生成的音色 ID。
- `VOLC_API_KEY` 缺失时，脚本也会尝试读取 `~/.volcengine_key` 中的 `api_key`，但环境变量更便于显式配置和排错。

不要把未经授权的真人声音用于克隆或发送。
