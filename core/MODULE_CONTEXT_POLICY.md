# MODULE_CONTEXT_POLICY

## Goal
Ограничить передачу контекста так, чтобы:
- модули читали текст, а не чужие интерпретации текста;
- поздние модули не “соглашались сами с собой”;
- синтез строился на structured signals, а не на цепочке prose-summary.

---

## Required by Default (all modules)
Каждый модуль по умолчанию получает:
- `raw_text`
- `corpus_profile`
- `segment_map`
- собственные профильные документы

---

## Optional Inputs by Module

### ai_detection_skill
May receive:
- nothing beyond default

Must NOT receive:
- branch analysis
- language analysis
- verdict prose
- revision priorities

### epistemic_contract_skill
May receive:
- nothing beyond default

Must NOT receive:
- ai verdict prose
- branch analysis
- line-level language findings

### propulsion_macro_skill
May receive:
- nothing beyond default

Must NOT receive:
- prose verdicts from upstream modules

### overall_verdict_skill
Receives:
- `raw_text`
- `corpus_profile`
- `segment_map`
- `ai_signal`
- `epistemic_signal`
- `propulsion_signal`
- `GENERAL_VERDICT`
- `FALSE_POSITIVE_GUARD`
- `CORE_SYSTEM`

Does NOT receive:
- `branch_analysis`
- `language_findings`
- `sentence_findings`
- `paragraph_findings`
- prose summaries from any module

### fiction_skill
May receive:
- `epistemic_signal` only if hybrid ambiguity affects interpretation
- relevant segment subset if routed by segment

Must NOT receive:
- overall verdict prose
- language verdict prose

### nonfiction_skill
May receive:
- `epistemic_signal`
- relevant segment subset if routed by segment

Must NOT receive:
- overall verdict prose
- language verdict prose

### hybrid_skill
May receive:
- `epistemic_signal`
- `propulsion_signal`

Must NOT receive:
- overall verdict prose
- downstream language findings

### language_skill
May receive:
- `branch mode label` only
- selected route notes such as `dominant_mode=fiction|nonfiction|hybrid`
- `segment_map`

Must NOT receive:
- branch verdict prose
- revision plan
- general verdict prose

### sentence_skill
May receive:
- `segment_map`
- selected route label if needed

Must NOT receive:
- language prose summary
- overall verdict prose

### paragraph_skill
May receive:
- `segment_map`
- selected route label if needed

Must NOT receive:
- sentence prose summary
- overall verdict prose

### synthesis_guard_skill
Receives:
- selected structured outputs from:
  - `ai_detection_skill`
  - `fiction/nonfiction/hybrid`
  - `language_skill`
  - `sentence_skill`
  - `paragraph_skill`
  - `propulsion_macro_skill`
- no prose-summary from upstream modules
- no `general_verdict` prose

### revision_plan_skill
Receives:
- `general_verdict`
- selected structured branch outputs
- selected structured language outputs
- `strengths`
- `cautions`
- `conflict_notes`

Receives only structured objects, not cumulative prose recaps.

---

## Forbidden by Default
По умолчанию запрещено передавать:
- cumulative prose summary of all previous modules
- human-facing `summary` fields from upstream modules
- final diagnosis text from another module
- branch verdict prose into line-level modules
- line-level verdict prose into structural modules

---

## No-Prose-Handoff Rule
Между модулями не ходит prose-summary.

Если модулю нужно передать downstream-сигнал, он делает это через:
- finding
- caution
- handoff note
- signal object

---

## Minimal Context Rule
Если есть сомнение, передавать меньше.

Контекст добавляется только если:
1. он реально нужен для решения;
2. без него модуль ошибётся;
3. этот контекст можно передать структурированно.

---

## Mixed/Uncertain Rule
Если `segment_map` содержит `mixed` или `uncertain`, downstream-модуль обязан:
- не делать жёстких жанровых выводов;
- добавить caution;
- при необходимости снизить confidence.

---

## Anti-Cascade Rule
Ранняя ошибка не должна автоматически становиться истиной для всех downstream-модулей.

Поэтому:
- segmentation uncertain → caution, not hard routing
- ai suspicion high → not proof
- early verdict → not authority for branch/language modules
