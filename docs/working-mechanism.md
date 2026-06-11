# Career Coach 作用机制

## 定位

Career Coach 不是通用聊天提示词，而是一套运行在 Claude Code 中的求职工作流：

- **全局安装**：skill 与 commands 安装在 `~/.claude/`
- **局部运行**：用户当前打开的简历 / JD 文件夹就是工作区
- **本地持久化**：所有系统状态写入当前工作区下的 `.career-coach/`
- **用户资料保留原位**：简历、JD、项目故事、面试反馈保留在工作区可见层

核心目标不是“陪聊”，而是让用户在求职周期内形成稳定执行节奏，并在结束后沉淀为可复用职业资产。

## 工作区模型

### 分层结构

```text
工作区根目录/
├── 简历-主赛道.md
├── JD-01-字节.md
├── 项目故事库.md
├── 面试反馈-01.md
├── .claude/
│   └── settings.json
└── .career-coach/
    ├── workspace.json
    ├── 求职执行计划.md
    ├── 求职策略与定位.md
    ├── tracking/
    │   ├── 每日状态.md
    │   ├── 漏斗记录表.md
    │   └── 周复盘记录.md
    └── archive/
        └── raw/
```

### 设计原则

- **全局能力，本地状态**：skill 只安装一次，但每个工作区各自独立
- **最小路径侵入**：不创建 `~/career-plan`，也不把用户资料迁走
- **状态隐藏，资料可见**：系统状态进入 `.career-coach/`，用户内容仍在可见层

## 三层能力

### 1. 执行层

负责日常推进，不做内容评估。

命令：
- `/career-checkin`
- `/career-record`
- `/career-checkout`
- `/career-review`
- `/career-decide`

输入：
- `.career-coach/tracking/*`
- `.career-coach/求职执行计划.md`
- `.career-coach/求职策略与定位.md`

输出：
- 今日三件事
- 本周漏斗进度
- 闸门触发提醒
- 下周第一调整项

### 2. 诊断层

负责分析“为什么转化低”，只在按需时读取用户资料。

命令：
- `/career-diagnose`

输入：
- `简历-*.md`
- `JD-*.md`
- `项目故事库.md`
- `面试反馈-*.md`
- `.career-coach/tracking/漏斗记录表.md`

输出：
- 内容缺口
- 匹配偏差
- 本周只改一项的建议

### 3. 收官层

负责把一次求职过程压缩为可复用资产。

命令：
- `/career-closeout`

输出到：
- `.career-coach/archive/求职总结报告.md`
- `.career-coach/archive/职业资产包.md`
- `.career-coach/archive/决策规则清单.md`
- `.career-coach/archive/下一阶段发展建议.md`

## 执行流程

### 首次初始化

```mermaid
flowchart LR
    A[全局安装 skill] --> B[进入简历/JD 文件夹]
    B --> C[/career-init]
    C --> D[生成 .career-coach/]
    C --> E[生成本地 .claude/settings.json]
    D --> F[填写两份规则文档]
    E --> F
    F --> G[/career-checkin 开始使用]
```

### 日常循环

```mermaid
flowchart LR
    A[/career-checkin] --> B[/career-record]
    B --> C[/career-checkout]
    C --> D[/career-review]
    D --> E{内容异常?}
    E -->|否| A
    E -->|是| F[/career-diagnose]
    F --> A
```

### 收官流程

```mermaid
flowchart LR
    A[tracking 数据] --> D[/career-closeout]
    B[规则文档] --> D
    C[简历/JD/面试反馈] --> D
    D --> E[求职总结报告]
    D --> F[职业资产包]
    D --> G[决策规则清单]
    D --> H[下一阶段发展建议]
```

## 文件职责

| 文件 | 谁维护 | 作用 | 何时读取 |
|------|--------|------|----------|
| `.career-coach/求职执行计划.md` | 用户 | 铁律、指标底线、阶段清单、闸门 | 执行层、决策层、收官层 |
| `.career-coach/求职策略与定位.md` | 用户 | 赛道、关键词、城市、薪资、简历版本策略 | 执行层、决策层、收官层 |
| `.career-coach/tracking/每日状态.md` | skill | 今日三件事、连续执行天数、闸门状态 | 签到、签退、周复盘 |
| `.career-coach/tracking/漏斗记录表.md` | skill | 投递/回复/约面/面试的唯一事实来源 | 记录、复盘、诊断、收官 |
| `.career-coach/tracking/周复盘记录.md` | skill | 周趋势、异常信号、下周调整项 | 周复盘、收官 |
| `简历-*.md` | 用户 | 简历多版本 | 诊断、收官 |
| `JD-*.md` | 用户 | 目标岗位要求 | 诊断、收官 |
| `项目故事库.md` | 用户 | 面试故事素材 | 诊断、收官 |
| `面试反馈-*.md` | 用户 | 面试中的真实反馈 | 诊断、收官 |

## 追踪与诊断边界

### 追踪

- 目标：让用户持续执行
- 关注：投递数、回复数、约面数、周趋势、闸门
- 特征：不主动读取简历全文

### 诊断

- 目标：让用户跑得更准
- 关注：简历匹配度、故事质量、面试卡点、JD 对齐情况
- 特征：不写回 tracking，不改闸门规则

### 边界规则

- 日常模式绝不自动进入诊断
- 周复盘只暴露“是否需要诊断”的信号
- 诊断结果只能形成建议，不能覆盖预先承诺规则

## 为什么这样设计

### 1. 减少路径侵入

- 用户的资料文件夹本来就存在
- skill 只在当前目录下新增 `.career-coach/`
- 不把状态散落到 home 目录

### 2. 保持产品边界

- 执行层解决“知而不行”
- 诊断层解决“行而不准”
- 两者分离可以防止日常对话被内容分析拖重

### 3. 支持长期资产沉淀

求职结束后，系统不只留下日志，而是沉淀出：

- 决策规则
- 职业叙事素材
- 机会转化经验
- 下一阶段发展建议

## 相关阅读

- [README](file:///Users/apple/Desktop/career-coach-claude-skill/README.md)
- [SKILL.md](file:///Users/apple/Desktop/career-coach-claude-skill/skills/career-coach/SKILL.md)
