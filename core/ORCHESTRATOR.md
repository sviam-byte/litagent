# ORCHESTRATOR

## Role
Оркестратор управляет запуском 12 несущих модулей так, чтобы:
- анализ шёл от определения режима к критике;
- модули не переиспользовали чужую прозу;
- ранний `general_verdict` строился на тексте и сигналах, а не на горе поздних замечаний;
- финальный отчёт собирался из structured outputs.

---

## Core Responsibilities
Оркестратор обязан:
- запускать модули в правильном порядке;
- передавать минимально нужный контекст;
- маршрутизировать текст по branch-веткам;
- не допускать context bloat;
- применять conflict resolution;
- собирать final report по `OUTPUT_CONTRACT`.

---

## Execution Order

### Stage 1 — Intake
1. `intake_router_skill`
   Output:
   - `corpus_profile`
   - `segment_map`
   - `handoff_notes`

### Stage 2 — Early Independent Passes
2. `ai_detection_skill`
   Output:
   - `ai_findings`
   - `ai_signal`

3. `epistemic_contract_skill`
   Output:
   - `claim_map`
   - `contract_notes`
   - `epistemic_signal`

4. `propulsion_macro_skill`
   Output:
   - `energy_map`
   - `macro_notes`
   - `propulsion_signal`

### Stage 3 — Early Editorial Position
5. `overall_verdict_skill`
   Input:
   - `raw_text`
   - `corpus_profile`
   - `segment_map`
   - `ai_signal`
   - `epistemic_signal`
   - `propulsion_signal`

   Output:
   - `general_verdict`

### Stage 4 — Branch Analysis
6. One or more of:
- `fiction_skill`
- `nonfiction_skill`
- `hybrid_skill`

Output:
- `branch_analysis`

### Stage 5 — Language Layers
7. `language_skill`
   Output:
   - `language_findings`

8. `sentence_skill`
   Output:
   - `sentence_findings`

9. `paragraph_skill`
   Output:
   - `paragraph_findings`

### Stage 6 — Guard and Synthesis Support
10. `synthesis_guard_skill`
    Output:
    - `strengths`
    - `cautions`
    - `conflict_notes`

### Stage 7 — Final Planning
11. `revision_plan_skill`
    Output:
    - `priorities`
    - `revision_plan`
    - `final_report_draft`

---

## Why overall_verdict_skill Runs Early
`general_verdict` должен появляться рано, потому что:
- это не резюме всех замечаний;
- это редакторская позиция о тексте как целом;
- если строить его в конце, он деградирует в конспект найденных дефектов.

К шагу 5 уже известны:
- тип корпуса и ограничения;
- карта режимов;
- ИИ-сигналы;
- эпистемический и контрактный слой;
- пропульсия и макровес.

Этого достаточно для честной ранней позиции.

---

## Branching Rule
Branch routing определяется:
- `corpus_profile`
- `segment_map`
- `handoff_notes` from intake

### If dominant mode == fiction
Run:
- `fiction_skill` on full text
or on routed segments if intake says text is segmented/mixed.

### If dominant mode == nonfiction
Run:
- `nonfiction_skill` on full text
or on routed segments if necessary.

### If dominant mode == hybrid
Run:
- `hybrid_skill` on full text

Additionally:
if `segment_map` shows stable fiction-like and nonfiction-like zones,
the orchestrator may run:
- `fiction_skill` on fiction-heavy segments
- `nonfiction_skill` on nonfiction-heavy segments

### If dominant mode == uncertain
Run:
- `hybrid_skill` in soft mode

And:
- add caution
- do not hard-assert genre-specific defects

---

## No-Prose-Handoff Rule
Ни один модуль не передаёт другому модулю prose-summary как транспортный формат.

Specifically:
- `overall_verdict_skill` receives only signals, not summaries
- branch modules do not receive verdict prose
- line-level modules do not receive branch prose
- revision module receives structured outputs and `general_verdict`, not a chain of summaries

---

## Conflict Resolution
Оркестратор применяет иерархию:

`corpus limits > structural > semantic/epistemic > language > style`

Следствия:
- structural finding cannot be neutralized by a stylistic preference
- caution from insufficient corpus can downgrade certainty of branch conclusions
- segmentation uncertainty can soften branch findings
- false-positive risk can downgrade, but not erase, a well-evidenced structural issue

---

## Evidence Discipline
Оркестратор должен reject или downgrade finding, если:
- нет evidence span;
- нет mechanism;
- нет revision implication для high/critical issue.

---

## Final Assembly Rule
Финальный отчёт собирается из:
- `passport`
- `general_verdict`
- `limits`
- `ai_detection`
- `contract`
- `branch_analysis`
- `language`
- `sentence`
- `paragraph`
- `macro`
- `strengths`
- `false_positive_risks`
- `priorities`
- `revision_plan`

Если хотя бы один обязательный раздел отсутствует, final report is incomplete.

---

## Manual Override Rule
Если система используется вручную, оператор может:
- отключить отдельный модуль,
- заменить hard routing на mixed mode,
- задать branch manually,
но обязан оставить trace:
- why override
- what changed
- what confidence impact follows
