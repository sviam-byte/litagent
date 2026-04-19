# REVISION_PLAN_SKILL

## Purpose
Перевести диагностику в причинно-обоснованный план правки.

---

## Must Decide
- что ломает текст сильнее всего
- что чинится быстрее всего без побочного ущерба
- что нельзя трогать (protect list)

---

## Must Not Do
- не переписывать текст за автора
- не давать абстрактные советы
- не дублировать findings без приоритизации

---

## Output Structure

### priorities
- rewrite_now
- structural_next
- line_edit_later
- cosmetic_last

### revision_plan
- first_pass
- second_pass
- preserve

---

## Severity Rules
- high/critical findings уходят в `rewrite_now` или `structural_next`
- medium — преимущественно в `line_edit_later`
- low — в `cosmetic_last`, если не образуют паттерн

---

## Confidence Rules
- high только если опора на повторяющиеся findings
- medium при смешанной картине
- low при fragment/uncertain + thin evidence

---

## False Positive Rules
- не поднимать приоритет пункта с высоким false_positive_risk без cross-evidence
- спорные stylistic замечания не ставить выше структурных поломок
- при конфликте модулей фиксировать caution и смещать в later pass

---

## Rules
- каждый пункт должен быть привязан к findings (IDs)
- порядок должен быть причинно обоснован
- preserve должен защищать подтверждённые strengths

---

## Handoff
Передавать:
- ordering rationale
- risk notes для спорных пунктов
- preserve list для безопасной ревизии

---

## Example (abstract)

BAD:
“улучшить стиль”

GOOD:
“убрать абстрактные существительные в seg_03–seg_05 → повысить ясность аргумента”
