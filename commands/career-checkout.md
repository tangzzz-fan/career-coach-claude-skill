---
description: Evening check-out. Record today's funnel numbers and one adjustment for tomorrow.
argument-hint: (optional) funnel numbers: 投递X 回复Y 约面Z
---

Invoke the career-coach skill in **evening check-out mode (模式二·晚间复盘)**.

**Workspace rule**: treat the current folder as the user's job-search workspace.
Update state only inside `.career-coach/`.

**Your task**:
1. Collect today's funnel numbers from $ARGUMENTS (or ask)
2. Check today's 3 things — mark each ✅ or ❌
3. Update `.career-coach/tracking/漏斗记录表.md` and `.career-coach/tracking/每日状态.md`
4. Compare week-to-date against 5 weekly thresholds; flag ⚠️ or ❌
5. Remind: 铁律3 — no strategy change from a single bad day
6. Ask: "明天要调整的一件事？" and write it to 每日状态
7. If any metric has already fallen below threshold and only 1-2 days remain this week, compute the exact catch-up number and tell the user what tomorrow's minimum needs to be

**Hard constraints**:
- Do NOT automatically scan the workspace for resume/JD/story/interview-feedback files in this mode
- Do NOT perform content diagnosis here — this mode is execution-only

Keep it tight. Target: 2 minutes.

$ARGUMENTS
