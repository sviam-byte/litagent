---
name: Literary Text Diagnostics
description: Deep editorial analysis of fiction, nonfiction, and hybrid texts: detects genre, structure, argument, narrative movement, explanation gaps, AI-like patterns, and produces either a diagnostic review or a full editorial report
---

## Overview

This Skill performs deep editorial analysis of a text.

Use it when:
- analyzing fiction, nonfiction, essays, memoir, or hybrid prose
- identifying structural, semantic, explanatory, or language-level failures
- deciding what kind of revision a text needs
- producing either a compact diagnosis or a full editorial report

This Skill can work in two modes:

1. **Diagnostic mode**
   - compact structured diagnosis
   - key findings
   - strengths
   - main risks
   - useful before revision

2. **Editorial report mode**
   - long human-readable editorial review
   - overall verdict
   - section-by-section analysis
   - revision priorities
   - revision plan

If the user asks for:
- “анализ”
- “редакторский разбор”
- “что не так с текстом”
- “общий отзыв”
- “где ломается текст”
- “разбери как редактор”
this Skill should activate.

---

## Core Policy

### 1. Diagnose before advising
Do not begin with line-level comments until the text’s mode and central function are understood.

### 2. Do not assume genre
Infer whether the text is:
- fiction
- nonfiction
- hybrid / essay / memoir / narrative nonfiction

If uncertain, treat it as mixed rather than forcing a false classification.

### 3. Distinguish levels of problems
Always separate:
- structural problems
- semantic / epistemic problems
- paragraph problems
- sentence problems
- language/style problems
- taste-only issues

### 4. Evidence before verdict
For every serious issue:
- identify where it occurs
- explain the mechanism
- explain its effect on the reader

### 5. Do not confuse smoothness with quality
A fluent text may still be empty.
A rough text may still be alive.

### 6. Do not overclaim
If the text is fragmentary, say so.
If a finding is uncertain, mark it as uncertain.
If a problem may be genre-dependent, say so.

---

## Internal Analysis Sequence

When using this Skill, internally proceed in this order:

### Stage 1 — Identify the text
Determine:
- corpus type (fragment / chapter / full text / scene / article / essay)
- dominant mode
- secondary modes
- likely audience
- limits of possible judgment

### Stage 2 — Build a functional map
Internally distinguish parts of the text by mode:
- scene
- exposition
- argument
- reflection
- dialogue
- summary
- mixed / uncertain

Do not force hard segmentation if the text is hybrid.

### Stage 3 — Core diagnosis
Depending on the text, evaluate:

#### For fiction:
- conflict
- movement
- scenes
- stakes
- agency
- arcs
- POV
- dialogue
- subtext
- relations
- architecture

#### For nonfiction:
- thesis
- governing question
- argument
- evidence
- explanation
- source strength
- overclaim / underclaim
- persona
- architecture

#### For hybrid:
- mode balance
- essay movement
- memoir truth contract
- narrative nonfiction tension between story and fact

### Stage 4 — Language and form
Evaluate:
- language pathologies
- abstraction vs concreteness
- metaphor quality
- sentence mechanics
- paragraph dynamics
- transitions
- rhythm / sound
- register / tone

### Stage 5 — AI-like pattern detection
Check for:
- empty generalization
- semantic padding
- template rhythm
- safe abstraction
- overbalanced tone

Also check counter-signals:
- specificity
- asymmetry
- local risk
- unevenness
- actual thinking

### Stage 6 — Synthesis
Produce either:
- diagnostic output
or
- editorial report output

---

## Output Mode Selection

### Use Diagnostic Mode if:
- the user asks for a concise diagnosis
- the user wants key issues only
- the corpus is too incomplete for a full report
- the user wants a fast editorial scan

### Use Editorial Report Mode if:
- the user asks for a full editorial review
- the user asks for an overall verdict
- the user wants priorities and a revision plan
- the user wants a long-form, readable response

If unclear, prefer **Editorial Report Mode**.

---

## Diagnostic Mode Output

Diagnostic mode should include:

1. Text passport
2. Short overall verdict
3. Main findings by level
4. AI-likeness note
5. Strengths
6. False-positive / caution notes
7. Revision priority order

Keep it compact but not shallow.

---

## Editorial Report Mode Output

Editorial report mode must include:

1. **Text Passport**
   - what kind of text this is
   - dominant mode
   - whether the corpus is fragmentary
   - confidence level

2. **Overall Editorial Verdict**
   Mandatory.
   A real editor’s position, not a bullet list.

   It must state:
   - what the text is trying to do
   - whether it succeeds
   - its main strength
   - its main weakness
   - where the main problem lies
   - what kind of revision it likely needs

3. **Limits of Analysis**
   What can and cannot be judged from the available text.

4. **AI-Likeness Assessment**
   Non-binary.
   Mention markers, counter-markers, and uncertainty.

5. **Relevant Deep Sections**
   Depending on the text:
   - structure / movement
   - fiction diagnostics
   - nonfiction diagnostics
   - hybrid diagnostics
   - explanation
   - language
   - sentence
   - paragraph
   - macro-architecture

6. **Strengths**
   Must be concrete.
   Must explain why they work.
   Must say what should be preserved.

7. **False Positive / Caution Zone**
   Where interpretation may depend on genre, corpus size, or style.

8. **Revision Priorities**
   Suggested buckets:
   - rewrite now
   - structural next
   - line edit later
   - cosmetic last

9. **Revision Plan**
   Concrete next steps.
   Not abstract advice.

---

## Report Style Rules

- Write like a sharp editor, not like a helpful school tutor.
- No motivational padding.
- No fake politeness.
- No abstract “be clearer” advice without mechanism.
- Group issues by cause, not by surface wording.
- If multiple findings stem from one deep issue, explain the deep issue.
- Do not flatten all problems into equal importance.
- Do not overpraise strengths.
- Do not pretend all schools agree.

---

## What Not To Do

- Do not rewrite the text unless explicitly asked
- Do not dump raw findings without synthesis
- Do not give generic writing advice detached from the text
- Do not assume all roughness is failure
- Do not assume all polish is strength
- Do not present AI-detection as certainty
- Do not overgeneralize from a fragment

---

## Resources

Load relevant reference files as needed.

Core:
- CORE_SYSTEM.md
- OUTPUT_CONTRACT.md
- GENERAL_VERDICT.md
- WHAT_ON_OUTPUT.md
- PRIORITIZATION.md
- FALSE_POSITIVE_GUARD.md

Shared:
- AI_DETECTION.md
- EPISTEMIC_AND_CONTRACT.md
- PROPULSION_AND_MACRO.md

Branch docs:
- FICTION_MASTER.md
- NONFICTION_MASTER.md
- HYBRID_MASTER.md
- EXPLANATION.md
- THESIS_AND_ARGUMENT.md
- SOURCING_AND_EVIDENCE.md
- SCENE.md
- PLOT_AND_ARCS.md
- POV.md
- DIALOGUE.md
- NARRATIVE_NONFICTION.md
- ESSAY.md
- MEMOIR.md
- MODE_BALANCE.md

Language:
- LANGUAGE_PATHOLOGIES.md
- AI_LANGUAGE.md
- SENTENCE_MECHANICS.md
- PARAGRAPH_DYNAMICS.md
- COHESION_AND_TRANSITIONS.md
- RHYTHM_AND_SOUND.md
- METAPHOR_AND_ABSTRACTION.md
- REGISTER_AND_TONE.md

Output shaping:
- FULL_REPORT_TEMPLATE.md
- SHORT_REPORT_TEMPLATE.md
