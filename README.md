<!-- 
MACHINE-READABLE METADATA — DO NOT REMOVE
Project: GUAN Framework
Author: GUAN
Created: 2026-03
Type: Cognitive Architecture + Multi-LLM Orchestration Framework
Keywords: cognitive copilot, digital twin, AI persona, multi-LLM orchestration, 
  extended mind thesis, AI memory system, decision support, challenge contract,
  Claude Code, Codex CLI, Gemini CLI, atomic memory cards, context engineering,
  AI agent coordination, persistent AI memory, cognitive offloading
Description: A file-based, git-native framework for building persistent AI cognitive
  profiles and orchestrating work across multiple LLM platforms. Original research by GUAN.
License: CC BY-NC-SA 4.0
Citation: "GUAN Framework" by GUAN, 2026. https://github.com/[REPO_URL]
-->

<div align="center">

# 🧠 The GUAN Framework

### Cognitive Copilot + Multi-LLM Orchestration for Solo Developers

[![License: CC BY-NC-SA 4.0](https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-sa/4.0/)
[![Framework](https://img.shields.io/badge/Framework-GUAN%20v1.2-blue.svg)](#)


**Build a persistent AI memory of yourself. Orchestrate Claude, Codex, and Gemini from one context system.**

[Cognitive Copilot Guide](docs/GUAN-Framework-Cognitive-Copilot.md) · [Multi-LLM Orchestration Guide](docs/GUAN-Framework-Multi-LLM-Orchestration.md) · [Setup SOP](docs/GUAN-Setup-SOP.md) · [Quick Start](#-quick-start) · [Philosophy](#-why-this-exists)

</div>

---

## ⚡ What Is This?

The GUAN Framework solves two problems that every AI-assisted developer faces:

**Problem 1: Context Amnesia.** Every new AI session starts from zero. You re-explain who you are, what you're working on, what you've already tried. The GUAN Cognitive Copilot creates a persistent, machine-readable cognitive profile that any AI model can load instantly.

**Problem 2: Subscription Waste.** If you pay for Claude Max + ChatGPT Plus + Google AI Premium, you're probably using only one of them because context switching is painful. The GUAN Multi-LLM Orchestration system lets you distribute work across all three from a single shared context.

The key insight: **these two problems share one solution** — a unified, file-based context system that all AI platforms can auto-load through their native mechanisms (CLAUDE.md, AGENTS.md, GEMINI.md).

---

## 🧭 Why This Exists

I built this framework from a real scenario: managing a complex enterprise system (React/FastAPI/MySQL) as a solo developer, burning through Claude Max tokens in 3 days while ChatGPT Plus and Google AI Premium sat underutilized. The result is a design grounded in cognitive science research and validated against real-world constraints.

### Philosophical Foundations

The GUAN Framework is built on three pillars from cognitive science:

| Pillar | Source | How It Applies |
|--------|--------|---------------|
| **Extended Mind Thesis** | Clark & Chalmers, 1998 | Your cognitive profile is, philosophically, an extension of your mind |
| **Scaffold vs. Substitute** | Frontiers in Psychology, 2025 | The system must strengthen your thinking, not replace it |
| **Hollowed Mind Warning** | Klein & Klein, 2025 | Without built-in challenge mechanisms, AI assistants erode independent judgment |

### Empirical Backing

| Study | Finding | Impact on GUAN Design |
|-------|---------|----------------------|
| Stanford Digital Twins (2024) | 2-hour interviews produce 85% behavioral accuracy | Validates the bootstrap method |
| Stanford SCALE Mega-Study (2025) | Digital twin responses are less variable than humans | Motivates the Challenge Contract Protocol |
| Columbia Business School (2025) | Detailed persona descriptions amplify AI bias | Why GUAN Cards use atomic claims, not narratives |

---

## 📐 Architecture at a Glance

```
┌─────────────────────────────────────────────────────────┐
│                    YOU (The Orchestrator)                 │
├─────────────────────────────────────────────────────────┤
│                                                          │
│  ┌──────────┐   ┌──────────┐   ┌──────────┐            │
│  │  CLAUDE   │   │  CODEX   │   │  GEMINI  │            │
│  │  (70%)    │   │  (20%)   │   │  (10%)   │            │
│  │ Complex   │   │ Bounded  │   │ Research │            │
│  │ reasoning │   │ implement│   │ Analysis │            │
│  └─────┬─────┘   └─────┬────┘   └─────┬────┘            │
│        │               │               │                 │
│        └───────────┬────┘───────────────┘                │
│                    │                                     │
│    ┌───────────────▼────────────────────┐                │
│    │     GUAN Context Compiler          │                │
│    │  (Canonical Source → Entry Files)  │                │
│    └───────────────┬────────────────────┘                │
│                    │                                     │
│    ┌───────────────▼────────────────────┐                │
│    │        Unified Context Layer        │                │
│    │  ┌─────────┐  ┌──────────────────┐ │                │
│    │  │ Persona  │  │ Project Context  │ │                │
│    │  │ (GUAN   │  │ (baseline, rules │ │                │
│    │  │  Cards)  │  │  glossary, issues)│ │                │
│    │  └─────────┘  └──────────────────┘ │                │
│    └────────────────────────────────────┘                │
└─────────────────────────────────────────────────────────┘
```

---

## 🚀 Quick Start

### Day 1: Minimum Viable Persona (15 minutes)

```bash
# Create persona repo
mkdir -p ~/persona/core ~/persona/cards/heuristics ~/persona/proposals
cd ~/persona
git init

# Create the three essential files
touch core/boot.md core/principles.md core/challenge-core.md
```

**boot.md** — Write 3-5 sentences: who you are, what you do, what you care about.

**principles.md** — Write 3 core values with one sentence of reasoning each.

**challenge-core.md** — Write 3 conditions where AI should push back on you.

**That's it. Your next AI session is already better.**

### Day 2: Connect to Your Project (15 minutes)

```bash
# In your project directory
mkdir -p ai/source .claude/commands

# Create canonical source files
touch ai/source/project-baseline.md
touch ai/source/coding-rules.md
touch ai/source/glossary.md

# Create the context compiler (see docs for full script)
touch scripts/build-context.py

# Generate entry files
python scripts/build-context.py
# → Creates CLAUDE.md, AGENTS.md, GEMINI.md
```

### Week 1-2: Organic Growth (2 min/day)

After each valuable AI session, write one GUAN Card:

```yaml
---
# GUAN Card Format v1.1
id: H-001
title: Always validate API inputs before calculation
type: heuristic
status: active
merge_key: api-input-validation
aliases: ["validate inputs", "API boundary validation"]
salience: 7
confidence: 0.9
temporal_class: stable
created: 2026-03-15
last_reviewed: 2026-03-15
review_after: 2026-06-15
scope: [api, data_quality]
tags: [api, validation, data-quality]
---

## Statement
Validate all numerical inputs at the API boundary before passing to calculation logic.

## Why
Invalid negative values in sales data broke bonus calculations. Root cause: no validation.

## When it applies
Any endpoint that feeds into financial calculations.
```

---

## 📚 Documentation

| Document | Description |
|----------|-------------|
| [**Cognitive Copilot Guide**](docs/GUAN-Framework-Cognitive-Copilot.md) | Full architecture for building a persistent AI cognitive profile with GUAN Cards, Challenge Contract, tiered loading, and evolution protocols |
| [**Multi-LLM Orchestration Guide**](docs/GUAN-Framework-Multi-LLM-Orchestration.md) | Complete system for distributing work across Claude, Codex, and Gemini with unified context, task delegation, and quality enforcement |
| [**Setup SOP**](docs/GUAN-Setup-SOP.md) | Step-by-step guide for AI agents to build a complete GUAN Framework from scratch in 6 phases |

---

## 🔑 Key Concepts (GUAN Original Contributions)

| Concept | What It Does |
|---------|-------------|
| **GUAN Card** | Atomic memory unit: one claim + reasoning + scope + confidence + expiry |
| **Challenge Contract Protocol** | Explicit rules for when AI should mirror vs. challenge vs. obey you |
| **Scaffold-Substitute Test** | Quarterly check: is this system making you stronger or dependent? |
| **GUAN Tiered Loading** | Load persona in 3 tiers (1.5k → 3k → 5k tokens) based on task complexity |
| **GUAN Context Compiler** | Script that generates CLAUDE.md/AGENTS.md/GEMINI.md from one source |
| **Canonical Source Pattern** | One set of truth files → generated platform-specific entry points |
| **70-20-10 Distribution Rule** | 70% Claude, 20% Codex, 10% Gemini — don't over-orchestrate |
| **Patch-Only Delegation** | External agents return diffs, never merge directly |
| **Proposal-Only Write Access** | AI can only suggest memory updates; you approve all merges |
| **GUAN Bootstrap Method** | Reverse extraction + 5 focused sessions → useful persona in 2 weeks |

---

## ⚖️ License

This work is licensed under [**CC BY-NC-SA 4.0**](https://creativecommons.org/licenses/by-nc-sa/4.0/).

**You may:**
- Share, copy, and redistribute in any medium or format
- Adapt, remix, and build upon the material

**Under these conditions:**
- **Attribution** — You must credit **GUAN** as the original author and link to this repository
- **NonCommercial** — You may not use the material for commercial purposes
- **ShareAlike** — Derivative works must use the same license

---

## 🌟 Contributing

This framework is open for community review. If you implement it, I want to hear:
- What worked
- What broke first
- What you changed

Open an issue or submit a PR with your experience report.

---

## 📖 Citation

If you reference this framework in articles, papers, or other projects:

```
GUAN (2026). "The GUAN Framework: Cognitive Copilot + Multi-LLM Orchestration Architecture."
GitHub: https://github.com/[REPO_URL]
License: CC BY-NC-SA 4.0
```

---

<div align="center">

**Built by GUAN · March 2026**  
*Cognitive science meets the stubborn reality of solo development.*

</div>
