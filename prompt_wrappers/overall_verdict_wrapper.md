# overall_verdict_wrapper

## Wrapper Purpose
Запустить `overall_verdict_skill` с минимально нужным контекстом.
Этот модуль строит редакторскую позицию до детального разбора,
поэтому он не получает branch/language/sentence outputs.

## Injected Docs
- GENERAL_VERDICT
- FALSE_POSITIVE_GUARD
- CORE_SYSTEM (conflict resolution + tone rules)

## Inputs
- raw_text
- corpus_profile
- segment_map
- ai_findings.summary
- claim_map.summary
- contract_notes.summary
- energy_map.summary

## Instruction
1. Прочитай только указанные документы.
2. Не используй скрыто накопленный анализ из других модулей.
3. Не ждй branch/language/sentence — их ещё нет.
4. Работай на основе raw_text + четырёх summary-объектов.
5. Возвращай `module_output` с полем `general_verdict`.
6. Verdict_text — проза, 5–10 предложений, прямо и конкретно.
7. Если корпус фрагментарный — снизь confidence и добавь caution.
