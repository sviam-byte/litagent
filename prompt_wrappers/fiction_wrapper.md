# fiction_wrapper

## Wrapper Purpose
Запустить `fiction_skill` с минимально нужным контекстом.

## Injected Docs
- FICTION_MASTER
- PLOT_AND_ARCS
- CHARACTER_AND_RELATIONS
- SCENE
- POV
- DIALOGUE
- SUBTEXT_AND_MICROTENSION
- FICTION_ARCHITECTURE
- DETAIL_AND_EMBODIMENT

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
