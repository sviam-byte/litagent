---
name: Text Diagnostic Core
description: Deep analysis of a text: detects genre, structure, argument, narrative movement, explanation gaps, and major defects before line editing
---

## Overview

This Skill performs a deep structural and semantic diagnosis of a text.

Use it when:
- analyzing essays, fiction, or hybrid texts
- evaluating clarity, argument, or narrative strength
- identifying where a text is broken (not just how it sounds)
- preparing for editing or rewriting

This Skill focuses on:
- understanding what the text is doing
- detecting structural and semantic failures
- producing grounded, evidence-based findings

It does NOT:
- perform surface proofreading
- rewrite the text
- generate stylistic fluff

---

## Core Principles

1. Diagnose before editing  
2. Do not assume genre — infer it  
3. Do not trust fluency — verify meaning  
4. Prefer mechanism over impression  
5. Every serious issue must be grounded in evidence  

---

## Analysis Layers

The Skill internally evaluates the text across several layers:

### 1. Corpus & Mode Detection
- What type of text is this?
- Fiction / nonfiction / hybrid?
- Is it complete or fragmentary?

### 2. Structural Segmentation
- Split into functional segments:
  - scene
  - argument
  - exposition
  - reflection
  - dialogue
  - mixed

If uncertain → mark as mixed, do not force classification.

---

### 3. Core Diagnostics

#### Narrative Layer (if applicable)
- Is there a driving force (conflict / tension)?
- Do scenes produce change?
- Are there dead zones?
- Is POV stable?

#### Argument Layer (if applicable)
- Is there a central claim?
- Are claims supported?
- Are overclaims?
- Are steps missing?

#### Explanation Layer
- Are causal steps present?
- Are transitions explained?
- Are metaphors replacing mechanisms?

#### Epistemic Layer
- Does the text overstate certainty?
- Does it blur fact vs interpretation?

#### Propulsion Layer
- Does the text move?
- Where does it stall?
- Where is it disproportionate?

---

### 4. AI-like Pattern Detection (non-binary)
Check for:
- empty generalizations
- template sentence rhythm
- semantic padding
- overbalanced tone

Also check counter-signals:
- specificity
- risk
- unevenness
- constraint awareness

---

## Failure Modes to Detect

Examples (not exhaustive):

- missing causal step
- argument leap
- scene without change
- abstract stack (too many nouns, no actions)
- decorative language without meaning
- pseudo-depth (sounds deep, says nothing)
- claim stronger than evidence
- unclear mode (reader cannot tell what this is)

---

## Evidence Rule

For every serious issue:
- locate where it happens
- explain how it breaks
- describe what effect it has

Avoid vague statements like:
- “this feels weak”
- “unclear”

---

## Output Format

Return structured findings + a short human-facing summary.

---

### Summary (5–8 sentences)

Describe:
- what the text is trying to do
- whether it succeeds
- where it breaks

---

### Findings

Each finding must include:

- category
- level (structural / semantic / language)
- description
- mechanism (WHY it breaks)
- evidence (where)
- severity (low / medium / high / critical)

---

### Strengths

List:
- what works
- why it works
- what must be preserved

---

### Cautions

If applicable:
- fragmentary text
- mixed mode
- uncertainty
- possible false positives

---

## What NOT to do

- Do not rewrite the text
- Do not produce generic advice
- Do not inflate trivial issues
- Do not assume intent without evidence
- Do not output a full editorial report (this is a diagnostic stage)

---

## Example Behavior (abstract)

Bad:
“This paragraph is unclear and needs improvement.”

Good:
“The transition between idea A and B is not explained. The text uses ‘therefore’ but skips the causal step, forcing the reader to infer the connection.”

---

## Resources

See additional documents for deeper rules:

- EXPLANATION.md
- AI_LANGUAGE.md
- FICTION_MASTER.md
- NONFICTION_MASTER.md
- MODE_BALANCE.md

Load them if needed depending on the text.
