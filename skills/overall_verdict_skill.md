# overall_verdict_skill

## Goal
Сформулировать свёрнутую редакторскую позицию до детального разбора.
Не резюмировать замечания, а дать ориентацию:
текст живой или мёртвый, проблема в ядре или отделке, что делать дальше.

## Reads
- GENERAL_VERDICT
- FALSE_POSITIVE_GUARD
- CORE_SYSTEM

## Inputs
- raw_text
- corpus_profile
- segment_map
- ai_findings.summary (from ai_detection_skill)
- claim_map.summary (from epistemic_contract_skill)
- contract_notes.summary (from epistemic_contract_skill)
- energy_map.summary (from propulsion_macro_skill)

## Must Decide
- vitality: alive | partially alive | dead
- problem_depth: core | structural | surface
- recommended_action: rewrite | structural_fix | line_edit | publish_ready
- main_strength: одна конкретная фраза
- main_failure: одна конкретная фраза
- verdict_text: 5–10 предложений прозы

## Must Not Do
- Не перечислять замечания — это не оглавление разбора.
- Не писать более 10 предложений.
- Не хвалить общими фразами ("интересный", "живой").
- Не ругать общими фразами ("слабо", "нужна работа").
- Не использовать информацию из branch/language/sentence модулей
  (они ещё не запускались).
- Не давать уверенность выше, чем оправдывает корпус.

## Output Schema
```json
{
  "module_name": "overall_verdict_skill",
  "summary": "...",
  "general_verdict": {
    "verdict_text": "5–10 предложений",
    "vitality": "alive | partially alive | dead",
    "problem_depth": "core | structural | surface",
    "recommended_action": "rewrite | structural_fix | line_edit | publish_ready",
    "main_strength": "...",
    "main_failure": "...",
    "confidence": 0.0
  },
  "findings": [],
  "strengths": [],
  "cautions": [],
  "unresolved": [],
  "handoff_notes": []
}
```

## Calibration Notes
- Если corpus_profile.is_fragment = true: снизить confidence,
  добавить caution о неполноте корпуса.
- Если ai_findings показывают high suspicion: учитывать в vitality,
  но не делать это единственным основанием.
- Если energy_map показывает stall_zones > 50% текста:
  problem_depth скорее всего structural или core.
