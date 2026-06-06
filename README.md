# ⚡ Everything Claude Code

> A curated, battle-tested toolkit for Claude Code — agents, skills, hooks, slash commands, rules, and MCP integrations you can drop straight into `~/.claude/`.

**English | [中文](#中文)**

[![Last commit](https://img.shields.io/github/last-commit/shengdabai/everything-claude-code)](https://github.com/shengdabai/everything-claude-code/commits)
[![Stars](https://img.shields.io/github/stars/shengdabai/everything-claude-code?style=social)](https://github.com/shengdabai/everything-claude-code/stargazers)
[![Follow @shengdabai](https://img.shields.io/github/followers/shengdabai?style=social)](https://github.com/shengdabai)

Stop re-inventing your Claude Code setup. This repo is a ready-to-install collection of **9 specialized agents, 11 skills, 15 slash commands, 8 rules, 6-event hooks, and 15 MCP server configs** — packaged as a single Claude Code plugin or copyable, à-la-carte parts.

---

## Why this exists

Most Claude Code setups start from scratch every time: the same agents, the same hooks, the same `console.log` guard, re-written by hand in every repo. This toolkit collects a coherent, opinionated baseline so you can install once and start working at full speed — then keep or delete whatever doesn't fit your stack.

It installs as a **Claude Code plugin** (one command) or you can cherry-pick individual `.md` files into `~/.claude/`. Everything is plain Markdown + Node.js, cross-platform on **Windows, macOS, and Linux**.

## ✨ What's inside

| Category | Count | What you get |
|----------|-------|--------------|
| 🤖 **Agents** | 9 | Specialized subagents for delegation — planner, architect, code-reviewer, security-reviewer, tdd-guide, build-error-resolver, e2e-runner, refactor-cleaner, doc-updater |
| 🧠 **Skills** | 11 | Workflow + domain knowledge — coding-standards, backend-patterns, frontend-patterns, tdd-workflow, security-review, eval-harness, verification-loop, continuous-learning, strategic-compact, project-guidelines |
| ⚡ **Commands** | 15 | Slash commands — `/tdd`, `/plan`, `/e2e`, `/code-review`, `/build-fix`, `/refactor-clean`, `/learn`, `/checkpoint`, `/verify`, `/orchestrate`, `/test-coverage`, `/update-docs`, `/update-codemaps`, `/eval`, `/setup-pm` |
| 📏 **Rules** | 8 | Always-follow guidelines — security, coding-style, testing, git-workflow, agents, hooks, patterns, performance |
| 🪝 **Hooks** | 6 events | Trigger-based automations across `PreToolUse`, `PostToolUse`, `Stop`, `SessionStart`, `SessionEnd`, `PreCompact` — memory persistence + strategic compaction |
| 🧩 **Contexts** | 3 | Dynamic system-prompt injection modes — dev, review, research |
| 🔌 **MCP configs** | 15 | Ready-to-paste server configs — GitHub, Supabase, Vercel, Railway, Firecrawl, ClickHouse, Context7, Magic, Filesystem, Memory, Sequential-Thinking, and the Cloudflare suite |

Plus a Node.js **test suite**, cross-platform **package-manager detection** (npm / pnpm / yarn / bun), and example `CLAUDE.md` configs at both project and user level.

## 🧱 How it's organized

```
everything-claude-code/
├── .claude-plugin/   # plugin.json + marketplace.json (install as a plugin)
├── agents/           # 9 specialized subagents
├── skills/           # 11 workflow / domain-knowledge skills
├── commands/         # 15 slash commands
├── rules/            # 8 always-follow guideline files
├── hooks/            # hooks.json + memory-persistence + strategic-compact
├── contexts/         # 3 dynamic system-prompt modes (dev / review / research)
├── mcp-configs/      # 15 MCP server configurations
├── scripts/          # cross-platform Node.js hook implementations + PM setup
├── tests/            # Node.js test suite (node tests/run-all.js)
└── examples/         # example project- and user-level CLAUDE.md
```

## 🚀 How to use

### Option 1 — Install as a plugin (recommended)

```bash
# Add this repo as a marketplace, then install the plugin
/plugin marketplace add shengdabai/everything-claude-code
/plugin install everything-claude-code@everything-claude-code
```

Or wire it into `~/.claude/settings.json` directly:

```json
{
  "extraKnownMarketplaces": {
    "everything-claude-code": {
      "source": { "source": "github", "repo": "shengdabai/everything-claude-code" }
    }
  },
  "enabledPlugins": {
    "everything-claude-code@everything-claude-code": true
  }
}
```

### Option 2 — Cherry-pick parts manually

```bash
git clone https://github.com/shengdabai/everything-claude-code.git

cp everything-claude-code/agents/*.md   ~/.claude/agents/
cp everything-claude-code/commands/*.md ~/.claude/commands/
cp everything-claude-code/rules/*.md    ~/.claude/rules/
cp -r everything-claude-code/skills/*   ~/.claude/skills/
```

Then merge `hooks/hooks.json` into `~/.claude/settings.json`, and copy the MCP servers you want from `mcp-configs/mcp-servers.json` into `~/.claude.json`.
**Important:** replace every `YOUR_*_HERE` placeholder with your own API keys before use.

### Run the tests

```bash
node tests/run-all.js
```

## 📖 Highlights

- **Memory persistence** — `SessionStart` / `SessionEnd` / `PreCompact` hooks save and reload context across sessions automatically, so long-running work survives compaction.
- **Continuous learning** — the `continuous-learning` skill + `/learn` command extract reusable patterns from a live session into new skills.
- **Verification loops** — `eval-harness` + `verification-loop` skills and `/checkpoint` / `/verify` commands turn "looks done" into evidence-backed done.
- **Context-window discipline** — `performance` rule + contexts keep your tool surface lean. (Rule of thumb: configure 20–30 MCPs, keep under 10 enabled per project, under 80 active tools.)
- **Cross-platform** — all hooks/scripts are Node.js; package-manager auto-detection works with npm, pnpm, yarn, and bun.

## 🗺️ Status

Actively maintained and used in real projects. Contributions are welcome — language-specific skills, framework configs, DevOps agents, and new hooks especially. See [CONTRIBUTING.md](CONTRIBUTING.md).

## 🤝 Connect / About

Maintained by **Tony (Sheng)** — a Chinese-language teacher with 6,000+ students, building AI + Chinese-teaching tools in public.

If this saves you setup time, please ⭐ **Star** the repo and **Follow [@shengdabai](https://github.com/shengdabai)** — it genuinely helps.

**Sibling repos worth a look:**
- [Tony-Claude-Code-Skills](https://github.com/shengdabai/Tony-Claude-Code-Skills) — a broader skills collection
- [Tony-claude-plugins](https://github.com/shengdabai/Tony-claude-plugins) — self-built Claude Code plugins
- [claude-code-config](https://github.com/shengdabai/claude-code-config) — personal Claude Code configuration

### Credits

Originally created by **[Affaan Mustafa](https://x.com/affaanmustafa)** as a community resource (the in-repo guides, examples, and many configs are his work). This is a maintained, curated fork. All original authorship and ideas remain credited to the original project.

### License

Released under the MIT License (see the original project's terms). Use freely, modify as needed, contribute back if you can.

---

<a name="中文"></a>
## 中文

> 一套精选、经实战检验的 Claude Code 工具箱 —— agents、skills、hooks、斜杠命令、规则与 MCP 集成，可直接放进 `~/.claude/` 使用。

**[English](#-everything-claude-code) | 中文**

别再每次从零搭建你的 Claude Code 配置。本仓库是一套即装即用的集合：**9 个专用 agent、11 个 skill、15 个斜杠命令、8 条规则、覆盖 6 类生命周期事件的 hooks、15 个 MCP 服务器配置** —— 既可作为单个 Claude Code 插件一键安装，也可按需挑选单个文件。

### 为什么需要它

大多数 Claude Code 配置每次都得从头来：同样的 agent、同样的 hook、同样的 `console.log` 拦截器，在每个仓库里手写一遍。这套工具箱把一套连贯、有主见的基线收拢到一起 —— 安装一次即可全速开工,再删掉不适合你技术栈的部分即可。

它以 **Claude Code 插件**形式安装(一条命令),也可把单个 `.md` 文件按需复制进 `~/.claude/`。全部为纯 Markdown + Node.js,跨平台支持 **Windows、macOS、Linux**。

### ✨ 包含内容

| 类别 | 数量 | 内容 |
|------|------|------|
| 🤖 **Agents** | 9 | 用于委派的专用子代理 —— planner、architect、code-reviewer、security-reviewer、tdd-guide、build-error-resolver、e2e-runner、refactor-cleaner、doc-updater |
| 🧠 **Skills** | 11 | 工作流 + 领域知识 —— coding-standards、backend-patterns、frontend-patterns、tdd-workflow、security-review、eval-harness、verification-loop、continuous-learning、strategic-compact、project-guidelines |
| ⚡ **Commands** | 15 | 斜杠命令 —— `/tdd`、`/plan`、`/e2e`、`/code-review`、`/build-fix`、`/refactor-clean`、`/learn`、`/checkpoint`、`/verify`、`/orchestrate`、`/test-coverage`、`/update-docs`、`/update-codemaps`、`/eval`、`/setup-pm` |
| 📏 **Rules** | 8 | 始终遵循的准则 —— security、coding-style、testing、git-workflow、agents、hooks、patterns、performance |
| 🪝 **Hooks** | 6 类事件 | 基于触发器的自动化,覆盖 `PreToolUse`、`PostToolUse`、`Stop`、`SessionStart`、`SessionEnd`、`PreCompact` —— 内存持久化 + 战略性压缩 |
| 🧩 **Contexts** | 3 | 动态系统提示注入模式 —— dev、review、research |
| 🔌 **MCP 配置** | 15 | 即贴即用的服务器配置 —— GitHub、Supabase、Vercel、Railway、Firecrawl、ClickHouse、Context7、Magic、Filesystem、Memory、Sequential-Thinking 以及 Cloudflare 全家桶 |

此外还有 Node.js **测试套件**、跨平台**包管理器检测**(npm / pnpm / yarn / bun),以及项目级与用户级的示例 `CLAUDE.md`。

### 🧱 目录结构

```
everything-claude-code/
├── .claude-plugin/   # plugin.json + marketplace.json(作为插件安装)
├── agents/           # 9 个专用子代理
├── skills/           # 11 个工作流 / 领域知识 skill
├── commands/         # 15 个斜杠命令
├── rules/            # 8 个始终遵循的准则文件
├── hooks/            # hooks.json + memory-persistence + strategic-compact
├── contexts/         # 3 种动态系统提示模式(dev / review / research)
├── mcp-configs/      # 15 个 MCP 服务器配置
├── scripts/          # 跨平台 Node.js hook 实现 + 包管理器设置
├── tests/            # Node.js 测试套件(node tests/run-all.js)
└── examples/         # 项目级与用户级 CLAUDE.md 示例
```

### 🚀 如何使用

**方式一 —— 作为插件安装(推荐)**

```bash
/plugin marketplace add shengdabai/everything-claude-code
/plugin install everything-claude-code@everything-claude-code
```

或直接写入 `~/.claude/settings.json`:

```json
{
  "extraKnownMarketplaces": {
    "everything-claude-code": {
      "source": { "source": "github", "repo": "shengdabai/everything-claude-code" }
    }
  },
  "enabledPlugins": {
    "everything-claude-code@everything-claude-code": true
  }
}
```

**方式二 —— 手动按需复制**

```bash
git clone https://github.com/shengdabai/everything-claude-code.git

cp everything-claude-code/agents/*.md   ~/.claude/agents/
cp everything-claude-code/commands/*.md ~/.claude/commands/
cp everything-claude-code/rules/*.md    ~/.claude/rules/
cp -r everything-claude-code/skills/*   ~/.claude/skills/
```

随后把 `hooks/hooks.json` 合并进 `~/.claude/settings.json`,并从 `mcp-configs/mcp-servers.json` 把需要的 MCP 服务器复制进 `~/.claude.json`。
**重要**:使用前请把所有 `YOUR_*_HERE` 占位符替换为你自己的 API 密钥。

**运行测试**

```bash
node tests/run-all.js
```

### 📖 亮点

- **内存持久化** —— `SessionStart` / `SessionEnd` / `PreCompact` hook 自动保存并重载会话上下文,让长任务在压缩后仍能延续。
- **持续学习** —— `continuous-learning` skill + `/learn` 命令,把活动会话中的可复用模式提炼为新 skill。
- **验证循环** —— `eval-harness` + `verification-loop` skill 配合 `/checkpoint` / `/verify` 命令,把"看起来完成"变成有证据的"真正完成"。
- **上下文窗口纪律** —— `performance` 规则与 contexts 让工具面保持精简。(经验法则:配置 20–30 个 MCP,每项目启用不超过 10 个,活跃工具不超过 80 个。)
- **跨平台** —— 所有 hook/脚本均为 Node.js;包管理器自动检测支持 npm、pnpm、yarn、bun。

### 🗺️ 状态

持续维护,正用于真实项目。欢迎贡献 —— 尤其是特定语言的 skill、框架配置、DevOps agent 和新的 hook。详见 [CONTRIBUTING.md](CONTRIBUTING.md)。

### 🤝 关于 / 联系

由 **Tony(盛)** 维护 —— 一名拥有 6000+ 学员的中文老师,以 build in public 的方式打造 AI + 中文教学工具。

如果这套配置帮你省了搭建时间,欢迎 ⭐ **Star** 本仓库并 **关注 [@shengdabai](https://github.com/shengdabai)** —— 这对我帮助很大。

**值得一看的同系列仓库:**
- [Tony-Claude-Code-Skills](https://github.com/shengdabai/Tony-Claude-Code-Skills) —— 更广的 skill 合集
- [Tony-claude-plugins](https://github.com/shengdabai/Tony-claude-plugins) —— 自研 Claude Code 插件
- [claude-code-config](https://github.com/shengdabai/claude-code-config) —— 个人 Claude Code 配置

### 致谢

最初由 **[Affaan Mustafa](https://x.com/affaanmustafa)** 作为社区资源创建(仓库内的指南、示例及大量配置均出自其手)。本仓库是一个持续维护、精选整理的 fork,原作者的署名与思路均予以保留。

### 许可

基于 MIT 许可证发布(以原项目条款为准)。自由使用、按需修改,有余力欢迎回馈贡献。
