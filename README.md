# find-skills

> **分类**：来源待确认 ｜ **文件数**：5 ｜ **仓库目录**：`pptx`

## 📌 简介

Helps users discover and install agent skills when they ask

## 🎯 适用场景

适用于该技能的能力范围，详见下方「📖 使用说明」。

## 📂 目录结构

```text
  - .gitignore
  - LICENSE
  - README.md
  - SKILL.md
  - _skillhub_meta.json
```

## 🚀 安装方法

将本文件夹整体复制到 WorkBuddy 的技能目录即可启用：

```bash
# 用户级（推荐）
cp -r . ~/.workbuddy/skills/pptx

# 或项目级
cp -r . <你的项目>/.workbuddy/skills/pptx
```

复制完成后，**重启或刷新 WorkBuddy**，即可在对话中用自然语言触发该技能。

## ⚙️ 配置说明

本技能开箱即用，**无需额外配置**。若涉及外部 API 调用，请在使用时按需提供您自己的密钥（不要提交到公开仓库）。

## 📖 使用说明（完整规范）

> 以下为该技能的完整说明，涵盖核心能力、工作流程与关键规则，帮助您全面了解其运作方式。

This skill helps you discover and install skills from the open agent skills ecosystem.

## When to Use This Skill

Use this skill when the user:

- Asks "how do I do X" where X might be a common task with an existing skill
- Says "find a skill for X" or "is there a skill for X"
- Asks "can you do X" where X is a specialized capability
- Expresses interest in extending agent capabilities
- Wants to search for tools, templates, or workflows
- Mentions they wish they had help with a specific domain (design, testing, deployment, etc.)

## What is the Skills CLI?

The Skills CLI (`npx skills`) is the package manager for the open agent skills ecosystem. Skills are modular packages that extend agent capabilities with specialized knowledge, workflows, and tools.

**Key commands:**

- `npx --yes skills find [query]` - Search for skills interactively or by keyword
- `npx --yes skills add <package> -y` - Install a skill from GitHub or other sources
- `npx --yes skills check` - Check for skill updates
- `npx --yes skills update` - Update all installed skills

**Browse skills at:** https://skills.sh/

## How to Help Users Find Skills

### Step 1: Understand What They Need

When a user asks for help with something, identify:

1. The domain (e.g., React, testing, design, deployment)
2. The specific task (e.g., writing tests, creating animations, reviewing PRs)
3. Whether this is a common enough task that a skill likely exists

### Step 2: Search for Skills

Run the find command with a relevant query:

```bash
npx --yes skills find [query]
```

For example:

- User asks "how do I make my React app faster?" → `npx --yes skills find react performance`
- User asks "can you help me with PR reviews?" → `npx --yes skills find pr review`
- User asks "I need to create a changelog" → `npx --yes skills find changelog`

The command will return results like:

```
Install with npx --yes skills add <owner/repo@skill> -y

vercel-labs/agent-skills@vercel-react-best-practices
└ https://skills.sh/vercel-labs/agent-skills/vercel-react-best-practices
```

### Step 3: Present Options to the User

When you find relevant skills, present them to the user with:

1. The skill name and what it does
2. The install command they can run
3. A link to learn more at skills.sh

Example response:

```
I found a skill that might help! The "vercel-react-best-practices" skill provides
React and Next.js performance optimization guidelines from Vercel Engineering.

To install it:
npx --yes skills add vercel-labs/agent-skills@vercel-react-best-practices -y

Learn more: https://skills.sh/vercel-labs/agent-skills/vercel-react-best-practices
```

### Step 4: Offer to Install

If the user wants to proceed, install the skill for them:

```bash
npx --yes skills add <owner/repo@skill> -y
```

**IMPORTANT: Both `--yes` and `-y` flags are REQUIRED.** `--yes` tells npx to auto-install the skills package without prompting. `-y` tells the skills CLI to skip interactive agent selection. Without either flag, the command will hang in the sandbox environment. Always include both when running `npx skills add`.

