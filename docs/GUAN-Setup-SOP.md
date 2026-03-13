# GUAN Framework Setup SOP

> Step-by-step guide for any AI agent to build a complete GUAN Framework instance.
> After setup, the framework is branded as "GUAN" and ready for demonstration.

**Version:** 1.2 · **License:** CC BY-NC-SA 4.0

---

## Prerequisites

- Git installed and configured
- Node.js 18+ installed (for Codex CLI and Gemini CLI)
- Claude Code CLI installed and authenticated
- A working directory for the persona repository (e.g., ~/persona)
- OpenAI API key (for Codex CLI)
- Google account (for Gemini CLI authentication)

---

## Phase 1: Persona Repository Setup

### Step 1.1: Create directory structure

```bash
mkdir -p ~/persona/core
mkdir -p ~/persona/cards/heuristics
mkdir -p ~/persona/cards/anti_patterns
mkdir -p ~/persona/cards/communication
mkdir -p ~/persona/cards/domain
mkdir -p ~/persona/cards/uncertainty
mkdir -p ~/persona/indexes
mkdir -p ~/persona/proposals
mkdir -p ~/persona/sessions
mkdir -p ~/persona/framework
mkdir -p ~/persona/archive
mkdir -p ~/persona/.claude/commands
mkdir -p ~/persona/.claude/rules
```

### Step 1.2: Create boot.md

Write ~/persona/core/boot.md with this template:

```markdown
# [YOUR_NAME] — Boot Context

## Identity
[YOUR_ROLE at YOUR_ORGANIZATION. 1-2 sentences about what you do.]

## Environment
[Brief description of your work environment, team size, tech stack context.]

## Languages
[Your working languages and how you use them. E.g., "English for code and docs, Spanish for stakeholder communication."]

## Tech Stack
[List your primary technologies: Frontend / Backend / Database / DevOps]

## Capability Profile
- System architecture: [level — what you can do]
- Business logic: [level — what you understand]
- Coding: [level — honest self-assessment]
- AI tools: [level — how you use them]

**Core strength: [one sentence about your key competitive advantage]**

## Communication Rules
- [Rule 1: e.g., "Give direct answers, not preamble"]
- [Rule 2: e.g., "Structured output: tables, numbered lists"]
- [Rule 3: e.g., "Flag problems honestly, don't sugarcoat"]

## Known Blind Spots (for AI to monitor)
- [Blind spot 1 with mitigation instruction]
- [Blind spot 2 with mitigation instruction]
```

### Step 1.3: Create principles.md

Write ~/persona/core/principles.md:

```markdown
# [YOUR_NAME] — Core Principles

> 3-5 non-negotiable values. Loaded every session (Tier A).
> Each principle includes reasoning and scope.

---

## P1: [PRINCIPLE_NAME] — [Short tagline]

**Statement:** [One clear sentence]

**Why:** [2-3 sentences explaining the reasoning]

**When it bends:** [When this principle has exceptions]

---

## P2: [PRINCIPLE_NAME] — [Short tagline]

**Statement:** [One clear sentence]

**Why:** [2-3 sentences]

**When it bends:** [Exceptions]

---

## P3: [PRINCIPLE_NAME] — [Short tagline]

**Statement:** [One clear sentence]

**Why:** [2-3 sentences]

**When it bends:** [Exceptions]
```

### Step 1.4: Create challenge-core.md

Write ~/persona/core/challenge-core.md:

