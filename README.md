# Career Coach

> 一个全局安装、局部运行的 Claude Code 求职教练 skill。
> 把 skill 安装到 `~/.claude`，然后在任意一个求职资料文件夹中打开 Claude Code，即可把当前文件夹升级为可执行的求职工作区。

## 快速开始

### 1. 进入你的求职资料文件夹

在任意一个放了简历、JD、面试反馈的文件夹中打开 Claude Code。文件夹可以是这个样子：

```text
我的求职资料/
├── 我的简历.md          # 随便叫什么
├── JD-01-字节.md
├── JD-02-腾讯.md
├── 项目故事库.md
├── 面试反馈-01.md
└── (其他文件也完全没关系)
```

### 2. 安装 skill

在 Claude Code 对话中输入：

```bash
/claude add-skill https://github.com/tangzzz-fan/career-coach-claude-skill.git
```

> **没有发布地址？** 可以先从本地仓库安装。克隆本仓库后，在仓库目录中打开 Claude Code，然后参考 [working-mechanism.md](docs/working-mechanism.md) 的开发安装步骤。

### 3. 运行初始化

```bash
/career-init
```

初始化后，当前文件夹会新增两样东西：

```text
我的求职资料/
├── .claude/
│   └── settings.json              # 自动写入权限配置
└── .career-coach/
    ├── workspace.json              # 工作区标记
    ├── 求职执行计划.md             # 🔧 需要你填写
    ├── 求职策略与定位.md           # 🔧 需要你填写
    ├── tracking/
    │   ├── 每日状态.md
    │   ├── 漏斗记录表.md
    │   └── 周复盘记录.md
    └── archive/
        └── raw/
```

**你的简历、JD、故事库、面试反馈不会被移动，也不会被改名。**

### 4. 填写两份规则文件（5–10 分钟）

打开 `.career-coach/` 下的这两份文件，把 `🔧` 标记的地方换成你的数字：

- `.career-coach/求职执行计划.md` — 周指标底线、闸门触发条件
- `.career-coach/求职策略与定位.md` — 目标岗位、赛道、薪资策略

### 5. 开始使用

```bash
/career-checkin
/career-record Boss直聘 某科技公司 iOS开发工程师 已投递 主赛道版简历
/career-checkout 投递22 回复3 约面0
/career-review
/career-diagnose 帮我对比简历和JD-01-字节的匹配度
/career-decide 要不要接受目前唯一的offer还是继续面
/career-closeout 接受了字节iOS 35K
```

## 这个 skill 做什么

### 执行层
- `/career-checkin`：晨间启动，锁定今天三件事
- `/career-record`：快速记一次投递/回复/约面事件
- `/career-checkout`：晚间复盘，记录数字与明日微调
- `/career-review`：周六看趋势、看闸门、定下周唯一调整项
- `/career-decide`：结构化做求职决策，不替你做决定

### 诊断层
- `/career-diagnose`：按需分析简历、JD、项目故事、面试反馈

### 收官层
- `/career-closeout`：在求职结束后生成总结报告、职业资产包、决策规则清单和下一阶段建议

## 深入说明

如果你想看这套 skill 的作用机制、执行流程、文件职责和追踪/诊断边界，查看 [working-mechanism.md](docs/working-mechanism.md)。

## 路径原则

- `~/.claude/`：只放全局 skill 和命令
- `当前打开的资料文件夹`：就是工作区根目录
- `.career-coach/`：只放系统状态、规则和输出资产
- `工作区可见层`：放用户自己的简历、JD、项目故事、面试反馈

## 不会发生什么

- 不会默认创建 `~/career-plan`
- 不会把你的简历/JD 自动搬走
- 不会把状态文件写到工作区外面
- 不会在日常执行模式里自动读取你的简历全文

## 文件命名

**你不需要改名。** 诊断模式会自动扫描工作区中的文件，通过内容特征判断每个文件是简历、JD、故事库还是面试反馈。首次诊断时会把识别结果写入 `.career-coach/workspace.json`，后续直接复用。

不过，如果你的文件恰好叫下面这样，匹配会更快：

```text
简历-主赛道.md
简历-第二赛道.md
JD-01-字节.md
JD-02-腾讯.md
项目故事库.md
面试反馈-01.md
面试反馈-02.md
```

## 平台范围

| 平台 | 兼容性 | 说明 |
|------|--------|------|
| Claude Code CLI | 原生支持 | 当前仓库的目标平台 |
| Claude Desktop | 不兼容 | skill 机制和文件访问模型不同 |
| Cursor IDE | 不兼容 | `.mdc` / rules 体系不同 |

## 说明

这是一个“全局安装、局部工作区运行”的 skill：
- 你只安装一次
- 你可以在任意一个求职资料文件夹中重复使用
- 每个文件夹都有自己独立的 `.career-coach/` 状态，不互相污染
