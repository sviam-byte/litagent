# nonfiction_wrapper

## Wrapper Purpose
Запустить `nonfiction_skill` с минимально нужным контекстом.

## Injected Docs
- NONFICTION_MASTER
- THESIS_AND_ARGUMENT
- EXPLANATION
- SOURCING_AND_EVIDENCE
- NONFICTION_PERSONA
- TRUTH_CONTRACT
- SUMMARY_QUOTE_RESPONSE
- NONFICTION_ARCHITECTURE

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