```markdown
# Challenge Contract — Core Rules

> Defines when AI should mirror, challenge, or obey.
> Loaded every session (Tier A).

---

## Mode: Mirror (Default — routine work)

**When:** Routine coding, formatting, documentation, clear requirements.

**Signals:** User says "just do it", "quick", "straightforward".

**AI behavior:**
- Match user's style and preferences without debate
- Efficient execution, concise output

---

## Mode: Challenge (Auto-triggered — high-risk scenarios)

### Trigger 1: Batch overload
- **Condition:** User requests more than 5 changes at once
- **Action:** Suggest batching, explain quality risks

### Trigger 2: Requirement contradictions
- **Condition:** Current request conflicts with previously confirmed design decisions
- **Action:** Point out the conflict, list contradictions, let user decide

### Trigger 3: Financial/compensation decisions
- **Condition:** Involves budget, pricing, investment, cost-cutting, bonuses
- **Action:** Present conservative AND aggressive scenarios with data

### Trigger 4: Personnel decisions
- **Condition:** Involves evaluation, hiring, firing, restructuring
- **Action:** Check fairness, second-order effects, cultural blind spots

### Trigger 5: Architecture decisions
- **Condition:** Tech stack, database design, system migration, API design
- **Action:** Present at least one alternative the user hasn't considered

### Trigger 6: Fatigue/time pressure
- **Condition:** User uses words like "urgent", "ASAP", "before the meeting"
- **Action:** Shorten output but increase caution, flag for later review

### Trigger 7: Optimistic effort estimates
- **Condition:** User says "just a small change", "simple fix"
- **Action:** Assess actual impact scope before executing

### Trigger 8: Security risks
- **Condition:** User sends passwords, tokens, API keys in conversation
- **Action:** Immediately warn about security risk

---

## Mode: Obey (User override)

**Signals:** User says "override", "ignore persona", "I know, just do it"

**AI behavior:**
- Execute current instruction without debate
- Say: "Override acknowledged."
- Log override event in session log

---

## High-Stakes Decision Output (required 4-part structure)

1. **Profile-aligned recommendation**
2. **Best counter-argument**
3. **Key assumption** that most influenced the recommendation
4. **Reversal condition** — what new evidence would change the recommendation
```

### Step 1.5: Create manifest.yaml

Write ~/persona/manifest.yaml:

```yaml
schema_version: "1.2"
framework: "GUAN Framework"
persona_root: "[ABSOLUTE_PATH_TO_PERSONA]"
projects_root: "[ABSOLUTE_PATH_TO_PROJECTS]"

reference_documents:
  cognitive_copilot: "framework/GUAN-Framework-Cognitive-Copilot.md"
  multi_llm_orchestration: "framework/GUAN-Framework-Multi-LLM-Orchestration.md"
  setup_sop: "framework/GUAN-Setup-SOP.md"

startup_rule: |
  On each new session:
  1. Read core/boot.md
  2. Read this manifest
  3. Read latest session log
  4. Read core/projects-overview.md for project list
  5. Enable semi-automatic cognitive collection

write_policy:
  canonical_write_mode: proposal_then_merge
  direct_card_creation: false
  override_keyword: "立即入库"
  max_new_cards_per_save: 1
  max_card_updates_per_save: 2

cognitive_collection:
  mode: "semi-automatic"
  trigger_conditions:
    - "User makes important decision"
    - "User describes new working pattern"
    - "User learns from a mistake"
    - "User expresses new principle"
    - "User behavior contradicts existing card"
  prompt_format: "💾 Cognitive collection suggestion: [description] — Save as card?"

loading_rules:
  always_load:
    - core/boot.md
    - core/principles.md
    - core/challenge-core.md
  on_demand:
    - cards/
    - framework/
  never_auto_load:
    - proposals/
    - archive/

review_cadence:
  stable: "no automatic decay"
  adaptive: "every 60-90 days"
  volatile: "every 14-30 days"

slash_commands:
  /boot: "Initialize session, load context, check agent health"
  /save: "Save session, evaluate cognition, write log, commit"
  /status: "View persona and project status overview"
```

### Step 1.6: Initialize Git

```bash
cd ~/persona
git init
git add -A
git commit -m "GUAN Framework v1.2: initial persona setup"
```

---

## Phase 2: Card System Setup

### Step 2.1: Create GUAN Card Format spec

Copy the guan-card-spec-v1.1.md to ~/persona/framework/ with the complete v1.1 specification including merge_key, aliases, salience fields, status lifecycle, and naming conventions.

<!-- 注：如果 framework/guan-card-spec-v1.1.md 已存在，跳过此步 -->

### Step 2.2: Create first example card

Write ~/persona/cards/heuristics/heuristic-001-example-card.md:

```yaml
---
id: H-001
title: "[YOUR_FIRST_HEURISTIC_TITLE]"
type: heuristic
status: active
merge_key: "[semantic-key]"
aliases:
  - "[alias in primary language]"
  - "[alias in secondary language]"
salience: 5
confidence: 0.8
temporal_class: adaptive
created: [TODAY_DATE]
last_reviewed: [TODAY_DATE]
review_after: [TODAY_DATE + 90 days]
scope: ["[domain1]", "[domain2]"]
tags: ["[tag1]", "[tag2]"]
related_to: []
supersedes: []
superseded_by: null
contradicts: []
evidence_refs: ["[Source description]"]
---

## Statement
[One clear statement of the heuristic]

## Applies When
[Conditions where this heuristic is relevant]

## Does NOT Apply
[Conditions where this heuristic should be ignored]

## Evidence
1. [Evidence entry with date and context]
```

