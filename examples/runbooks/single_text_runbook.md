# Runbook: Manual Single-Text Analysis

Пошаговая инструкция для ручного запуска системы на одном тексте.

## Подготовка
1. Определи режим вывода: full | short | debug | api.
2. Убедись, что у тебя есть raw_text.
3. Если есть метаданные (жанр, аудитория, этап работы) — подготовь.

---

## Шаг 1. Intake
**Файлы:** CORE_SYSTEM, DATA_CONTRACTS, GENRE_ROUTER
**Промпт:** intake_router_wrapper

Что получить:
```json
{
  "corpus_profile": { ... },
  "segment_map": { "segments": [...] },
  "handoff_notes": [...]
}
```

Проверь:
- dominant_mode понятен или помечен uncertain?
- is_fragment = true? → снизь ожидания от макровыводов.

---

## Шаг 2. AI Detection
**Файлы:** AI_DETECTION, FALSE_POSITIVE_GUARD
**Промпт:** ai_detection_wrapper

Inputs: raw_text + corpus_profile + segment_map

Сохрани: ai_findings (будет нужен для overall_verdict как summary).

---

## Шаг 3. Epistemic + Contract
**Файлы:** EPISTEMIC_AND_CONTRACT, EVIDENCE_POLICY
**Промпт:** epistemic_contract_wrapper

Inputs: raw_text + corpus_profile + segment_map

Сохрани: claim_map.summary + contract_notes.summary.

---

## Шаг 4. Propulsion + Macro
**Файлы:** PROPULSION_AND_MACRO
**Промпт:** propulsion_macro_wrapper

Inputs: raw_text + corpus_profile + segment_map

Сохрани: energy_map.summary.

---

## Шаг 5. Overall Verdict ← КРИТИЧЕСКИЙ ШАГ
**Файлы:** GENERAL_VERDICT, FALSE_POSITIVE_GUARD, CORE_SYSTEM
**Промпт:** overall_verdict_wrapper

Inputs:
- raw_text + corpus_profile + segment_map
- ai_findings.summary
- claim_map.summary + contract_notes.summary
- energy_map.summary

НЕ передавай: branch/language/sentence findings (их ещё нет).

Результат: general_verdict — второй раздел финального отчёта.

Проверь:
- Это 5–10 предложений прозы, не список?
- Есть vitality + problem_depth + recommended_action?
- Нет пустых похвал?

---

## Шаг 6. Genre Branch
По dominant_mode из corpus_profile:
- fiction → fiction_wrapper
- nonfiction → nonfiction_wrapper
- hybrid → hybrid_wrapper
- uncertain → hybrid_wrapper в мягком режиме

Inputs: raw_text + corpus_profile + segment_map

---

## Шаги 7–9. Language Passes
Запускай последовательно, каждый независимо:

**Шаг 7:** language_wrapper (LANGUAGE_PATHOLOGIES, REGISTER_AND_TONE, METAPHOR_AND_ABSTRACTION, RHYTHM_AND_SOUND)
**Шаг 8:** sentence_wrapper (SENTENCE_MECHANICS, RHYTHM_AND_SOUND)
**Шаг 9:** paragraph_wrapper (PARAGRAPH_DYNAMICS, COHESION_AND_TRANSITIONS)

Inputs каждого: raw_text + corpus_profile + segment_map

---

## Шаг 10. Synthesis Guard
**Файлы:** STRENGTHS, FALSE_POSITIVE_GUARD, CONFLICT_PLAYBOOK
**Промпт:** synthesis_guard_wrapper

Inputs (выборочно):
- raw_text + corpus_profile + segment_map
- ai_findings, branch_analysis summary
- language/sentence/paragraph findings
- energy_map

НЕ передавай: general_verdict

---

## Шаг 11. Revision Plan
**Файлы:** PRIORITIZATION, OUTPUT_CONTRACT, QUALITY_GATES
**Промпт:** revision_plan_wrapper

Inputs: все module summaries + general_verdict + strengths + cautions

Результат: финальный отчёт.

---

## Финальная проверка (Quality Gates)
- [ ] general_verdict стоит вторым?
- [ ] Написан прозой, 5–10 предложений?
- [ ] Есть corpus limits?
- [ ] Есть strengths?
- [ ] Нет дублей одной проблемы в 3 разделах?
- [ ] Есть evidence для critical findings?
- [ ] Revision plan привязан к диагностике?
