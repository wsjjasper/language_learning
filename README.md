# language_learning

用 Claude 当英语教练：手机上做语音对练，这个 repo 记录错题、表达和进度。完整方案见 [PLAN.md](PLAN.md)。

```
PLAN.md                          方案总览：节奏、规则、三个月进阶、测量方法
coach/
  project-instructions.md        粘贴到 Claude Project 的教练指令
  scenarios.md                   场景库（M1/M2/M3）
  prompts/                       每天的开场提示词：listening / speaking / life / baseline
progress/
  inbox.md                       每次练完把 SESSION CARD 粘到这里
  coach-memory.md                上传到 Claude Project 的知识文件（每周更新）
  mistakes.md                    错误模式本
  expressions.md                 表达库（用对 3 次 = 掌握）
  measurements.md                月度测量
  weekly/                        每周复盘报告
.claude/skills/weekly-review/    周末在 Claude Code 里跑 /weekly-review
```

## 每天
打开对应的 `coach/prompts/*.md`，照着练 → 把 SESSION CARD 粘进 `progress/inbox.md`。

## 每周末
在 Claude Code 里运行 `/weekly-review` → 把新的 `progress/coach-memory.md` 替换到 Claude Project。