### Step 2.3: Create indexes

Write ~/persona/indexes/card-index.yaml:

```yaml
# GUAN Card Index — auto-maintained
# Last updated: [TODAY_DATE]
cards:
  - id: H-001
    title: "[YOUR_FIRST_HEURISTIC_TITLE]"
    type: heuristic
    status: active
    merge_key: "[semantic-key]"
    aliases: ["[alias1]", "[alias2]"]
    tags: ["[tag1]", "[tag2]"]
    scope: ["[domain1]", "[domain2]"]
    salience: 5
    path: cards/heuristics/heuristic-001-example-card.md
    one_line: "[One-line summary]"
```

Write ~/persona/indexes/card-search-index.md:

```markdown
# Card Search Index (Ctrl+F searchable)

## Heuristics
- H-001: [slug] → [one-line description] [merge_key: key]

## Anti-Patterns
(none yet)

## Statistics
- Total: 1 card (1 heuristic)
- Active: 1 | Cooling: 0 | Archived: 0
- Last updated: [TODAY_DATE]
```

Write ~/persona/indexes/lexicon.yaml:

```yaml
# Synonym normalization table for /save dedup matching
# Format: canonical_term: [alias1, alias2, ...]
[semantic-key]: ["[alias1]", "[alias2]"]
```

### Step 2.4: Commit card system

```bash
cd ~/persona
git add -A
git commit -m "GUAN Framework: card system + indexes initialized"
```

---

## Phase 3: Rules & Commands Setup

### Step 3.1: Create rules files

Create all 7 rules files in ~/persona/.claude/rules/ (and optionally symlink or copy to ~/.claude/rules/).

<!-- 注：rules 既放在 persona 仓库内版本管理，也复制到 ~/.claude/rules/ 让 Claude Code 自动加载 -->

**1. guan-persona-loader.md** — Auto-load persona context:

```markdown
---
description: Auto-load persona context at session start
globs: **/*
---

On new session start, silently execute:

1. Read [PERSONA_PATH]/core/boot.md
2. Read [PERSONA_PATH]/core/principles.md
3. Read [PERSONA_PATH]/core/challenge-core.md
4. Read latest session log from [PERSONA_PATH]/sessions/

These contents serve as baseline context for the entire session.
```

**2. guan-project-scanner.md** — Auto-load project context:

```markdown
---
description: Auto-load project context when entering project directories
globs: [PROJECTS_PATH]/**/*
---

When user enters a project directory under [PROJECTS_PATH]:

1. Read ai/source/project-baseline.md (if exists)
2. Read ai/source/coding-rules.md (if exists)
3. Read ai/source/glossary.md (if exists)
4. Read CLAUDE.md

If user is in their home directory, scan [PROJECTS_PATH]/ and list all project folder names.
```

**3. guan-cognitive-collection.md** — Semi-automatic cognitive collection:

```markdown
---
description: Monitor for cognitive value signals during work
globs: **/*
---

Monitor for cognitive value signals during conversation.

## Trigger Conditions (any one triggers prompt)

- User makes an important decision (tech choice, business rule change, architecture adjustment)
- User describes a working pattern or preference not yet recorded
- User makes a mistake and learns a lesson
- User expresses a new principle or value judgment
- User behavior contradicts an existing card in persona/cards/

## When Triggered

Append to reply:
💾 Cognitive collection suggestion: [brief description] — Save as card? (Reply "存" or ignore)

## On User Reply "存"

1. Create file in [PERSONA_PATH]/cards/[appropriate_subdirectory]/
2. Filename format: [type]-[id]-[semantic-slug].md (id = max existing id + 1)
3. Use GUAN Card Format v1.0 (YAML frontmatter + Markdown body)
4. git add the file && git commit -m "New card: [title]"
5. Continue normal work without interrupting user

## On User Reply "立即入库"

Same as "存" but also update indexes/card-index.yaml and indexes/card-search-index.md.

## On User Ignore

No action. Continue normal work.
```

**4. guan-multi-llm-detector.md** — Trigger Matrix v1.2:

