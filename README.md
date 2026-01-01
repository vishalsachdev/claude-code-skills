# Claude Code Skills by Vishal Sachdev

[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-Compatible-blue?style=flat&logo=anthropic)](https://agentskills.io)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Professional skills for [Claude Code](https://claude.com/claude-code) following the [Agent Skills](https://agentskills.io) open specification.

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
- APA Style (7th Edition)
- IEEE Editorial Style
- Jason Bennett Thatcher's "Rules for Writing Elite Information Systems Papers"
- Academic writing best practices from Ohio University, Duke, MIT, USC, UCSD

📖 [Full Documentation](./skills/paper-writing/README.md) | 💾 [Download v1.0.0](https://github.com/vishalsachdev/claude-code-skills/releases/download/v1.0.0/paper-writing-v1.0.0.skill)

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
│       ├── README.md                  # Skill documentation
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
- Website: [vishalsachdev.com](https://vishalsachdev.com) *(if applicable)*

---

## ⭐ Show Your Support

If you find these skills useful:
- ⭐ Star this repository
- 🐛 Report issues
- 💡 Suggest new skills
- 🤝 Contribute improvements

---

**Made with ❤️ for the Claude Code community**
