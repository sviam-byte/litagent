# ORCHESTRATOR

## Role
Управлять запуском 13 модулей, не допуская контекстного распухания
и самоподтверждающейся аналитики.

## Responsibilities
- запускать модули в правильном порядке;
- передавать минимально нужный контекст;
- собирать structured outputs;
- резолвить конфликты по CONFLICT_PLAYBOOK;
- не давать поздним модулям жить на одних чужих выводах;
- собирать final report по ORDER ниже.

## Execution Order
1. intake_router_skill          → corpus_profile + segment_map
2. ai_detection_skill           → ai_findings
3. epistemic_contract_skill     → claim_map + contract_notes
4. propulsion_macro_skill       → energy_map + macro_notes
5. overall_verdict_skill        → general_verdict ← строится здесь, рано
6. fiction_skill
   OR nonfiction_skill
   OR hybrid_skill              → branch_analysis
7. language_skill               → language_findings
8. sentence_skill               → sentence_findings
9. paragraph_skill              → paragraph_findings
10. synthesis_guard_skill       → strengths + cautions + conflict_notes
11. revision_plan_skill         → priorities + revision_plan

## Why overall_verdict_skill Runs at Step 5
К этому моменту известны:
- корпус и его ограничения (intake);
- признаки машинности (ai_detection);
- эпистемический и контрактный статус (epistemic_contract);
- распределение энергии и макровес (propulsion_macro).

Этого достаточно для позиции. Ждать конца пайплайна — значит
строить отзыв на всех замечаниях, что превращает его в их резюме.

## Branching Rule
- fiction / nonfiction / hybrid выбирается не один раз на весь текст,
  а может уточняться по segment_map.
- Если segment_map содержит mixed/uncertain сегменты, ветка запускается
  в мягком режиме: не форсировать жёсткое разделение.
- Для hybrid-текстов с выраженными fiction и nonfiction сегментами
  допускается запуск двух веток на разных сегментах.

## Context Policy for overall_verdict_skill
Получает:
- raw_text
- corpus_profile
- segment_map
- ai_detection output (summary only)
- epistemic_contract output (summary only)
- propulsion_macro output (summary only)
- GENERAL_VERDICT doc
- FALSE_POSITIVE_GUARD doc

Не получает:
- branch_analysis
- language_findings
- sentence_findings
- paragraph_findings