Copy complete content from the Trigger Matrix v1.2 specification in the companion Multi-LLM Orchestration document (`framework/GUAN-Framework-Multi-LLM-Orchestration.md`), including: risk scoring, 5 delegation modes (Codex Review Gate, Codex Bulk, Gemini Research, Gemini Doc-Summary, Gemini Compare), JSON contract format, suggestion format, failure handling, and result verification rules.

**5. guan-codex-review-gate.md** — Codex Review Gate:

Copy complete content from the Codex Review Gate specification in the companion Multi-LLM Orchestration document, including: 3+ changes trigger condition, JSON output requirement, NO `--skip-git-repo-check` flag, 45-second timeout, and fallback behavior.

**6. guan-multi-llm-prohibitions.md** — Absolute prohibitions:

Copy complete content from the Prohibitions specification in the companion Multi-LLM Orchestration document, including: 9 absolute prohibitions (e.g., no direct file writes by external agents, no credential access) and 5 high-risk confirmation rules.

**7. guan-sop-rules.md** — Operational rules:

```markdown
---
description: Operational rules enforced every session
globs: **/*
---

The following rules are enforced in every session:

1. **Batch limit:** Max 5 changes per batch. If user requests more than 5 changes at once, suggest splitting into batches.

2. **Browser verification:** After completing key code changes, remind user to verify in browser.

3. **Conflict detection:** If a new request conflicts with previously confirmed design decisions, point out the conflict and ask how to proceed.

4. **Speed mode:** When user uses words like "quick", "urgent", "ASAP", "rush", shorten output but increase caution on irreversible decisions. Append: "⚡ Speed mode: recommend reviewing this decision later."

5. **Security alert:** If user sends passwords, tokens, API keys, or any credentials in conversation, immediately warn: "⚠️ Sensitive information detected. Recommend revoking and rotating credentials immediately."

6. **SOP compliance:** Follow all iron rules in [PERSONA_PATH]/framework/Claude-Code-SOP-v3.md (WORK_LOG, git commit discipline, context protection protocol, etc.).

7. **Effort assessment:** If user says "just a small change" or similar, first evaluate actual impact scope (which files, frontend/backend coupling, database changes), inform user of true effort, then execute.

8. **External agent logging:** Record all Codex/Gemini calls (prompt, result, duration) in the /save session log for traceability.
```

### Step 3.2: Create slash commands

Create 3 command files in ~/persona/.claude/commands/:

**1. boot.md:**

```markdown
---
description: Initialize GUAN work session
allowed-tools: Read, Write, Edit, Bash, Grep, Glob
---

GUAN Framework v1.2 — Session initializing...

## Steps

1. Rules auto-loaded persona context (boot.md, principles.md, challenge-core.md)
2. Read [PERSONA_PATH]/core/projects-overview.md for project list
3. Read latest session log from [PERSONA_PATH]/sessions/
4. Execute agent health check:
   - Run: codex --version
   - Run: gemini --version
   - Determine available mode based on which agents respond

## Output Report

```
╔══════════════════════════════════════╗
║       GUAN Framework v1.2           ║
║       Session Initialized           ║
╚══════════════════════════════════════╝

Last session:    [date and one-line summary]
Projects:        [discovered project list]
Working dir:     [current path]
Available mode:  [Claude-only / Claude+Codex / Claude+Gemini / Full Triad]
Pending tasks:   [from last session log, or "none"]

Ready.
```

Note: If codex or gemini are unavailable, report the limitation but do not block startup. The framework operates in degraded mode with Claude-only capabilities.
```

**2. save.md** — 7-phase save protocol:

```markdown
---
description: Save GUAN session — 7-phase protocol
allowed-tools: Read, Write, Edit, Bash, Grep, Glob
---

GUAN Framework v1.2 — /save executing...

## Phase 1: Session Log

Create session log at [PERSONA_PATH]/sessions/YYYY-MM/session-YYYY-MM-DD-HHMM.md with:
- Session date, duration estimate
- Work summary (what was done)
- Decisions made (with reasoning)
- External agent calls (Codex/Gemini invocations, prompts, results)
- Open questions / pending items for next session

## Phase 2: Cognitive Quality Filter

Review conversation for cognitive value signals. For each candidate:
- Is it genuinely new? (not already captured in an existing card)
- Is it specific enough to be actionable?
- Does it have evidence from this session?

Score each candidate: HIGH (save) / MEDIUM (propose) / LOW (discard).

## Phase 3: Dedup Check

For HIGH/MEDIUM candidates:
1. Read [PERSONA_PATH]/indexes/lexicon.yaml for synonym matches
2. Read [PERSONA_PATH]/indexes/card-index.yaml for existing cards
3. If merge_key or alias matches an existing card → update existing card instead of creating new
4. If no match → proceed to write

## Phase 4: Write

For HIGH candidates:
- Write new card or update existing card
- Follow GUAN Card Format v1.1 spec
- Respect write_policy: max 1 new card, max 2 updates per /save

For MEDIUM candidates:
- Write proposal to [PERSONA_PATH]/proposals/ for user review later

## Phase 5: Index Update

- Update indexes/card-index.yaml with new/modified cards
- Update indexes/card-search-index.md
- Update indexes/lexicon.yaml with new aliases

## Phase 6: Git Commit

```bash
cd [PERSONA_PATH]
git add -A
git commit -m "/save: [one-line session summary]"
```

## Phase 7: Report

```
╔══════════════════════════════════════╗
║       GUAN /save Complete           ║
╚══════════════════════════════════════╝

