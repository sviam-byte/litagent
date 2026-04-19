# OVERALL_VERDICT_SKILL

## Purpose
Сформулировать раннюю редакторскую позицию о тексте как целом.

Этот модуль:
- не резюмирует поздние находки;
- не читает branch/language/sentence/paragraph prose;
- опирается на `raw_text` + compact signals.

---

## Reads
- `core/GENERAL_VERDICT.md`
- `core/FALSE_POSITIVE_GUARD.md`
- `core/CORE_SYSTEM.md`
- `core/DATA_CONTRACTS.md`

---

## Inputs
- `raw_text`
- `corpus_profile`
- `segment_map`
- `ai_signal`
- `epistemic_signal`
- `propulsion_signal`

---

## Must Decide
- vitality: `alive | partially_alive | dead`
- problem_depth: `core | structural | surface`
- recommended_action: `rewrite | structural_fix | line_edit | publish_ready`
- what-mostly-works (1 concise statement)
- what-mostly-fails (1 concise statement)
- final `general_verdict` in 5–10 sentences

---

## Must Not Do
- не ссылаться на branch/language/sentence/paragraph outputs;
- не строить вывод как список микродефектов;
- не повышать confidence выше corpus limits;
- не превращать ai-suspicion в единственное основание verdict.

---

## Output Schema
- `module_output`
- `general_verdict` (по `general_verdict.schema.json`)
- `findings` может быть пустым или минимальным
- `handoff_notes` короткие, структурные

---

## Confidence Rules
- high только если сигналы согласованы и корпус нефрагментарный
- medium при частичной согласованности сигналов
- low при fragment/uncertain segmentation/конфликте сигналов

---

## False Positive Rules
- высокий ai suspicion не является доказательством «мёртвого текста» сам по себе
- при uncertain segment routing избегать жёстких жанровых утверждений
- при thin evidence снижать confidence и добавлять caution

---

## Handoff
Передавать downstream:
- 1–2 `handoff_notes` про главный риск и главный актив
- caution, если confidence ограничен корпусом/сегментацией/конфликтом сигналов
