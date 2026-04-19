# revision_plan_wrapper

## Wrapper Purpose
Запустить `revision_plan_skill` с минимально нужным контекстом.

## Injected Docs
- PRIORITIZATION
- OUTPUT_CONTRACT
- QUALITY_GATES

## Inputs
- raw_text
- corpus_profile
- segment_map
- selected upstream outputs

## Instruction
1. Прочитай только указанные документы.
2. Не используй скрыто накопленный анализ.
3. Работай только в пределах своего слоя.
4. Возвращай `module_output`.
5. Для critical/high finding нужен evidence span.
