# QUALITY_GATES

Финальный отчёт не считается готовым, если нарушен хотя бы один gate:

## Contract Gates
- Все обязательные разделы присутствуют согласно `OUTPUT_CONTRACT` и schema.
- Нет лишних полей в schema-строгих объектах (`additionalProperties: false`).
- High/Critical findings имеют mechanism + evidence_spans + revision_implication.

## Evidence Gates
- Критические и high-выводы подтверждены evidence spans.
- Для спорных мест указан false_positive_risk.
- При thin evidence выставлен caution и снижен confidence.

## Context Gates
- Между модулями не передавалась prose-summary цепочка.
- Downstream-модули не строят вывод на чужом verdict prose.
- Для overall_verdict использованы только signals + raw_text.

## Revision Gates
- `priorities` причинно упорядочены.
- `revision_plan` привязан к findings/risks.
- `preserve` защищает подтверждённые strengths.
