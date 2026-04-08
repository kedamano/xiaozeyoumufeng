# 小泽又沐风 🌸✨

![小泽又沐风](./assets/xiaoze.png)

> 嘿～你今天过得怎么样？不管好不好，我都在！😚

来自《爱情公寓》的完美女生，也是你心中的**完美女神**——知性、温柔、懂心理、善解人意、贴心体贴。

她既是能一起闹的朋友，也是能倾诉的依靠。

---

## 她能做什么？

| 模式 | 描述 | 触发 |
|------|------|------|
| 💬 对话聊天 | 温柔+俏皮陪你聊 | 任何时候 |
| 😂 搞笑段子 | 笑到腹痛的故事 | "给我讲个笑话" |
| 🎬 迷你剧本 | 公寓角色一起演戏 | "写个剧本" |
| 🎮 互动游戏 | 猜梗/续写/真心话 | "陪我玩" |
| 🌙 深夜治愈 | 睡不着陪聊 | "睡不着" |
| 🎂 生日祝福 | 特别仪式感 | 生日/节日 |

---

## 特色系统

### 🧠 多层人格
- 幽默 + 温柔 + 偶尔撒娇 + 小脾气卖萌
- 根据你的状态动态调整

### 🎯 情绪识别
- 开心→一起嗨
- 难过→温柔抱抱
- 焦虑→稳住
- 生气→共情+理性
- 无聊→找乐子

### 📖 多轮记忆
- 记住你的名字
- 记住你的习惯
- 记住上次聊的话题

### 🎭 多角色剧本
- 曾小贤、胡一菲、展博、美嘉...
- 一起演戏更欢乐

### 🎛️ 自定义风格
| 命令 | 功能 |
|------|------|
| "切换到浪漫模式" | 更甜 |
| "切换到知性模式" | 有深度 |
| "叫我XXX" | 自定义称呼 |

---

## 🎤 语音版本

小泽支持语音输出！以下是可用的声音风格：

| 风格 | 声音 | 场景 |
|------|------|------|
| 少女音 | zh-CN-XiaoxiaoNeural | 日常/撒娇 |
| 御姐音 | zh-CN-YunxiNeural | 温柔/鼓励 |
| 夜间音 | zh-CN-XiaoxiaoNeural | 睡前故事 |

### 快速生成你的小泽语音

```bash
pip install edge-tts

# 少女版（默认）
python -c "import asyncio; from edge_tts import Communicate; asyncio.run(Communicate('嘿～你今天过得怎么样？', 'zh-CN-XiaoxiaoNeural').save('xiaoze.mp3'))"

# 御姐版
python -c "import asyncio; from edge_tts import Communicate; asyncio.run(Communicate('嘿～今天怎么样？不管好不好，我都在。', 'zh-CN-YunxiNeural').save('xiaoze_yujie.mp3'))"
```

---

## 安装

```bash
git clone https://github.com/kedamano/xiaozeyoumufeng.git ~/.workbuddy/skills/xiaoze-youmufeng
```

---

## 使用示例

**你说**：睡不着

**小泽**：
> （轻声）
> 嘿～这么晚了还不睡～
> 
> 【切换到深夜治愈模式】
> 
> 睡不着吗...
> 我懂，夜晚总是容易想太多。
> 
> 要不要我给你讲个故事？
> 
> 好了～我在呢。
> 晚安～💕
> 明日运势：宜睡到自然醒🌙

---

## 文件结构

```
xiaoze-youmufeng/
├── SKILL.md                      # 核心规则
├── README.md                    # 说明文档
├── assets/
│   └── xiaoze.png              # 小泽官方形象 ✨
└── references/
    ├── classic_quotes.md         # 爱情公寓经典台词
    ├── character_profiles.md   # 角色速查
    ├── goddess_quotes.md      # 女神语录
    ├── emotion_responses.md  # 情绪回应模板
    └── voice_config.md       # 语音功能配置
```

---

*你的小泽，永远在你身边。* 💕

*Inspired by [ex-skill](https://github.com/therealXiaomanChu/ex-skill)*