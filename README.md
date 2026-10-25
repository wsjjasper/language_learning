# language_learning

用 Claude 当英语教练：手机上语音对练，这个 repo 记录错题、表达和进度。完整方案见 [PLAN.md](PLAN.md)。

## 每天
Claude Project → 语音模式 → 说 **"listening"** / **"speaking"** / **"life"** → 练完关掉。什么都不用复制。

## 每周末
1. 在 Project 里说 **"weekly cards"**，复制它给的那一整块。
2. 在 claude.ai/code 用这个 repo 开 session，粘贴，运行 `/weekly-review`。它会自动更新并 push。
3. 复制它输出的 `coach-memory.md` 全文，替换 Project 里的旧版本。

## 文件

```
PLAN.md                          方案总览
coach/
  project-instructions.md        粘贴到 Claude Project 的教练指令
  scenarios.md                   场景库（M1/M2/M3），复盘时从这里排下周计划
  prompts/                       各类练习的说明：listening / speaking / life / baseline
progress/
  coach-memory.md                放进 Claude Project 的知识（含本周计划，每周更新）
  mistakes.md                    错误模式本
  expressions.md                 表达库（用对 3 次 = 掌握）
  measurements.md                月度测量
  weekly/                        每周复盘报告
  archive/                       每周原始卡片
  inbox.md                       可选：也可以把卡片存在这里
.claude/skills/weekly-review/    /weekly-review
```
