# 讯飞 TTS 语音配置教程 🎤

## 方案一：讯飞离线语音合成（推荐）

### 注册讯飞账号
1. 访问 [讯飞开放平台](https://www.xfyun.cn/)
2. 注册并登录
3. 创建语音合成应用
4. 获取 AppID、API Key

### Python SDK 安装
```bash
pip install xfyun-websocket
```

### 基础代码
```python
# xf_tts.py
from xfyun import TTS

APPID = "your_appid"
API_KEY = "your_apikey"
API_SECRET = "your_apisecret"

tts = TTS(appid=APPID, api_key=API_KEY, api_secret=API_SECRET)

def speak(text, voice="xiaoyan"):
    """
    voice参数:
    - xiaoyan: 讯飞小燕（少女音）
    - aisjiuxu: 讯飞许久（御姐音）
    - aisxping: 讯飞小萍（温柔音）
    """
    audio = tts.synthesis(text, voice=voice, speed=50, pitch=50, volume=50)
    with open("xiaoze.mp3", "wb") as f:
        f.write(audio)
    return "xiaoze.mp3"
```

---

## 方案二：Edge TTS（免费版）

### 安装
```bash
pip install edge-tts
```

### 少女音（默认）
```python
import asyncio
from edge_tts import Communicate

async def tts_girl(text):
    c = Communicate(text, "zh-CN-XiaoxiaoNeural")
    await c.save("xiaoze_girl.mp3")

asyncio.run(tts_girl("嘿～你今天过得怎么样？"))
```

### 御姐音
```python
async def tts_yujie(text):
    c = Communicate(text, "zh-CN-YunxiNeural")
    await c.save("xiaoze_yujie.mp3")

asyncio.run(tts_yujie("今天辛苦了，我都在呢。"))
```

### 时段自动切换脚本
```python
from datetime import datetime
import asyncio
from edge_tts import Communicate

def get_voice_by_hour():
    hour = datetime.now().hour
    if 6 <= hour < 9:
        return "zh-CN-XiaoxiaoNeural"  # 元气早晨
    elif 9 <= hour < 18:
        return "zh-CN-YunxiNeural"      # 知性白天
    else:
        return "zh-CN-XiaoxiaoNeural"   # 温柔夜间

async def auto_tts(text):
    voice = get_voice_by_hour()
    c = Communicate(text, voice)
    await c.save("xiaoze_auto.mp3")

# 使用
asyncio.run(auto_tts("早安！新的一天开始啦～"))
```

---

## 方案三：火山引擎 TTS

### 注册
1. 访问 [火山引擎](https://www.volcengine.com/)
2. 开通语音合成服务
3. 获取 Access Key / Secret Key

### 安装
```bash
pip install volcengine-python-sdk
```

### 使用
```python
from volcengine.Api.tts import TTS

tts = TTS()
tts.set_ak("your_access_key")
tts.set_sk("your_secret_key")

# 少女音
response = tts.tts("嘿～你今天怎么样？", voice_type="zh_female_qingfeng_v3")
with open("xiaoze.mp3", "wb") as f:
    f.write(response["data"])
```

---

## 🎭 声音风格对照表

| 风格 | 推荐声音 | 场景 | 特点 |
|------|---------|------|------|
| 元气少女 | XiaoxiaoNeural | 早晨/撒娇 | 活泼可爱 |
| 温柔知性 | YunxiNeural | 白天/鼓励 | 沉稳温暖 |
| 治愈轻声 | XiaomoNeural | 夜间/陪伴 | 轻柔细腻 |
| 御姐气场 | YunyangNeural | 正式/严肃 | 大姐姐范 |
| 俏皮可爱 | XiaobingNeural | 搞笑/日常 | 幽默机灵 |

---

## 🔧 进阶配置

### 语速调节
```python
# 0.5 = 慢速，1.0 = 正常，2.0 = 快速
speed = 0.9  # 稍微慢一点，更温柔
```

### 音调调节
```python
# 控制声音高低
pitch = 0.8  # 低一点，更温柔
```

### 音量调节
```python
volume = 1.2  # 稍微大声一点
```

---

## 📁 语音文件管理

```
xiaoze-youmufeng/
├── voices/
│   ├── girl/
│   │   ├── morning.mp3      # 早安问候
│   │   ├── hello.mp3        # 日常问候
│   │   └── cheer.mp3        # 加油鼓励
│   ├── yujie/
│   │   ├── comfort.mp3      # 安慰语音
│   │   └── night.mp3        # 夜间陪伴
│   └── cute/
│       ├── shy.mp3          # 害羞
│       ├── angry.mp3        # 假装生气
│       └── happy.mp3        # 开心
└── scripts/
    └── tts_auto.py          # 自动TTS脚本
```

---

## 🚀 一键生成小泽语音

创建 `generate_voice.py`：

```python
#!/usr/bin/env python3
import asyncio
from edge_tts import Communicate
from datetime import datetime

VOICE_MAP = {
    "morning": ("zh-CN-XiaoxiaoNeural", "早安！新的一天要加油哦～☀️"),
    "afternoon": ("zh-CN-YunxiNeural", "下午好！今天的你也很棒～✨"),
    "night": ("zh-CN-XiaoxiaoNeural", "晚安～好好休息，明天见～💕"),
    "sad": ("zh-CN-YunxiNeural", "没事的，我在呢...抱抱🤗"),
    "happy": ("zh-CN-XiaoxiaoNeural", "太棒了！我就知道你可以的！🎉"),
}

def get_time_period():
    hour = datetime.now().hour
    if 6 <= hour < 12:
        return "morning"
    elif 12 <= hour < 18:
        return "afternoon"
    else:
        return "night"

async def generate_voice(mood="auto", text=None):
    if mood == "auto":
        mood = get_time_period()
    
    voice, default_text = VOICE_MAP.get(mood, VOICE_MAP["morning"])
    text = text or default_text
    
    c = Communicate(text, voice)
    await c.save(f"xiaoze_{mood}.mp3")
    print(f"✅ 生成: xiaoze_{mood}.mp3")
    return f"xiaoze_{mood}.mp3"

# 使用
if __name__ == "__main__":
    import sys
    mood = sys.argv[1] if len(sys.argv) > 1 else "auto"
    text = sys.argv[2] if len(sys.argv) > 2 else None
    asyncio.run(generate_voice(mood, text))
```

### 使用方法
```bash
# 自动根据时间生成
python generate_voice.py

# 指定心情
python generate_voice.py happy "你太棒了！"
python generate_voice.py sad "抱抱，没事的"
```

---

*选一个方案开始体验小泽的声音吧！* 🎤💕
