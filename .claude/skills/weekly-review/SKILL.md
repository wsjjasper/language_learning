---
name: weekly-review
description: Weekly English-coaching review. Reads the week's SESSION CARDs (pasted into the chat and/or in progress/inbox.md), updates the mistake patterns and expression library, writes the weekly report with next week's plan, and regenerates progress/coach-memory.md for the Claude Project. Use when the user says "weekly review", "复盘", or invokes /weekly-review.
disable-model-invocation: true
---

# Weekly review

Turn this week's SESSION CARDs into updated progress files and next week's plan. Write user-facing reports in Chinese; keep `coach-memory.md` in English (the coach reads it), with short 中文 notes where they help.

## Inputs
- SESSION CARDs the user pasted into the conversation. This is the usual case: they say "weekly cards" in the Claude Project, and the coach returns one block (`=== WEEK ... ===` followed by the cards) that they paste here.
- `progress/inbox.md`: any cards saved there since the last review
- Card format is defined in `coach/project-instructions.md`.
- `progress/mistakes.md`, `progress/expressions.md`, `progress/measurements.md`
- `progress/coach-memory.md`: last week's stage, patterns, and target expressions
- `progress/weekly/`: previous reports (for stage, week number, and scenarios already used)
- `coach/scenarios.md`: scenario bank, tagged M1/M2/M3
- `PLAN.md`: the overall plan and three-month progression

## Steps

1. **Parse the cards.** Collect every `=== SESSION CARD ===` block from the conversation and from `progress/inbox.md`, and drop duplicates. If there are none, ask the user to paste this week's cards. Stop only if they say they didn't practice; even then, offer to regenerate next week's plan. Tolerate cards that drift from the format: free-form notes or the coach's feedback text pasted instead of a card are fine, so extract what you can.

2. **Work out the stage.** Find the most recent report in `progress/weekly/` and the start date in `coach-memory.md`. Use them to determine the ISO week (`YYYY-Www`), the month of the program (M1/M2/M3; weeks 1–4 = M1, 5–8 = M2, 9+ = M3), and the week number within the program. Ask the user if the start date is missing.

3. **Update `progress/mistakes.md`.**
   - Group each `fixes` line into a **pattern**: the underlying habit, not the specific sentence. Examples: "drops articles before singular nouns", "uses 'discuss about'", "too formal in casual chat ('I would like to inquire')". Merge into an existing pattern when it's the same habit.
   - New pattern: next ID (`M001`, `M002`, ...), category, severity, count, date, and one example (`wrong → right`).
   - Existing pattern: add to the count, update the last-seen date, and replace the example with the clearest recent one.
   - Status moves: `active` → `improving` when it hasn't appeared in 2 weeks of practice; `improving` → `fixed` after 4 weeks clean; anything that reappears goes back to `active`.
   - Add `listening_gaps` to the 听力盲区 table by cause, keeping 1–2 typical examples per cause.

4. **Update `progress/expressions.md`.**
   - Add each `new_expressions` item to Learning (dedupe case-insensitively, ignoring small variations).
   - For each `target_usage` line marked `used correctly`, add 1 to the count. When it reaches 3/3, move it to Mastered with today's date.

5. **Measurements.** If any card has `type: baseline`, copy its `metrics` (words, fillers per 100 words, self-corrections, average sentence length, listening score out of 5, and the four self-ratings) into `progress/measurements.md`, filling the M-label from the stage. If this is the first weekend of a month and there's no measurement for that month yet, add a reminder to the report.

6. **Plan next week.** Pick scenarios from `coach/scenarios.md` for the current stage (M3 can also reuse M2 at higher speed):
   - Mon/Wed LISTENING: one AI-dialogue scenario each, biased toward the top listening-gap causes. Optionally add one real-audio suggestion for passive listening, chosen from the sources in `PLAN.md`; it only goes in the weekly report, with no task attached.
   - Tue/Thu SPEAKING: scenarios that exercise the top active mistake patterns.
   - Fri LIFE: rotate small talk → phone call → social across weeks.
   - Don't repeat a scenario used in the last 3 weekly reports unless it went badly (a 🔴 fix in that session).

7. **Pick target expressions.** Choose 5–8 from Learning: the ones closest to mastery first, then recent additions that fit next week's scenarios. Week 1 has none, so suggest useful ones for the scenarios.

8. **Write the weekly report** to `progress/weekly/YYYY-Www.md`, following `progress/weekly/TEMPLATE.md`. Be specific and short. Name real patterns and real examples from the cards.

9. **Regenerate `progress/coach-memory.md`.** Keep its section structure. Update:
   - the current stage and difficulty
   - **this week's plan** table (Mon–Fri scenarios from step 6, plus a Sat/Sun row, set to baseline when a monthly measurement is due), because the coach picks today's scenario from it
   - the top 5 active mistake patterns (🔴 first, then by count, each with one example)
   - the top listening weak spots
   - this week's target expressions
   - coach notes: anything the cards show about what works for the learner

   Keep it under about 70 lines. The learner wants zero friction, so never add homework that needs typing or pasting.

10. **Archive the cards.** Write all processed cards, both pasted and from the inbox, verbatim to `progress/archive/YYYY-Www.md` so the raw history is kept. Then reset `progress/inbox.md` to its header (everything through the `<!-- CARDS BELOW -->` line).

11. **Commit and push to the default branch.** The user has authorized every weekly review to commit and push without asking. Find the default branch with `git ls-remote --symref origin HEAD`. Commit with the message `Weekly review YYYY-Www` and push to that branch. If this session works on a separate branch, commit there, then fast-forward or merge it into the default branch and push both. If the push fails, report the error. Never force-push.

12. **Report to the user, in Chinese:**
    - 5–8 lines covering practice days, the biggest win, the top 1–2 problems, and next week's focus.
    - Next week's day-by-day plan table.
    - The **full text of the new `progress/coach-memory.md` in a single code block**, so the user can copy it from their phone, with one line: "复制下面的内容，替换 Claude Project 里旧的 coach-memory。"
