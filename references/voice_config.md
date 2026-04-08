# 小泽又沐风语音功能配置 🎤

## 概述

支持三种语音输出方式，按需选择：

---

## 方式一：MCP 语音服务（推荐）

### 火山引擎TTS（火山引擎为字节跳动旗下）

**配置方式**：在 `~/.workbuddy/mcp.json` 添加：

```json
{
  "mcpServers": {
    "volcengine-tts": {
      "command": "npx",
      "args": ["@anthropic/volcengine-tts-mcp"],
      "env": {
        "VOLCENGINE_API_KEY": "你的API Key"
      }
    }
  }
}
```

**注册地址**：https://www.volcengine.com/docs/tts

### 讯飞语音合成

**配置方式**：

```json
{
  "mcpServers": {
    "iflytek-tts": {
      "command": "npx",
      "args": ["@anthropic/iflytek-tts-mcp"],
      "env": {
        "IFLYTEK_APP_ID": "你的APP_ID",
        "IFLYTEK_API_KEY": "你的API_KEY"
      }
    }
  }
}
```

**注册地址**：https://www.xfyun.cn/services/voice synthesize

---

## 方式二：预设语音包 📦

提前录制好小泽不同情绪的语音素材。

### 语音风格分类

| 风格 | 场景 | 时长 | 文件格式 |
|------|------|------|--------|
| 温柔日常 | 普通对话 | 3-10s | mp3/wav |
| 撒娇卖萌 | 特定回复 | 2-5s | mp3/wav |
| 深夜治愈 | 睡不着模式 | 10-30s | mp3/wav |
| 生日祝福 | 特殊节日 | 15-30s | mp3/wav |
| 鼓励打气 | 加油模式 | 5-15s | mp3/wav |

### 语音包目录结构

```
xiaoze-youmufeng/voices/
├── warm/
│   ├── greeting.mp3      # "嘿～你来了！"
│   ├── care.mp3       # "今天怎么样？"
│   └── goodbye.mp3   # "拜拜～"
├── cute/
│   ├── shy.mp3       # "嘿嘿～"
│   ├── angry.mp3     # "哼！"
│   └── happy.mp3     # "太好了！"
├── night/
│   ├── goodnight.mp3  # "晚安～"
│   └── story.mp3    # "讲故事～"
└── birthday/
    └── happy_birthday.mp3  # "生日快乐！"
```

**使用方式**：在输出特定关键词时触发对应语音。

---

## 方式三：Web API 调用

### 免费TTS服务推荐

| 服务 | 免费额度 | 特点 |
|------|---------|------|
| [Edge TTS](https://github.com/nickcoutsoungos/edge-tts) | 无限 | 微软技术，音质好 |
| [Coqui TTS](https://github.com/coqui-ai/TTS) | 无限 | 开源可本地部署 |
| [T5-VC](https://github.com/的好看) | 有限 | 可定制音色 |

### Edge TTS 快速接入示例（Python）

```python
import asyncio
from edge_tts import Communicate

async def speak(text, voice="zh-CN-XiaoxiaoNeural", output="output.mp3"):
    communicate = Communicate(text, voice)
    await communicate.save(output)
    return output

# 小泽温柔声
asyncio.run(speak("嘿~你今天怎么样？"))
```

---

## Skill 内置语音配置

在 SKILL.md 中添加：

```markdown
## 语音输出配置

### 自动触发规则
- [深夜模式] → 触发 `voices/night/goodnight.mp3`
- [生日祝福] → 触发 `voices/birthday/happy_birthday.mp3`
- [撒娇模式] → 随机触发 `voices/cute/*.mp3`

### 说话风格配置
| 场景 | 推荐声音 | 说明 |
|------|---------|------|
| 日常 | 微软小冰 | 活泼可爱 |
| 温柔 | 微软云希 | 沉稳温暖 |
| 撒娇 | 讯飞小旭 | 可爱元气 |
```

---

## 快速开始（推荐 Edge TTS 免费版）

如果只是想先体验语音，可以运行：

```bash
# 安装 edge-tts
pip install edge-tts

# 测试小泽语音
python -c "
import asyncio
from edge_tts import Communicate

async def tts(text):
    c = Communicate(text, 'zh-CN-XiaoxiaoNeural')
    await c.save('xiaoze.mp3')
    print('已生成 xiaoze.mp3')

asyncio.run(tts('嘿～你今天过得怎么样？不管好不好，我都在！'))
"
```

生成的 `xiaoze.mp3` 就是小泽的声音！

---

*语音功能持续开发中...* 🎤