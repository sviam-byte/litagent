# DATA_CONTRACTS

## General Rule
Каждый модуль возвращает структурированный объект. Свободный текст допускается только в `summary`.

## Core Objects

### corpus_profile
- corpus_type
- estimated_scope
- is_fragment
- word_count_estimate
- analysis_limits[]
- confidence

### segment_map
Each segment:
- id
- start_anchor
- end_anchor
- mode
- confidence
- notes

Allowed modes:
- scene
- summary
- exposition
- argument
- reflection
- dialogue
- description
- mixed
- uncertain

### finding
- id
- module
- level
- category
- description
- mechanism
- evidence_spans[]
- severity
- confidence
- revision_implication
- false_positive_risk

### strengths_item
- level
- description
- mechanism
- evidence_spans[]
- protect_in_revision
- confidence

### caution_item
- type
- description
- related_finding_ids[]
- impact_on_confidence

### module_output
- module_name
- summary
- findings[]
- strengths[]
- cautions[]
- unresolved[]
- handoff_notes[]

## Context Minimization
Каждый модуль получает только обязательные входы.
Upstream-данные передаются только через структурированные поля.
