# language_wrapper

## Wrapper Purpose
Запустить `language_skill` с минимально нужным контекстом.

## Injected Docs
- LANGUAGE_PATHOLOGIES
- REGISTER_AND_TONE
- METAPHOR_AND_ABSTRACTION
- RHYTHM_AND_SOUND

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
