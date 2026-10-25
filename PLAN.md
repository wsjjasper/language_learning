# AI 英语教练方案

在美国做软件工作，工作英语能用但不流利，生活英语和听力要靠猜。用 AI 当教练，三个月内同时提升 **听力、口语流利度、生活化表达**。

## 系统怎么运转

```
手机 Claude Project（语音对练）         浏览器 Enjoy（真实素材听力）
        │  每次练完输出一张 SESSION CARD        │  听完也让 Claude 出卡片
        └──────────────┬───────────────────────┘
                       ▼
            progress/inbox.md（复制粘贴，<1 分钟）
                       │  周末 /weekly-review（Claude Code）
                       ▼
   mistakes.md · expressions.md · weekly/YYYY-Www.md
                       │
                       ▼
     coach-memory.md ──上传──► Claude Project（教练记得你的弱点和本周目标）
```

- **Claude Project** = 教练本人。指令在 `coach/project-instructions.md`，知识文件是 `progress/coach-memory.md`。
- **这个 repo** = 总账本。错题、表达、复盘、测量都在这里，用 git 留历史。
- **Enjoy**（[enjoy.bot](https://enjoy.bot) / Chrome 插件，开源项目 [everyone-can-use-english](https://github.com/ZuodaoTech/everyone-can-use-english)）= 真实素材的逐句精听、听写、跟读工具。

## 每周节奏（每天 30 分钟）

| 日 | 内容 | 提示词 |
|---|---|---|
| 周一 | 听力：AI 生成的快速多人对话（15 min）+ Enjoy 真实素材精听（15 min） | `coach/prompts/listening.md` |
| 周二 | 口语：工作场景语音对练 | `coach/prompts/speaking.md` |
| 周三 | 听力：同周一，换场景 / 换素材 | `coach/prompts/listening.md` |
| 周四 | 口语：工作场景语音对练 | `coach/prompts/speaking.md` |
| 周五 | 生活场景角色扮演（small talk / 打电话办事 / 社交） | `coach/prompts/life.md` |
| 周末 | 30 分钟复盘：Claude Code 里跑 `/weekly-review` | `.claude/skills/weekly-review` |

具体场景每周由 `/weekly-review` 从 `coach/scenarios.md` 里挑，写进当周复盘的「下周计划」。

时间不够时的底线：**只做 10 分钟语音对练 + 出卡片**。断一天没关系，别断两天。

## 教练规则（已写进 Project 指令）

1. 对话中 **不打断**，结束后给 **3–5 个** 最关键的问题 + 更地道的说法。
2. 全英文；俚语、文化梗、语气差异加一句中文解释。
3. 每次结束输出固定格式的 **SESSION CARD**，你复制到 `progress/inbox.md`。
4. 新表达靠 **在对话里反复用** 来记：教练会故意制造情境让你用本周的目标表达，用对 3 次 = 掌握。

## 错题本与表达库（参考 [m98/fluent](https://github.com/m98/fluent) 的结构）

- `progress/mistakes.md`：按 **错误模式** 归类，不是逐条罗列。每个模式记录类别、严重度（🔴 影响理解 / 🟡 听起来不自然 / 🟢 小瑕疵）、出现次数、最近例句、状态。
- `progress/expressions.md`：每个表达有 0–3 的使用计数，3 次用对即标记掌握。
- 不用 Anki/SM-2，复习发生在对话里。

## 三个月进阶

| 阶段 | 听力 | 口语 | 生活 |
|---|---|---|---|
| 第 1 月 | 正常语速，2 人对话；第 1 周做基线 | standup、1:1、解释自己的工作 | small talk 基本盘：周末、天气、球赛 |
| 第 2 月 | 快语速、3–4 人抢话、吞音连读 | design review、反驳与让步、开会插话 | 打电话办事：约医生、保险、客服 |
| 第 3 月 | 口音（印度、南方、英式）、电话音质类内容 | 即兴讲解 trade-off、处理被打断 | 社交：happy hour、美剧梗、开玩笑和接梗 |

## 怎么判断有效（每月一次，`coach/prompts/baseline.md`）

1. **口语**：录 2 分钟自由口语（固定题目轮换）→ 转文字 → 算 WPM、填充词（um/uh/like）数、自我修正次数。
2. **听力**：同一档 podcast 新一期的 3 分钟片段，不看字幕复述要点 → 对照文稿估算理解率。
3. **主观自评**（1–5 分）：开会能主动插话 / 闲聊能接住梗 / 打电话不慌 / 听不懂时敢问。

结果记在 `progress/measurements.md`，和第 1 周的基线对比。

## 第一次上手（约 20 分钟）

1. 在 Claude App 新建 Project，名字随意（如 "English Coach"）。
2. 把 `coach/project-instructions.md` 的全文贴进 Project 的 **Instructions**。
3. 把 `progress/coach-memory.md` 上传为 Project **知识文件**。
4. 本周第一天做 `coach/prompts/baseline.md` 的基线测试，卡片贴进 `progress/inbox.md`。
5. 之后按上面的周表练。每周跑完 `/weekly-review` 后，**用新的 `coach-memory.md` 替换 Project 里的旧文件**。

## 推荐真实素材

| 用途 | 素材 |
|---|---|
| 科技圈闲聊、抢话 | Hard Fork（NYT）、Decoder、Lenny's Podcast（YouTube 有字幕） |
| 工作会议氛围 | YouTube 搜 "engineering standup recording" / "sprint planning example" / 公司公开的 all-hands |
| 生活闲聊、幽默 | Conan O'Brien Needs a Friend、SmartLess、Late night 节目片段 |
| 美剧（梗 + 语速） | Silicon Valley、The Office (US)、Brooklyn Nine-Nine |
| 打电话 / 服务场景 | YouTube 搜 "customer service call example" / "calling doctor's office English" |

YouTube 视频可以直接在 Enjoy 的 Chrome 插件里逐句精听、跟读。