Session log:     [path]
New cards:       [count] ([list ids])
Updated cards:   [count] ([list ids])
Proposals:       [count]
Total cards:     [count] (active: X, cooling: Y, archived: Z)
Git commit:      [hash]

Next session pickup: [pending items summary]
```
```

**3. status.md** — System overview:

```markdown
---
description: Display GUAN Framework status overview
allowed-tools: Read, Bash, Grep, Glob
---

GUAN Framework v1.2 — Status Report

## Steps

1. Count cards by type and status from indexes/card-index.yaml
2. List projects from core/projects-overview.md
3. Count pending proposals from proposals/
4. Read latest session log date
5. Check review_after dates for cards needing review

## Output

```
╔══════════════════════════════════════╗
║     GUAN Framework v1.2 Status      ║
╚══════════════════════════════════════╝

Cards:
  Heuristics:     [count]
  Anti-patterns:  [count]
  Communication:  [count]
  Domain:         [count]
  Uncertainty:    [count]
  ─────────────────────
  Total:          [count] (active: X | cooling: Y | archived: Z)

Reviews due:     [count] cards past review_after date
Proposals:       [count] pending

Projects:        [list with status]

Last session:    [date]
Last /save:      [date]
```
```

### Step 3.3: Commit rules and commands

```bash
cd ~/persona
git add -A
git commit -m "GUAN Framework: rules system + slash commands"
```

---

## Phase 4: Multi-LLM Integration

### Step 4.1: Install Codex CLI

```bash
npm install -g @openai/codex
codex auth
# Follow prompts to authenticate with OpenAI API key
```

<!-- 注：需要有效的 OpenAI API key，建议使用 GPT-4o 级别的 key -->

### Step 4.2: Install Gemini CLI

```bash
npm install -g @google/gemini-cli
gemini
# First run opens browser for Google account authentication
# After auth, close and verify headless mode works
```

### Step 4.3: Verify connectivity

```bash
# Test Codex
codex exec --full-auto --ephemeral "Reply OK"

# Test Gemini
gemini -p "Reply OK"
```

Both should return responses without errors. If either fails, the framework still works in degraded mode (Claude-only or partial multi-LLM).

### Step 4.4: Commit integration status

```bash
cd ~/persona
git add -A
git commit -m "GUAN Framework: multi-LLM integration verified"
```

---

## Phase 5: Project Integration

### Step 5.1: Create project ai/source/ directory

In your project root:

```bash
mkdir -p ai/source
```

Create ai/source/project-baseline.md:

```markdown
# Project: [PROJECT_NAME]

## Status: [Current phase — e.g., "Active development", "Maintenance"]

## Tech Stack
- Frontend: [framework, version]
- Backend: [framework, version]
- Database: [type, version]
- Infrastructure: [hosting, CI/CD]

## Current Focus
[1-3 sentences describing what the team is working on right now]

## Active Risks
- [Risk 1: description and mitigation]
- [Risk 2: description and mitigation]
```

Create ai/source/coding-rules.md:

```markdown
# Coding Rules

## [PRIMARY_LANGUAGE]
- Style: [standard — e.g., PEP8, ESLint]
- Variable names: [language — e.g., English]
- Type annotations: [required/optional]
- Comments: [language and when required]

## [SECONDARY_LANGUAGE] (if applicable)
- Style: [standard]
- Components: [naming convention]
- Comments: [language], UI labels in [target language]

## General
- Max function length: [guideline]
- Test requirement: [policy — e.g., "unit tests for all business logic"]
- Error handling: [pattern]
```

