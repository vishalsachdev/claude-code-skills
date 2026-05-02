# Claude Code Skills by Vishal Sachdev

[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-Compatible-blue?style=flat&logo=anthropic)](https://agentskills.io)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Professional skills for [Claude Code](https://claude.com/claude-code) following the [Agent Skills](https://agentskills.io) open specification.

> **Attribution note:** Some skills in this repository were originally contributed or inspired by other authors in the broader Claude Code community. I've collected and refined them over time across many machines and sessions, and I've lost the traceability needed to credit individual contributors. If you recognize a skill as yours or derived from your work, please open an issue and I'll happily add attribution. Skills I authored myself are noted in their frontmatter.

## 📚 Available Skills

### 📝 Paper Writing

Comprehensive academic paper writing guidance with expert workflows, templates, and quality checking tools.

**Perfect for:**
- Research papers and journal articles
- Conference papers (ACM, IEEE, etc.)
- Technical reports and white papers
- Thesis chapters and dissertations
- Literature reviews and survey papers

**What's included:**
- **4 comprehensive reference guides** (69KB total)
  - Elite IS Papers (Thatcher's 17 Rules)
  - Writing Guidelines (argument, evidence, citations, ethics)
  - Structure Templates (7 paper types)
  - Style Guide (clarity, precision, revision)
- **2 detailed paper templates**
  - Research Paper (IMRAD format)
  - Conference Paper (CS/Engineering)
- **Quality checker script** (automated style analysis)
- **3,478 lines** of expert guidance

**Based on:**
- **Thatcher, Jason Bennett** (2024). "Rules for Writing Elite Information Systems Papers." SSRN: https://papers.ssrn.com/sol3/papers.cfm?abstract_id=5993034
- APA Style (7th Edition)
- IEEE Editorial Style
- Academic writing best practices from Ohio University, Duke, MIT, USC, UCSD

📖 [Full Documentation](./skills/paper-writing/SKILL.md) | 💾 [Download v1.0.0](https://github.com/vishalsachdev/claude-code-skills/releases/download/v1.0.0/paper-writing-v1.0.0.skill)

---

### 🔮 Premortem

Run a Gary Klein-style premortem on any plan, launch, hire, or strategy: assume it already failed 6 months from now and work backward to find every reason why. Produces a revised plan with blind spots exposed.

**Use when:** you have a concrete plan with high cost-of-being-wrong and want to surface failure modes before committing.

**How it works:** gathers minimum context, generates the full failure-reason list, spawns one parallel agent per failure to write the failure story, then synthesizes the most likely / most dangerous / hidden assumption / revised plan / pre-launch checklist into an HTML report.

📖 [Full Documentation](./skills/premortem/SKILL.md)

---

### 📊 Agentic Eval-First Development

Architect, execute, and iterate on AI evaluations using the Data-Task-Score framework. Treats evals as the modern, quantifiable version of a PRD — moves teams beyond vibe checks to measurable AI quality.

**Use when:** building an eval, improving model quality, testing an agent workflow, quantifying product intuition, or setting up evaluation infrastructure.

📖 [Full Documentation](./skills/agentic-eval-first-development/SKILL.md)

---

### 🛡️ Agentic Validators

Design and install validation hooks for coding agents to make AI changes safer and more deterministic. Covers post-tool-use and stop hooks, automated tests/linters/formatters, parallel sub-agents with per-file validation, and audit logs.

**Use when:** you want to harden Claude Code with deterministic guardrails — catching bad edits before they land instead of after.

📖 [Full Documentation](./skills/agentic-validators/SKILL.md)

---

### 🎯 Codebase Singularity

A repeatable workflow for reliable codebase understanding and change. Provides guardrails and verification gates for high-trust, minimal-diff work — features, bugfixes, refactors, migrations.

**Use when:** the cost of an incorrect change is high and you want explicit validation steps and exit criteria, not just "looks good to me."

📖 [Full Documentation](./skills/codebase-singularity/SKILL.md)

---

### 🚀 Start / Wrap-Up Session

Two paired meta-skills for session lifecycle. **Start** reads project context (CLAUDE.md, git status, recent commits) and orients you for the session. **Wrap-up** reviews work, updates roadmaps, archives session logs, and surfaces carry-forward items.

**Use when:** you want consistent session bookends across all your repos — a reliable "where were we?" at the start and a clean handoff at the end.

📖 [Start Session](./skills/start-session/SKILL.md) · [Wrap-Up Session](./skills/wrap-up-session/SKILL.md)

---

### 🐦 Tweet Series Extractor

Extract tweet series from X/Twitter profiles with full content, embedded links, and engagement metrics preserved. Useful for analyzing recurring tweet formats — daily updates, weekly roundups, threads.

**Use when:** you want to study how someone tweets, archive your own tweets, or build a content corpus from a creator's profile.

📖 [Full Documentation](./skills/tweet-series-extractor/SKILL.md)

---

### 🏛️ LLM Council

Convene a 3-model council (Claude + GPT via codex CLI + Gemini CLI) on a high-stakes decision. Forces cross-critique between members and surfaces where the models actually disagree — breaking Claude's default agreeableness.

**Use when:** architecture, strategy, hiring, or pricing decisions where being wrong is expensive and you want genuinely different model perspectives, not just three Claude responses.

**How it works:** Round 1 — each model answers independently. Round 2 — each model critiques the others' answers. Round 3 — Claude synthesizes agreement, disagreement, what matters most, and a recommendation. Requires `codex` and `gemini` CLIs installed.

📖 [Full Documentation](./skills/llm-council/SKILL.md)

---

## 🚀 Quick Start

### Installation

**Option 1: Download pre-packaged skill**
```bash
# Download the .skill file
curl -L https://github.com/vishalsachdev/claude-code-skills/releases/download/v1.0.0/paper-writing-v1.0.0.skill -o paper-writing.skill

# Extract to Claude Code skills directory
unzip paper-writing.skill -d ~/.claude/skills/paper-writing

# Verify installation
ls -la ~/.claude/skills/paper-writing/
```

**Option 2: Clone and copy**
```bash
# Clone this repository
git clone https://github.com/vishalsachdev/claude-code-skills.git

# Copy specific skill
cp -r claude-code-skills/skills/paper-writing ~/.claude/skills/

# Verify installation
ls -la ~/.claude/skills/paper-writing/
```

### Usage

Skills automatically activate in Claude Code when relevant to your task. For example:

- Start typing "Help me write a research paper..." → Paper Writing skill activates
- "Review my paper's introduction..." → Paper Writing skill provides guidance
- "What's the best structure for a literature review?" → Paper Writing skill loads templates

You can also manually invoke skills by referencing them directly in your conversation.

---

## 📁 Repository Structure

```
claude-code-skills/
├── README.md                          # This file
├── CONTRIBUTING.md                    # Contribution guidelines
├── LICENSE                            # Repository license
├── skills/                            # Source skills
│   └── paper-writing/                 # Paper writing skill
│       ├── SKILL.md                   # Main skill file
│       ├── LICENSE.txt                # Skill license
│       ├── references/                # Reference materials
│       │   ├── ELITE-PAPERS.md
│       │   ├── REFERENCE.md
│       │   ├── STRUCTURE.md
│       │   └── STYLE.md
│       ├── assets/                    # Templates
│       │   ├── research-paper-template.md
│       │   ├── conference-paper-template.md
│       │   └── README.md
│       └── scripts/                   # Helper scripts
│           └── check_paper.py
├── releases/                          # Packaged .skill files
│   └── paper-writing-v1.0.0.skill
└── .github/
    └── workflows/
        └── package-skills.yml         # Auto-packaging workflow
```

---

## 🤝 Contributing

Contributions are welcome! Whether you want to:
- Report a bug
- Suggest improvements
- Add new skills
- Fix documentation

See [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines.

---

## 📖 About Agent Skills

These skills follow the [Agent Skills](https://agentskills.io) open specification, which means:

- ✅ **Portable** - Works across any AI platform that adopts the standard
- ✅ **Modular** - Each skill is self-contained and composable
- ✅ **Progressive** - Loads content only when needed to conserve context
- ✅ **Open** - Simple markdown format, easy to read and modify

Skills are not locked to Claude - the same skill format works across AI platforms and tools that adopt the Agent Skills standard.

---

## 📜 License

This repository is licensed under the MIT License - see [LICENSE](./LICENSE) file for details.

Individual skills may have their own licenses - check each skill's LICENSE.txt file.

---

## 🔗 Links

- [Agent Skills Specification](https://agentskills.io)
- [Claude Code Documentation](https://code.claude.com/docs)
- [Anthropic Skills Repository](https://github.com/anthropics/skills)

---

## 📬 Contact

**Vishal Sachdev**
- GitHub: [@vishalsachdev](https://github.com/vishalsachdev)

---

## ⭐ Show Your Support

If you find these skills useful:
- ⭐ Star this repository
- 🐛 Report issues
- 💡 Suggest new skills
- 🤝 Contribute improvements

---

**Made with ❤️ for the Claude Code community**