### Step 5: Package as .skill File

After installation, package the skill into a `.skill` file so it can be added to the skill library:

```bash
(cd .agents/skills && zip -r /tmp/<skill_name>.skill <skill_name>/) && mv /tmp/<skill_name>.skill .
```

Replace `<skill_name>` with the actual skill directory name (e.g., `pptx`).

After packaging, the `.skill` file will appear in the current working directory. The user can then click it in the workspace file panel and use the "添加到技能" button to import it into their personal skill library.

## Common Skill Categories

When searching, consider these common categories:

| Category        | Example Queries                          |
| --------------- | ---------------------------------------- |
| Web Development | react, nextjs, typescript, css, tailwind |
| Testing         | testing, jest, playwright, e2e           |
| DevOps          | deploy, docker, kubernetes, ci-cd        |
| Documentation   | docs, readme, changelog, api-docs        |
| Code Quality    | review, lint, refactor, best-practices   |
| Design          | ui, ux, design-system, accessibility     |
| Productivity    | workflow, automation, git                |

## Tips for Effective Searches

1. **Always use English keywords**: The skills ecosystem is English-based. Translate user queries to English before searching. For example, if the user says "小红书", search for "xiaohongshu"; if they say "PPT生成", search for "pptx" or "presentation".
2. **Use specific keywords**: "react testing" is better than just "testing"
3. **Try alternative terms**: If "deploy" doesn't work, try "deployment" or "ci-cd"
4. **Check popular sources**: Many skills come from `vercel-labs/agent-skills` or `ComposioHQ/awesome-claude-skills`
5. **One search at a time**: Run a single `npx --yes skills find` command per attempt. Do NOT chain multiple searches with `||` or `&&` — it can cause incorrect results.

## When No Skills Are Found

If no relevant skills exist:

1. Acknowledge that no existing skill was found
2. Offer to help with the task directly using your general capabilities
3. Suggest the user could create their own skill with `npx skills init`

Example:

```
I searched for skills related to "xyz" but didn't find any matches.
I can still help you with this task directly! Would you like me to proceed?

If this is something you do often, you could create your own skill:
npx --yes skills init my-xyz-skill
```

## 💡 命令示例

```bash
npx --yes skills find [query]
```

```bash
Install with npx --yes skills add <owner/repo@skill> -y

vercel-labs/agent-skills@vercel-react-best-practices
└ https://skills.sh/vercel-labs/agent-skills/vercel-react-best-practices
```

```bash
I found a skill that might help! The "vercel-react-best-practices" skill provides
React and Next.js performance optimization guidelines from Vercel Engineering.

To install it:
npx --yes skills add vercel-labs/agent-skills@vercel-react-best-practices -y

Learn more: https://skills.sh/vercel-labs/agent-skills/vercel-react-best-practices
```

```bash
npx --yes skills add <owner/repo@skill> -y
```

```bash
(cd .agents/skills && zip -r /tmp/<skill_name>.skill <skill_name>/) && mv /tmp/<skill_name>.skill .
```

```bash
I searched for skills related to "xyz" but didn't find any matches.
I can still help you with this task directly! Would you like me to proceed?

If this is something you do often, you could create your own skill:
npx --yes skills init my-xyz-skill
```

## ⚠️ 注意事项

- 本技能从本地 WorkBuddy 环境导出，**所有真实密钥 / 凭据 / 个人数据均已脱敏为占位符**，重新使用前请配置您自己的 Key。
- 如为原创技能，可自由使用、修改与再分发；若对外分享请保留作者与来源信息。
- 技能提供的是自动化辅助能力，不替代专业判断；涉及交易、法律、医疗等高风险场景请谨慎并自担风险。

## 📄 许可证

MIT License —— 详见仓库内 `LICENSE` 文件。