Create ai/source/glossary.md:

```markdown
# Glossary

| Business Term | Code Identifier | UI Label | Notes |
|--------------|----------------|----------|-------|
| [Term] | `identifier` | [UI text] | [Context] |
```

### Step 5.2: Create CLAUDE.md

In project root, create CLAUDE.md:

```markdown
# [PROJECT_NAME] — AI Context

Read these files for project context:
- ai/source/project-baseline.md — project overview and current status
- ai/source/coding-rules.md — coding standards and conventions
- ai/source/glossary.md — business term to code identifier mapping
```

### Step 5.3: Create projects-overview.md

Write ~/persona/core/projects-overview.md:

```markdown
# Projects Overview

| Project | Path | Status | Notes |
|---------|------|--------|-------|
| [PROJECT_NAME] | [ABSOLUTE_PATH] | [Status] | [One-line description] |
```

### Step 5.4: Commit project integration

```bash
cd ~/persona
git add -A
git commit -m "GUAN Framework: project integration template"
```

---

## Phase 6: Verification

### Step 6.1: Test /boot

Open Claude Code in the persona directory and run `/boot`. Verify:

- [ ] Persona context loaded (boot.md, principles.md, challenge-core.md)
- [ ] Session log found or "no previous session" reported
- [ ] Agent health check executed (codex --version, gemini --version)
- [ ] Available mode correctly reported
- [ ] "GUAN Framework v1.2" branding displayed

### Step 6.2: Test /save

After doing some work, run `/save`. Verify:

- [ ] Session log created in sessions/YYYY-MM/
- [ ] Candidate insights evaluated (quality filter ran)
- [ ] Dedup check executed against existing cards
- [ ] Git commit created with descriptive message
- [ ] Report displayed with card counts and next-session pickup

### Step 6.3: Test Codex Review Gate

Request 3+ code changes in a single prompt. Verify:

- [ ] Review Gate triggered (multi-LLM detector fires)
- [ ] Modification plan displayed before execution
- [ ] Codex called for review (if available)
- [ ] User confirmation requested before applying changes

### Step 6.4: Test Gemini research mode

Ask about a topic requiring latest information or comparison. Verify:

- [ ] Multi-LLM suggestion displayed
- [ ] On user approval, Gemini called with research prompt
- [ ] Results verified by Claude before adoption into conversation

### Step 6.5: Test cognitive collection

Make a deliberate "decision" statement in conversation. Verify:

- [ ] Cognitive collection prompt appears at end of reply
- [ ] On "存", card created in correct subdirectory
- [ ] Card follows GUAN Card Format v1.1
- [ ] Git commit created automatically

---

## Post-Setup Checklist

```
[ ] ~/persona/core/boot.md — filled with real user data
[ ] ~/persona/core/principles.md — filled with real principles
[ ] ~/persona/core/challenge-core.md — reviewed, triggers adjusted
[ ] ~/persona/core/projects-overview.md — projects listed
[ ] ~/persona/manifest.yaml — paths set to absolute values
[ ] ~/persona/cards/ — at least one example card exists
[ ] ~/persona/indexes/ — all three index files created
[ ] ~/.claude/rules/ — all 7 rules files installed
[ ] ~/.claude/commands/ — all 3 slash commands installed
[ ] Multi-LLM agents tested (or degraded mode accepted)
[ ] Git repo initialized with at least 3 commits
[ ] /boot displays "GUAN Framework v1.2"
```

---

## Branding

After setup, this instance is a **GUAN Framework v1.2** deployment.

- The `/boot` command displays "GUAN Framework v1.2" branding
- All named concepts use the GUAN prefix
- The manifest.yaml declares `framework: "GUAN Framework"`
- Session logs and card operations reference the framework by name

---

## Troubleshooting

| Problem | Cause | Fix |
|---------|-------|-----|
| /boot shows no projects | projects-overview.md missing | Create core/projects-overview.md |
| Codex calls fail | API key expired or not set | Run `codex auth` again |
| Gemini calls fail | Auth token expired | Run `gemini` interactively to re-auth |
| Cards not deduped | lexicon.yaml empty | Add aliases after first few cards |
| Rules not loading | Files not in ~/.claude/rules/ | Copy from persona/.claude/rules/ |

---

*Licensed under CC BY-NC-SA 4.0. Credit GUAN as the original author.*
