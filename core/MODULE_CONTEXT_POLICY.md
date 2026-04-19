# MODULE_CONTEXT_POLICY

## Goal
Ограничить передачу контекста, чтобы модули не начинали соглашаться
с уже созданным анализом вместо чтения текста.

## Required by Default (all modules)
- raw_text
- corpus_profile
- segment_map
- own docs

## Module-Specific Optional Inputs

### overall_verdict_skill
Receives (summary only):
- ai_detection output → ai_findings.summary
- epistemic_contract output → claim_map.summary + contract_notes.summary
- propulsion_macro output → energy_map.summary

Does NOT receive:
- branch_analysis
- language_findings
- sentence_findings
- paragraph_findings

### nonfiction_skill
May receive:
- epistemic_contract output (claim_map only)

### synthesis_guard_skill
Receives (selective):
- ai_findings
- branch_analysis summary
- language_findings
- sentence_findings
- paragraph_findings
- energy_map

Does NOT receive:
- general_verdict (to avoid circular confirmation)

### revision_plan_skill
Receives:
- all module summaries (structured, not prose)
- general_verdict
- strengths
- cautions

## Forbidden by Default
- cumulative prose summary of all previous modules
- final diagnosis text from another module
- full dump of unrelated findings

## Rule
Если есть сомнение, передавать меньше.
Prose summary от другого модуля — всегда запрещён.
Только структурированные поля.
