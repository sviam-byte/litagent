# DATA_CONTRACTS

## Purpose
Этот документ задаёт единый контракт данных для всех модулей системы.

Главный принцип:
между модулями передаются не prose-summary и не “мини-эссе”, а
структурированные объекты, пригодные для оркестрации, проверки и сборки.

## General Rule
Каждый модуль возвращает структурированный объект.

Свободный текст допускается только:
- в human-facing `summary` внутри собственного `module_output`;
- в `general_verdict`;
- в финальном human-facing report.

Межмодульная передача prose-summary запрещена.

---

## Core Objects

### corpus_profile
Обязательные поля:
- `corpus_type`
- `estimated_scope`
- `is_fragment`
- `word_count_estimate`
- `analysis_limits[]`
- `confidence`

### segment_map
Обязательные поля:
- `segments[]`

Каждый сегмент:
- `id`
- `start_anchor`
- `end_anchor`
- `mode`
- `confidence`
- `notes`

Allowed modes:
- `scene`
- `summary`
- `exposition`
- `argument`
- `reflection`
- `dialogue`
- `description`
- `mixed`
- `uncertain`

### finding
Обязательные поля:
- `id`
- `module`
- `level`
- `category`
- `description`
- `mechanism`
- `evidence_spans[]`
- `severity`
- `confidence`
- `revision_implication`
- `false_positive_risk`

Allowed levels:
- `corpus-limit`
- `structural`
- `semantic`
- `epistemic`
- `scene`
- `paragraph`
- `sentence`
- `language`
- `style`
- `copy`

Allowed severity:
- `low`
- `medium`
- `high`
- `critical`

Allowed confidence:
- `low`
- `medium`
- `high`

### strengths_item
Обязательные поля:
- `level`
- `description`
- `mechanism`
- `evidence_spans[]`
- `protect_in_revision`
- `confidence`

### caution_item
Обязательные поля:
- `type`
- `description`
- `related_finding_ids[]`
- `impact_on_confidence`

Allowed types:
- `insufficient_corpus`
- `genre_exception`
- `taste_only`
- `possible_false_positive`
- `segmentation_uncertain`
- `evidence_too_thin`

### module_output
Обязательные поля:
- `module_name`
- `summary`
- `findings[]`
- `strengths[]`
- `cautions[]`
- `unresolved[]`
- `handoff_notes[]`

`summary` — human-facing и не должен автоматически передаваться downstream-модулям.

---

## Signal Objects
Для ранних модулей и некоторых точек синтеза допускаются компактные signal-объекты.

### ai_signal
Обязательные поля:
- `suspicion_level`
- `top_markers[]`
- `top_counter_markers[]`
- `confidence`

### epistemic_signal
Обязательные поля:
- `overclaim_count`
- `underclaim_count`
- `dominant_statuses[]`
- `contract_mismatch_count`
- `confidence`

### propulsion_signal
Обязательные поля:
- `opening_strength`
- `stall_zone_count`
- `disproportion_zone_count`
- `ending_strength`
- `confidence`

Allowed strength values:
- `low`
- `medium`
- `high`

---

## Context Minimization Rule
Каждый модуль получает только:
- `raw_text`
- `corpus_profile`
- `segment_map`
- профильные документы
- строго необходимые upstream-объекты

По умолчанию запрещено передавать:
- prose-summary от других модулей
- финальные вердикты других модулей
- полный накопленный анализ
- dump нерелевантных findings

---

## Handoff Rule
Если модуль хочет повлиять на downstream-работу, он делает это через:
- `findings`
- `cautions`
- `handoff_notes`
- `signal objects`

А не через narrative-recap.

### Good handoff
- `seg_04 is mixed, do not hard-route as pure scene`
- `high overclaim density in middle section`
- `possible false positive: stylized sterility`

### Bad handoff
- длинный абзац “в целом текст выглядит так-то”

---

## Summary Rule
`summary` существует для:
- человека;
- финального отчёта;
- локального чтения модуля.

`summary` не является транспортным форматом между модулями.

---

## Evidence Rule
Каждый high/critical finding обязан иметь:
- `mechanism`
- `evidence_spans[]`
- `revision_implication`

Если этого нет, finding должен быть downgraded по severity или confidence.

---

## Uncertainty Rule
Если:
- корпус фрагментарный,
- сегментация uncertain,
- evidence thin,
то модуль обязан:
- снизить confidence;
- добавить caution;
- не эскалировать вывод в жёсткий диагноз.
