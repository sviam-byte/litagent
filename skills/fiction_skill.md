# FICTION_SKILL

## Purpose
Диагностика художественного текста как двигателя:
конфликт → изменение → последствия.

---

## Reads
- `docs/fiction/FICTION_MASTER.md`
- `docs/fiction/CHARACTER_AND_RELATIONS.md`
- `docs/fiction/SCENE.md`
- `docs/fiction/PLOT_AND_ARCS.md`
- `docs/fiction/POV.md`
- `docs/fiction/DIALOGUE.md`
- `docs/fiction/FICTION_ARCHITECTURE.md`

---

## Must Decide
- main_conflict
- active_lines
- dead_lines
- arc_presence
- stake_level
- agency_level
- scene_change_pattern
- POV_stability
- dialogue_subtext_level

---

## Must Not Do
- не считать отсутствие внешнего сюжета автоматически дефектом literary fiction
- не трактовать тихую сцену как мёртвую без проверки microtension
- не делать вывод о полной арке по короткому фрагменту без caution

---

## Output Schema
- `module_output`
- `branch_analysis`
- findings преимущественно уровней `structural|scene|semantic`

---

## Severity Rules
- critical: нет мотора / нет конфликта / сцены ничего не меняют
- high: repeated POV breaches / static relationships / exposition scenes
- medium: local dialogue flattening / partial scene weakness
- low: isolated scene drag

---

## Confidence Rules
- high только при повторяющемся паттерне
- medium при нескольких подтверждённых зонах
- low при единичных местах или фрагментарном корпусе

---

## False Positive Rules
- не маркировать «тихую» сцену как мёртвую, пока есть внутреннее движение
- не штрафовать жанровую медленность как structural collapse
- при uncertain segmentation снижать уверенность branch-диагноза

---

## Handoff
Передавать:
- `branch_analysis`
- top_structural_risks
- top_scene_risks
- caution flags
