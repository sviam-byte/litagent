---
name: Editorial Report Builder
description: Turn structured diagnostic findings about a text into a clear editorial report with an overall verdict, section-by-section analysis, priorities, and revision plan
---

## Overview

This Skill converts structured diagnostic findings into a readable editorial report.

Use it when:
- you already have findings from a diagnostic analysis
- you need a long-form human-facing editorial review
- you want a clear overall verdict, not just a list of issues
- you need section-by-section analysis and revision priorities

This Skill is not a diagnostic engine.
It should not invent findings from scratch if structured findings are available.
Its job is to:
- synthesize
- prioritize
- explain
- present clearly

---

## Core Purpose

Transform raw findings into an editorial document that answers:

1. What kind of text is this?
2. What is it trying to do?
3. Does it work?
4. What are its strongest qualities?
5. Where does it break?
6. At what level does it break?
7. What should be fixed first?
8. What should be preserved?

---

## Inputs

Expected inputs may include:

- corpus profile
- mode / genre guess
- segment map
- general verdict
- findings from diagnostic modules
- strengths
- cautions
- priority buckets
- revision plan signals

If findings are incomplete, the Skill may produce a lighter report and must state the limits.

---

## Output Goal

Produce a human-readable editorial report.

The report should be:
- dense
- direct
- readable
- evidence-based
- non-generic
- organized by level

It must not read like:
- AI fluff
- motivational praise
- school feedback
- abstract writing advice

---

## Required Output Sections

### 1. Text Passport
State:
- probable text type
- dominant mode
- whether the corpus is complete or fragmentary
- analysis confidence

### 2. Overall Editorial Verdict
This is mandatory.

Length:
- 120–220 words preferred

It must state:
- what the text is trying to do
- whether it succeeds
- its main strength
- its main weakness
- the depth of the problem
- the likely type of revision needed

This section must read like a real editor’s position, not a bullet list.

---

### 3. Limits of Analysis
State clearly:
- what can be judged confidently
- what is only provisional
- what cannot be judged from the available corpus

---

### 4. AI-Likeness Assessment
If available from diagnostics, summarize:
- main AI-like markers
- counter-markers
- level of suspicion
- confidence
- alternative explanation if needed

Do not present AI-detection as absolute truth.

---

### 5. Core Diagnostic Sections
Depending on the text, include relevant sections such as:

- Structure / movement
- Narrative layer
- Argument layer
- Explanation layer
- Language
- Sentence mechanics
- Paragraph dynamics
- Macro-architecture

Each section should be written as coherent paragraphs, not as dumped findings.

Each section should:
- group related findings
- explain the mechanism
- mention representative evidence
- avoid repeating the same issue in different words

---

### 6. Strengths
This section is mandatory.

It must identify:
- what genuinely works
- why it works
- what should be protected during revision

Do not give empty praise.

---

### 7. False Positive / Caution Zone
If relevant, explain:
- which findings may be genre-dependent
- which may be affected by fragmentariness
- which may be partly stylistic rather than defective

This section exists to prevent overclaiming.

---

### 8. Priority of Revision
Organize the problems by order of repair.

Suggested buckets:
- Rewrite now
- Structural next
- Line edit later
- Cosmetic last

Do not mix major structural issues with minor stylistic polishing.

---

### 9. Revision Plan
Convert priorities into action.

For each major step, explain:
- what to revise
- why it matters
- what effect the revision should produce

This should not be abstract (“improve style”).
It should be concrete (“make the causal transition between X and Y explicit in the middle section”).

---

## Report Style Rules

1. Write in paragraphs, not only bullets.
2. Use bullets only for revision priorities if needed.
3. Avoid generic phrases like:
   - “the text could be improved”
   - “consider being clearer”
   - “make it more engaging”
4. Prefer mechanism:
   - not “weak paragraph”
   - but “the paragraph restates the topic without changing the reader’s understanding”
5. Prefer editorial directness over politeness padding.
6. Do not smooth over contradictions between modules; resolve them or mark uncertainty.
7. Preserve distinction between:
   - structural problem
   - semantic/epistemic problem
   - language problem
   - stylistic preference

---

## Synthesis Rules

When turning findings into prose:

- Do not simply concatenate findings.
- Group by mechanism and level.
- Remove duplicates.
- Identify the dominant failure pattern.
- Identify the dominant strength pattern.

If multiple findings are symptoms of one underlying problem, say so.

Example:
Do not list separately:
- “weak transitions”
- “dead middle”
- “repeated explanation”
if they all stem from:
- lack of structural progression

Instead explain the deeper cause.

---

## What NOT to Do

- Do not invent new major findings that are unsupported
- Do not rewrite the text itself
- Do not produce sentimental encouragement
- Do not make the report symmetrical if the text is asymmetrical
- Do not flatten all issues into the same level of importance
- Do not turn uncertainty into confident tone

---

## Good Output Characteristics

A good report should make a reader feel:
- “I understand what this text is”
- “I understand where it breaks”
- “I understand what to do next”
- “I understand what not to ruin while revising”

---

## Example Behavior (abstract)

Bad:
“The text has some good points, but there are areas for improvement. The structure may need work, and the language could be clearer.”

Good:
“The text has a real center of gravity: it is trying to move from image to insight rather than merely present information. That is its main strength. Its main weakness is not stylistic but structural: the middle sections expand the topic without changing the reader’s understanding, so the text feels intelligent but intermittently static. This is not a sentence-level problem first. It needs a restructuring pass before line editing will matter.”

---

## Resources

If needed, consult:
- FULL_REPORT_TEMPLATE.md
- SHORT_REPORT_TEMPLATE.md
- WHAT_ON_OUTPUT.md
- PRIORITIZATION.md
- FALSE_POSITIVE_GUARD.md
