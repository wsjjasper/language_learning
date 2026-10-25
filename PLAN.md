# AI 英语教练方案

在美国做软件工作，工作英语能用但不流利，生活英语和听力要靠猜。用 AI 当教练，三个月内同时提升 **听力、口语流利度、生活化表达**。

**设计原则：每天零摩擦。** 打开 → 语音模式 → 说一个词 → 练 → 关掉。不打字、不复制、不贴字幕。

## 系统怎么运转

```
每天：Claude Project 语音模式，说 "listening" / "speaking" / "life"
      教练按本周计划自动选场景，练完自动在对话里留一张 SESSION CARD（你不用管）

周末：① Project 里说 "weekly cards" → 复制它给的一整块
      ② claude.ai/code 开 session，粘贴，运行 /weekly-review
         → 自动更新错题本、表达库、周报，自动 push
         → 输出新的 coach-memory.md（含下周每天的场景）
      ③ 复制 coach-memory.md，替换 Project 里的旧版本
```

- **Claude Project** = 教练本人。指令在 `coach/project-instructions.md`，知识文件是 `progress/coach-memory.md`（里面有下周计划，所以教练知道今天练什么）。
- **这个 repo** = 总账本。错题、表达、复盘、测量都在这里，用 git 留历史。不需要本地 checkout，也不需要你自己 push。

## 每周节奏（每天 20–30 分钟）

| 日 | 你说 | 内容 |
|---|---|---|
| 周一 | "listening" | AI 演 2–3 段快速多人对话 → 你用嘴复述 → 讲漏听原因 → 跟读 |
| 周二 | "speaking" | 工作场景对练 → 反馈 → 重说更好的版本 |
| 周三 | "listening" | 同周一，换场景 |
| 周四 | "speaking" | 同周二，换场景 |
| 周五 | "life" | small talk / 打电话办事 / 社交，轮换 |
| 周末 | "weekly cards" + `/weekly-review` | 约 10 分钟 |

**真实音频（可选）**：通勤时听 Hard Fork、美剧之类，**只听，不复盘**，不算进每天的 30 分钟。完全没听懂的句子，倒回去看一眼字幕就行（YouTube 或 [Enjoy](https://enjoy.bot)）。

时间不够时的底线：**10 分钟语音对练**。断一天没关系，别断两天。

## 教练规则（已写进 Project 指令）

1. 对话中 **不打断**，结束后给 **3–5 个** 最关键的问题 + 更地道的说法，并让你说一遍。
2. 全英文；俚语、文化梗、语气差异加一句中文解释。
3. 新表达靠 **在对话里反复用** 来记：教练会故意制造情境让你用本周的目标表达，用对 3 次 = 掌握。
4. 每次练完在对话里留一张 SESSION CARD，不读出来，你也不用复制；周末 "weekly cards" 会把它们一次性汇总。

## 错题本与表达库（参考 [m98/fluent](https://github.com/m98/fluent) 的结构）

- `progress/mistakes.md`：按 **错误模式** 归类，记录类别、严重度（🔴 影响理解 / 🟡 不自然 / 🟢 小瑕疵）、次数、例句、状态。
- `progress/expressions.md`：每个表达 0–3 使用计数，3 次用对 = 掌握。
- 全部由 `/weekly-review` 维护，你不用手动编辑。

## 三个月进阶

| 阶段 | 听力 | 口语 | 生活 |
|---|---|---|---|
| 第 1 月 | 正常语速，2 人对话；第 1 周做基线 | standup、1:1、解释自己的工作 | small talk 基本盘：周末、天气、球赛 |
| 第 2 月 | 快语速、3–4 人抢话、吞音连读 | design review、反驳与让步、开会插话 | 打电话办事：约医生、保险、客服 |
| 第 3 月 | 口音（印度、南方、英式）、电话场景 | 即兴讲 trade-off、处理被打断 | 社交：happy hour、美剧梗、开玩笑和接梗 |

## 怎么判断有效（每月一次，说 "baseline"，约 15 分钟）

一次语音 session 就能完成：
1. 固定题目自由说 2 分钟 → 教练从转录里算总词数、每 100 词的填充词数、自我修正次数。
2. 听一段标准难度的 3 人对话，答 5 题（含 2 道语气和言外之意题）。
3. 4 项自评（1–5 分）：开会插话 / 闲聊接梗 / 打电话 / 敢问。

结果由 `/weekly-review` 自动记进 `progress/measurements.md`，和第一次对比。

## 第一次上手（约 15 分钟）

1. 在 Claude App 新建 Project（如 "English Coach"）。
2. 在 GitHub 网页上打开 `coach/project-instructions.md`，复制分隔线以下的内容，贴进 Project 的 **Instructions**。
3. 打开 `progress/coach-memory.md`，复制全文，在 Project 知识库里用 **添加文本内容** 粘贴进去（开始日期可以先留空，第一次复盘时会补上）。
4. 点语音模式，说 **"baseline"**，做第一次测量。
5. 第一个周末先试 "weekly cards"。如果教练说读不到过去的对话，说明你的账号用不了这个功能，就改成每次练完复制一下卡片，存进手机备忘录。

## 推荐真实素材（只听，不复盘）

| 用途 | 素材 |
|---|---|
| 科技圈闲聊、抢话 | Hard Fork（NYT）、Decoder、Lenny's Podcast |
| 生活闲聊、幽默 | Conan O'Brien Needs a Friend、SmartLess |
| 美剧（梗 + 语速） | Silicon Valley、The Office (US)、Brooklyn Nine-Nine |
