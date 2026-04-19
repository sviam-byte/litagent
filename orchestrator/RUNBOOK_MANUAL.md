# RUNBOOK_MANUAL

## Manual Use (Step by Step)

### Step 1. Intake
Запусти `intake_router_skill`.
Проверь паспорт и segment_map.
Если dominant_mode uncertain — не форсируй ветку.

### Step 2–4. Early Independent Checks
Запусти последовательно:
- ai_detection_skill
- epistemic_contract_skill
- propulsion_macro_skill

Каждый получает только: raw_text + corpus_profile + segment_map + свои docs.
Не передавай им выводы друг друга.

### Step 5. General Verdict ← NEW
Запусти `overall_verdict_skill`.

Получает:
- raw_text + corpus_profile + segment_map
- ai_findings.summary
- claim_map.summary + contract_notes.summary
- energy_map.summary

НЕ получает: branch/language/sentence findings (их ещё нет).

Результат — 5–10 предложений прямой редакторской позиции.
Это второй раздел финального отчёта.

### Step 6. Genre Branch
Выбери fiction / nonfiction / hybrid по segment_map.
Для hybrid с выраженными сегментами разных типов —
можно запустить два модуля на разных сегментах.

### Steps 7–9. Language Passes
- language_skill
- sentence_skill
- paragraph_skill

Каждый читает raw_text независимо.
Не передавай им общий накопленный анализ.

### Step 10. Synthesis Guard
Запусти `synthesis_guard_skill`.

Получает выборочно:
- ai_findings
- branch_analysis summary
- language/sentence/paragraph findings
- energy_map

НЕ получает general_verdict (чтобы не подтверждать его рефлексивно).

### Step 11. Revision Plan
Запусти `revision_plan_skill`.

Получает: все module summaries + general_verdict + strengths + cautions.
Строит: priority_buckets + revision_plan + final_report.

---

## Manual Quality Check (Before Finalizing)
Перед финалом проверь:
- [ ] Есть ли general_verdict на месте 2?
- [ ] Написан ли он прозой (не списком)?
- [ ] Есть ли corpus limits?
- [ ] Есть ли strengths?
- [ ] Нет ли дублей одной проблемы в трёх разделах?
- [ ] Есть ли evidence для critical/high findings?
- [ ] Привязан ли план ревизии к диагностике?

---

## Output Modes
- **Full Diagnostic Mode** — все 14 разделов.
- **Short Editor Mode** — паспорт + general_verdict + 3–5 проблем + 3–5 strengths + ИИ-сводка + порядок правки.
- **Module Debug Mode** — structured outputs модулей без финального синтеза.
- **API Mode** — только JSON по final_report.schema.json.
