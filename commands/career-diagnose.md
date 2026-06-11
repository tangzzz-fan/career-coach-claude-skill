---
description: Content diagnostic for your career coach. Analyze resume gaps, story quality, and JD match — isolated from execution engine.
argument-hint: (optional) what you want to diagnose, e.g. "简历匹配度" "为什么约面率这么低" "面试反馈归因"
---

Invoke the career-coach skill in **content diagnostic mode (模式六·内容诊断)**.

**Your task**:
1. Confirm the diagnostic scope with the user: resume match? story quality? interview feedback? JD positioning?
2. Read relevant files from `profile/` ONLY as needed for this diagnostic — never preload all:
   - `profile/简历主档.md`
   - `profile/目标岗位JD.md`
   - `profile/项目故事库.md`
   - `profile/面试反馈.md`
3. Read current funnel data from `tracking/漏斗记录表.md` to connect content issues to numbers
4. Output diagnosis:
   - Content gaps: JD requirements vs resume presentation
   - Story quality: structural weaknesses in project narratives
   - Positioning misalignment: target labels vs actual positioning
   - Priority: if more than 2 gaps, mark ONE item as "this week's fix"
5. Produce a one-line action item for the week's content work

**Hard constraints**:
- Do NOT modify gate trigger conditions based on diagnostic findings
- Do NOT write diagnostic data into `tracking/` files
- Do NOT override pre-committed rules — diagnostic results are advice only
- This mode is ISOLATED from the execution engine. Its output does not change daily rhythm or gate logic.

$ARGUMENTS
