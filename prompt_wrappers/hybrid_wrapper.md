# hybrid_wrapper

## Wrapper Purpose
Запустить `hybrid_skill` с минимально нужным контекстом.

## Injected Docs
- HYBRID_MASTER
- MODE_BALANCE
- NARRATIVE_NONFICTION
- ESSAY
- MEMOIR

## Inputs
- raw_text
- corpus_profile
- segment_map


## Instruction
1. Прочитай только указанные документы.
2. Не используй скрыто накопленный анализ.
3. Работай только в пределах своего слоя.
4. Возвращай `module_output`.
5. Для critical/high finding нужен evidence span.
