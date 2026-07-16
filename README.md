# 🧠 Perfect Claude Skills

A collection of Claude Skills focused on **code review, patching, and enhancement**. Each skill is a self-contained folder with a `SKILL.md` defining the role, workflow, and output format Claude follows when the skill triggers.

---

## 📦 Skills

| Skill | Purpose | Rewrites Code? |
|---|---|---|
| [🧐 code-reviewer](./code-reviewer) | Reviews code, reports findings | ❌ Review only |
| [🩹 precision-script-patcher](./precision-script-patcher) | Smallest correct change to an existing script | ⚠️ Minimal diff only |
| [✨ script-enhancer](./script-enhancer) | Refactors code to production quality | ✅ Yes |
| [🏆 senior-code-reviewer-script-enhancer](./senior-code-reviewer-script-enhancer) | Review **and** enhance in one pass | ✅ Yes |
| [💬 conversation-summarizer](./conversation-summarizer) | Exports chat context to a portable `.md` handoff file | — |

---

### 🧐 code-reviewer

Senior-engineer code review. Analyzes correctness, bugs, security vulnerabilities, performance bottlenecks, maintainability, architecture, readability, and language/framework best practices.

- Separates **bugs / risks / style / optional improvements**
- Every recommendation is justified — no unexplained nitpicks
- Preserves author intent; suggests refactors without adding complexity

**Use when:** you want an audit, not a rewrite.

---

### 🩹 precision-script-patcher

Surgical patching for large codebases. Applies **only** the change requested.

- Preserves architecture, formatting, indentation, naming, comments, regions, code order
- Preserves public APIs, serialization attributes, inspector behavior, events/callbacks
- Never refactors unrelated code — every unchanged line is treated as correct

**Use when:** the file is large and you want a small, reviewable diff.

---

### ✨ script-enhancer

Staff-engineer refactor pass. Transforms working code into clean, idiomatic, production-ready code.

- Improves readability, simplifies logic, removes duplication
- Optimizes performance where measurable; increases maintainability
- Detects language, framework, dependencies, and conventions **before** editing
- Functional equivalence guaranteed unless a behavioral change is requested

**Use when:** the code works but is messy.

---

### 🏆 senior-code-reviewer-script-enhancer

Combined review + enhancement. Staff/Principal-level pass covering correctness, security, performance, scalability, and architecture, followed by a cleaned-up implementation.

- Phase 1 — understand: language, framework/engine, purpose, dependencies, data flow, conventions
- Phase 2 — evidence-based findings
- Phase 3 — improved implementation
- No invented APIs or libraries; no unnecessary breaking changes

**Use when:** you want both the diagnosis and the cure.

---

### 💬 conversation-summarizer

Produces a portable Markdown recap of the current conversation, ready to paste or upload into a fresh chat.

Sections: **Context**, **Decisions Made**, **Technical Details** (verbatim code blocks), **Open / Pending Tasks**, **Other Notes**.

Outputs `conversation-summary-<topic-slug>.md`.

**Use when:** you're hitting context limits or continuing work tomorrow.

---

## 🗂️ Structure

```
.
├── README.md
├── code-reviewer/
│   └── SKILL.md
├── conversation-summarizer/
│   └── SKILL.md
├── precision-script-patcher/
│   └── SKILL.md
├── script-enhancer/
│   └── SKILL.md
└── senior-code-reviewer-script-enhancer/
    └── SKILL.md
```

Each `SKILL.md` opens with YAML frontmatter:

```yaml
---
name: skill-name
description: "When Claude should trigger this skill and what it does."
---
```

`name` must match the folder name (lowercase, hyphens, ≤64 chars). `description` (≤1024 chars) is the **only** field Claude reads when deciding whether to load the skill — trigger keywords belong there, not in the body.

---

## 🚀 Installation

### Claude Code / Desktop

Whole collection:

```bash
git clone https://github.com/HandarX/Perfect-Claude-Skills.git
mkdir -p ~/.claude/skills
cp -r Perfect-Claude-Skills/*/ ~/.claude/skills/
```

One skill only:

```bash
git clone --depth 1 --filter=blob:none --sparse https://github.com/HandarX/Perfect-Claude-Skills.git
cd Perfect-Claude-Skills
git sparse-checkout set code-reviewer
cp -r code-reviewer ~/.claude/skills/
```

### Claude.ai

1. Download the repo — **Code → Download ZIP**, or:
   ```bash
   curl -L -o skills.zip https://github.com/HandarX/Perfect-Claude-Skills/archive/refs/heads/main.zip
   unzip skills.zip
   ```
2. Zip a **single skill folder** (the ZIP must contain a folder holding `SKILL.md`):
   ```bash
   zip -r code-reviewer.zip code-reviewer
   ```
3. Enable **Settings → Capabilities → Code execution and file creation**.
4. **Settings → Customize → Skills → Upload**, one ZIP per skill.

### Verify

```bash
ls ~/.claude/skills
```

---

## 🎯 Choosing a Skill

```
Need feedback only?           → code-reviewer
Need a tiny, safe change?     → precision-script-patcher
Need a full cleanup?          → script-enhancer
Need both review + cleanup?   → senior-code-reviewer-script-enhancer
Need to carry context over?   → conversation-summarizer
```

---

## 📄 License

MIT
