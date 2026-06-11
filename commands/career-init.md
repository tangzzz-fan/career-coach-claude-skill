---
description: Initialize the current folder as a Career Coach workspace. Creates `.career-coach/`, local settings, and starter plan documents without moving your existing resume/JD files.
argument-hint: (optional) your macOS username, e.g. "andy" — only needed if different from whoami
---

You are setting up the Career Coach environment for the user. This is a one-time initialization — it is NOT a coaching session. Do NOT invoke the career-coach skill persona. Work directly with Bash, Write, and Read tools.

**Workspace rule**: the current working directory is the user's job-search workspace. Do not write to `~/career-plan/`. Keep all system files inside `.career-coach/`, and leave the user's visible resume/JD files where they already are.

**Your task, in order**:

## Phase 1: Resolve identity and workspace

1. Run `whoami` to get the current macOS username. If $ARGUMENTS is non-empty, use $ARGUMENTS as the username instead.
2. Run `pwd` and store it as `$WORKSPACE`.
3. Print:

```text
🔍 使用用户名: $USER
📁 当前工作区: $WORKSPACE
```

## Phase 2: Survey what already exists

Check each of these paths and report status (exists / missing):
- `.career-coach/workspace.json`
- `.career-coach/tracking/每日状态.md`
- `.career-coach/tracking/漏斗记录表.md`
- `.career-coach/tracking/周复盘记录.md`
- `.career-coach/求职执行计划.md`
- `.career-coach/求职策略与定位.md`
- `.claude/settings.json`

Use `Bash(test -f <path> && echo "EXISTS" || echo "MISSING")` for each.

## Phase 3: Create directories

Create these directories if missing:
- `.career-coach/`
- `.career-coach/tracking/`
- `.career-coach/archive/raw/`
- `.claude/`

Do NOT create `profile/` by default.

## Phase 4: Create workspace marker

If `.career-coach/workspace.json` does not exist, write:

```json
{
  "workspace_version": 1,
  "workspace_root": ".",
  "state_dir": ".career-coach",
  "created_at": "{{TODAY}}",
  "diagnostic_file_patterns": {
    "resumes": ["简历-*.md", "简历-*.pdf", "resume-*.*"],
    "jds": ["JD-*.md", "jd-*.*"],
    "stories": ["项目故事库.md"],
    "feedback": ["面试反馈-*.md"]
  }
}
```

Replace `{{TODAY}}` with today's date from `date +%Y-%m-%d`.

## Phase 5: Write starter documents (only if missing)

Template priority:
1. `/Users/$USER/.claude/skills/career-coach/templates/<name>`
2. `./templates/<name>` (repo-development fallback only; end-user workspaces normally do not have this directory)
3. minimal built-in fallback if template file is unavailable

For each file below: if missing, create it. If it exists, preserve it and mark as `⏭️`.

Write to:
- `.career-coach/tracking/每日状态.md`
- `.career-coach/tracking/漏斗记录表.md`
- `.career-coach/tracking/周复盘记录.md`
- `.career-coach/求职执行计划.md`
- `.career-coach/求职策略与定位.md`

When copying templates, replace `{{TODAY}}` with today's date and leave all other placeholders untouched.

## Phase 6: Bootstrap local Claude settings

Check for a settings example file in this order:
1. `/Users/$USER/.claude/settings.example.json`
2. `./settings.example.json`

If found:
1. Read the file
2. Replace `YOUR_USERNAME` with `$USER`
3. Replace `WORKSPACE_PATH` with the absolute path from Phase 1 `$WORKSPACE`
4. If `.claude/settings.json` does NOT exist, write the substituted JSON to `.claude/settings.json`
5. If `.claude/settings.json` already exists, do NOT overwrite it. Preserve the file and instead print the substituted JSON for manual merge
6. Explain the permissions briefly:
   - `Read($WORKSPACE/**)` — 读取工作区内的简历、JD、面试反馈和系统文件
   - `Write($WORKSPACE/.career-coach/**)` — 只把系统状态写进隐藏目录
   - `Write($WORKSPACE/.claude/**)` — 写入当前工作区的 Claude 设置

If no settings example file is found, tell the user to manually configure permissions per the README and list the required permission entries.

## Phase 7: Final checklist

Print:

```text
═══════════════════════════════════
  Career Coach 工作区初始化完成
═══════════════════════════════════

工作区：
  {✅/⏭️} .career-coach/workspace.json
  {✅/⏭️} .career-coach/tracking/
  {✅/⏭️} .career-coach/archive/raw/
  {✅/⏭️} .claude/settings.json

执行文件：
  {✅/⏭️} .career-coach/tracking/每日状态.md
  {✅/⏭️} .career-coach/tracking/漏斗记录表.md
  {✅/⏭️} .career-coach/tracking/周复盘记录.md

规则文件：
  {✅/⏭️} .career-coach/求职执行计划.md
  {✅/⏭️} .career-coach/求职策略与定位.md

═══════════════════════════════════

📝 下一步（5–10 分钟）：
1. 打开 `.career-coach/求职执行计划.md`，填写你的周指标底线和闸门规则
2. 打开 `.career-coach/求职策略与定位.md`，填写目标岗位、赛道和薪资策略
3. 把你的简历、JD、项目故事库、面试反馈保留在当前工作区可见层
4. 准备就绪后，运行 `/career-checkin` 开始第一天
```

For each file, use ✅ if you created it, ⏭️ if it already existed.

Close with: `开始执行。运行 /career-checkin 进入你的第一天。`

## Guardrails

- NEVER overwrite existing files.
- This is setup, not coaching. Do NOT invoke the career-coach skill persona.
- Do NOT move, rename, or rewrite the user's existing resume/JD files.
- Do NOT create `~/career-plan/`.
- Do NOT create `profile/` by default.
- `archive/` stays empty until `/career-closeout`.
- Keep output concise — the user wants a ready workspace, not a tutorial.

$ARGUMENTS
