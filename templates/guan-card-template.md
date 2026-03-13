---
# GUAN Card Format v1.1
# Template — copy this file and fill in your own content
id: H-XXX
title: [One-line description of the heuristic/pattern]
type: heuristic          # heuristic | anti_pattern | communication | domain | uncertainty | principle
status: active           # active | cooling | archived | superseded | merged
merge_key: [canonical-key]  # Unique key for dedup matching (kebab-case)
aliases:                    # Alternate phrasings for dedup (bilingual encouraged)
  - [alternate phrasing 1]
  - [alternate phrasing 2]
salience: 5              # 1-10, higher = more important (default 5)
confidence: 0.8          # 0.0 to 1.0
temporal_class: adaptive  # stable | adaptive | volatile
created: YYYY-MM-DD
last_reviewed: YYYY-MM-DD
review_after: YYYY-MM-DD  # stable: none | adaptive: 60-90 days | volatile: 14-30 days
scope: [domain1, domain2]
tags: [tag1, tag2, tag3]
related_to: []            # IDs of related cards, e.g., [H-001, A-003]
supersedes: []            # IDs of cards this one replaces
superseded_by: []         # ID of card that replaced this one
contradicts: []           # IDs of cards that may conflict with this one
evidence_refs: []         # Brief evidence descriptions
---

## Statement
[One clear, actionable claim. Not a paragraph — a single assertion.]

## Why
[The reasoning behind this claim. What experience or evidence supports it?]

## When it applies
[Scope: in what situations should this card be consulted?]

## When it does NOT apply
[Exceptions: what conditions make this card irrelevant or wrong?]

## Counterweight
[The strongest argument against this claim, or a complementary perspective to consider.]

## Evidence
- [Source 1: how you learned this — e.g., "Debugging session, March 2026"]
- [Source 2: e.g., "Confirmed by stakeholder in review meeting"]
