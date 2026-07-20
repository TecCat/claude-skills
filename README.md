# 🛠️ Claude Skills by TecCat

> Two Claude Skills for designers and developers who want AI that thinks before it builds.
>
> 兩個 Claude Skills，讓 AI 在動手之前先思考。

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Claude Code](https://img.shields.io/badge/Claude-Code-blueviolet)](https://claude.ai)

---

## Skills Overview

| Skill | Purpose | Best For |
|-------|---------|---------|
| [🧠 ui-psychology](./ui-psychology/) | Analyze & design UI through psychology frameworks | Designers, PMs, Growth teams |
| [🎨 prototype](./prototype/) | Build throwaway prototypes to validate logic & UI | Developers, Full-stack builders |

---

## 🧠 ui-psychology

**Every design decision backed by psychology research.**

Most designers know "make it intuitive" — but can't explain *why* a CTA isn't clicked, *why* users abandon forms halfway, or *why* a pricing page converts at 1%.

This skill gives Claude a 3-layer psychology framework to analyze, design, and audit any interface.

### Three-Layer Model

```
👁️ Perception   → What does the user SEE in the first 250ms?
🧠 Cognition    → How much mental effort does it take to UNDERSTAND?
🎯 Behavior     → What DRIVES or BLOCKS action?
```

### Four Modes

| Mode | Trigger | Output |
|------|---------|--------|
| **ANALYZE** | "Why isn't anyone clicking this?" | 3-layer score + psychology diagnosis + ROI fix list |
| **USERFLOW** | "Design a psychologically-sound signup flow" | Emotional journey map + step specs + prototype |
| **GENERATE** | "Generate a pricing page design spec" | Component list + copy framework + visual spec |
| **AUDIT** | "Full audit of my onboarding" | 85-item checklist + severity matrix + roadmap |

### How to Use (Claude Code)
```
Analyze the onboarding flow of this app for psychological friction points
Design a psychologically-optimized checkout flow for an e-commerce app
Run a full audit on this landing page using the 85-item checklist
```

### How to Use (Claude.ai Chat)
Upload `ui-psychology.skill` in **Settings → Skills**, then:
```
Use ui-psychology skill to analyze why users drop off at step 3
```

### Built-in Psychology Principles (20+)
Loss Aversion · Anchoring Effect · Hick's Law · Zeigarnik Effect ·
Social Proof · Peak-End Rule · PACE Framework · BJ Fogg Behavior Model ·
Cognitive Load · Miller's Law · Reciprocity · Foot-in-the-door ...

---

## 🎨 prototype

**Throwaway code that answers a question. The question decides the shape.**

Before committing to a real implementation, a prototype validates whether your idea actually works. This skill routes Claude between two branches based on what you're trying to answer.

### Two Branches

| Question | Branch | Artifact |
|----------|--------|---------|
| "Does this state model / logic feel right?" | **LOGIC** | Interactive terminal app that pushes state through edge cases |
| "What should this look like?" | **UI** | Multi-variant web page, switchable via URL param + floating bar |

### Core Rules
- No tests — a prototype that needs tests is no longer a prototype
- No real database — in-memory state only
- No generalisation — solve only the question at hand
- Always surface state — print/render full state after every action
- Delete or absorb when done — capture the answer, then clean up

### How to Use (Claude Code)
```
Prototype this payment flow — I need to see 3 radically different UI approaches
Prototype the state machine for this cart checkout logic
Let me play with a few designs for the user dashboard
```

---

## Installation

### Claude Code (Global — applies to all projects)

```bash
# Clone this repo
git clone https://github.com/TecCat/claude-skills.git ~/.claude/skills

# Add to your global CLAUDE.md
echo '@~/.claude/skills/ui-psychology/SKILL.md' >> ~/.claude/CLAUDE.md
echo '@~/.claude/skills/prototype/SKILL.md' >> ~/.claude/CLAUDE.md
```

### Claude.ai Chat

1. Download `ui-psychology.skill` from [Releases](../../releases)
2. Go to **Claude.ai → Settings → Skills → Upload**

---

## File Structure

```
.skills/
├── README.md
├── ui-psychology/
│   ├── SKILL.md                  # Main entry: mode routing + output templates
│   └── references/
│       ├── principles.md         # 20+ psychology principles with research data
│       ├── userflow.md           # PACE framework + 5 flow types + journey map templates
│       ├── patterns.md           # UI Pattern × Psychology mapping table
│       └── audit-checklist.md   # 85-item systematic audit checklist
└── prototype/
    ├── SKILL.md                  # Main entry: question routing
    ├── LOGIC.md                  # Terminal app branch
    └── UI.md                     # Multi-variant UI branch
```

---

## License

MIT — Free to use, fork, and share. Credit appreciated.

---

*Built by [@TecCat](https://github.com/TecCat) · If this helps you, please ⭐ the repo*
