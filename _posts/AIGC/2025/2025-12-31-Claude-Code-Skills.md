---
layout: post
title: Claude Code
excerpt: "记录一些关于AI的思考"
modified: 
tags: [LLM, Chatgpt]
comments: true
category: AIGC

---



Claude Code真是太火了，忍不住订阅了 200 刀/月的Pro Max，非常值得。



## Claude Code 项目配置

```
your-project/
├── CLAUDE.md                      # Project memory (alternative location)
├── .mcp.json                      # MCP server configuration (JIRA, GitHub, etc.)
├── .claude/
│   ├── settings.json              # Hooks, environment, permissions
│   ├── settings.local.json        # Personal overrides (gitignored)
│   ├── settings.md                # Human-readable hook documentation
│   ├── .gitignore                 # Ignore local/personal files
│   │
│   ├── agents/                    # Custom AI agents
│   │   └── code-reviewer.md       # Proactive code review agent
│   │
│   ├── commands/                  # Slash commands (/command-name)
│   │   ├── onboard.md             # Deep task exploration
│   │   ├── pr-review.md           # PR review workflow
│   │   └── ...
│   │
│   ├── hooks/                     # Hook scripts
│   │   ├── skill-eval.sh          # Skill matching on prompt submit
│   │   ├── skill-eval.js          # Node.js skill matching engine
│   │   └── skill-rules.json       # Pattern matching configuration
│   │
│   ├── skills/                    # Domain knowledge documents
│   │   ├── README.md              # Skills overview
│   │   ├── testing-patterns/
│   │   │   └── SKILL.md
│   │   ├── graphql-schema/
│   │   │   └── SKILL.md
│   │   └── ...
│   │
│   └── rules/                     # Modular instructions (optional)
│       ├── code-style.md
│       └── security.md
│
└── .github/
    └── workflows/
        ├── pr-claude-code-review.yml           # Auto PR review
        ├── scheduled-claude-code-docs-sync.yml # Monthly docs sync
        ├── scheduled-claude-code-quality.yml   # Weekly quality review
        └── scheduled-claude-code-dependency-audit.yml
```

### 核心组件

**1. CLAUDE.md - 项目记忆** 作为 Claude 的持久记忆，在会话开始时自动加载，包含项目技术栈、关键命令、代码规范和目录结构等信息。

**2. Skills（技能）** 教会 Claude 项目特定模式的 Markdown 文档，包括测试模式、GraphQL 架构、React UI 模式、表单处理等。

**3. Hooks（钩子）** 用于自动化任务，例如在保存时自动格式化代码、在测试文件更改时运行测试、阻止在 main 分支上的编辑等。

**4. Agents（代理）** 专门用途的 AI 助手，如代码审查代理、Git 工作流代理等。

**5. Commands（命令）** 自定义斜杠命令，如 `/onboard`（任务探索）、`/pr-review`（PR 审查）、`/ticket`（JIRA 工单工作流）等。

**6. MCP 服务器** 连接外部工具（JIRA、GitHub、Slack、数据库等），实现"读取工单→实现功能→更新状态"的完整工作流。



## Agent Skills

Agent Skills 是一种轻量级、开放格式，用于通过专门的知识和工作流来扩展 AI 智能体的能力。

从本质上看，一个技能就是一个包含 `SKILL.md` 文件的文件夹。该文件至少包含元数据（`name` 和 `description`）以及指导智能体如何执行某项特定任务的说明。技能还可以捆绑脚本、模板和参考资料。



```perl
my-skill/
├── SKILL.md          # 必需：说明 + 元数据
├── scripts/          # 可选：可执行代码
├── references/       # 可选：文档
└── assets/           # 可选：模板、资源

```

## 技能是如何工作的

技能通过**渐进式披露（progressive disclosure）**来高效管理上下文：

1. **发现（Discovery）**：在启动时，智能体只加载每个可用技能的名称和描述，这些信息刚好足以判断该技能在何时可能相关。
2. **激活（Activation）**：当某个任务与技能的描述相匹配时，智能体会将完整的 `SKILL.md` 指令读入上下文。
3. **执行（Execution）**：智能体按照指令执行任务，并在需要时加载引用的文件或执行捆绑的代码。

这种方式既能保持智能体的高效运行，又能在需要时为其提供更多上下文信息。



## SKILL.md 文件

每个技能都以一个 `SKILL.md` 文件开始，该文件包含 YAML 前置元数据（frontmatter）和 Markdown 指令内容：



```mdx
---
name: pdf-processing
description: 从 PDF 文件中提取文本和表格，填写表单，合并文档。
---

# PDF 处理

## 何时使用该技能
当用户需要处理 PDF 文件时，使用该技能……

## 如何提取文本
1. 使用 pdfplumber 进行文本提取……

## 如何填写表单
……

```

在 `SKILL.md` 文件顶部必须包含以下前置元数据：

- `name`：简短的标识符
- `description`：说明在什么情况下使用该技能

Markdown 正文包含实际的操作说明，对结构或内容没有特定限制。

这种简单的格式具有几个关键优势：

- **自文档化**：技能作者或用户可以直接阅读 `SKILL.md` 来理解其功能，使技能易于审查和改进。
- **可扩展**：技能的复杂度可以从纯文本说明扩展到包含可执行代码、资源和模板。
- **可移植**：技能本质上只是文件，因此易于编辑、版本管理和共享。



## 与Git配合

在Vibe Coding的过程中，经常需要做很多尝试，又不希望影响到主版本的代码，这个时候就可以用 git 来很好的实现。



### 主分支策略

Main (或master)只接受“已验证”的改动，每次开始尝试前，从main拉取一个分支进行实验，实验成功就合并到 main，失败就直接丢弃分支。



```bash
# 新建一个主仓库
git init -b main

# 首次提交：

git add .
git commit -m "Initial commit"


# 创建测试分支
git checkout -b theme-unification

# 满意时合并
git checkout main
git merge theme-unification

# 不满意时删除
git checkout main
git branch -D theme-unification


```



## 市场

1. [Skillsmp](https://skillsmp.com) (已有 7 万多个skills，截止 2026.1.19)



## 教程

1. [Claude Code 免费从入门到精通](https://claudecode.tangshuang.net)

2. [Claude Code Project Configuration Showcase](https://github.com/ChrisWiles/claude-code-showcase)

3. [Claude Code 实战课程（中文）](https://cholf5.com/claude-code-in-action/index.html)