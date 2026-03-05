# Feishu Morty TTS Skill

使用火山引擎 TTS 将文本转换为语音，并发送到飞书。

## 配置

需要配置以下环境变量：

- `FEISHU_APP_ID` - 飞书 App ID
- `FEISHU_APP_SECRET` - 飞书 App Secret
- `FEISHU_CHAT_ID` - 飞书聊天 ID (user:xxx 或 chat:xxx)
- `VOLC_API_KEY` - 火山引擎 API Key
- `VOLC_VOICE_TYPE` - 火山引擎音色 ID

## 使用

```
用户: 用语音说"你好"
OpenClaw: [调用 TTS] [发送语音消息到飞书]
```

## 命令

- `python feishu_tts.py "文本"` - 发送语音消息
- `python feishu_tts.py -c "chat:oc_xxx" "文本"` - 发送到指定群聊
