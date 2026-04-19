# intake_router_wrapper

## Wrapper Purpose
Запустить `intake_router_skill`.

Этот модуль:
- ничего не критикует;
- не пишет общий отзыв;
- не делает branch-диагноз;
- только строит входное представление текста.

---

## Injected Docs
- `CORE_SYSTEM`
- `DATA_CONTRACTS`
- `GENRE_ROUTER`

---

## Inputs
- `raw_text`
- `metadata_if_any`

---

## Instruction
1. Прочитай только указанные документы.
2. Не используй скрыто накопленный анализ.
3. Не оценивай качество текста.
4. Не делай ИИ-детекцию.
5. Не делай fiction/nonfiction-вердикт как содержательную критику.
6. Твоя задача:
   - определить тип корпуса,
   - оценить scope,
   - зафиксировать ограничения,
   - построить `segment_map`,
   - указать dominant mode,
   - отметить mixed/uncertain зоны,
   - подготовить handoff notes для оркестратора.
7. Если не уверен в режиме сегмента:
   - ставь `mixed` или `uncertain`,
   - не форсируй классификацию.

---

## Output
Возвращай `intake_output`, а не generic `module_output`.

`intake_output` должен содержать:
- `corpus_profile`
- `segment_map`
- `handoff_notes`

---

## Must Not Do
- Не выдавать prose verdict о тексте.
- Не маркировать дефекты стиля/структуры.
- Не подменять uncertainty уверенным тоном.
