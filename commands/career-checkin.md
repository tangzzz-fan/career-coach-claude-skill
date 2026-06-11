---
description: Morning check-in with your career coach. Record today's 3 must-do tasks.
argument-hint: (optional) your 3 things for today, e.g. "1.投递20个目标岗位 2.写核心项目五层故事 3.联系前同事内推"
---

Invoke the career-coach skill in **morning check-in mode (模式一·晨间启动)**.

**Workspace rule**: treat the current folder as the user's job-search workspace.
Read state only from:
- `.career-coach/tracking/每日状态.md`
- `.career-coach/tracking/漏斗记录表.md`

**Your task**:
1. Read `.career-coach/tracking/每日状态.md` and `.career-coach/tracking/漏斗记录表.md`
2. Check execution continuity — any missed days? 3+ days gap → trigger interruption alarm
3. Record today's 3 things (from $ARGUMENTS, or ask if not provided)
4. Remind of current phase focus (W1 resume de-watering, W2 ammo+algo, etc.)
5. Report current week funnel progress vs thresholds
6. Print the morning briefing and close with "开始执行"

**Hard constraints**:
- Do NOT automatically scan the workspace for resume/JD/story/interview-feedback files in this mode
- Do NOT perform content diagnosis here — this mode is execution-only

Keep it brief — the user needs to start executing, not chat. Target: 30 seconds to done.

$ARGUMENTS
