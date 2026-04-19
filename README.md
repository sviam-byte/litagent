# Editor Agent Full v5

Полноценная библиотека для многошагового ИИ-агента редакторского анализа.

## Что внутри
- `core/` — базовые правила системы
- `docs/` — операциональные справочники по веткам анализа
- `skills/` — 13 несущих skill-спеков
- `schemas/` — JSON-схемы входов и выходов
- `orchestrator/` — документы для сборки оркестратора
- `outputs/` — пакет «что агент обязан выдавать»
- `prompt_wrappers/` — шаблоны обвязки для отдельных вызовов
- `examples/` — примеры JSON и markdown-отчётов

---

## Главное изменение v5 относительно v4

### Добавлен «Общий отзыв» (general_verdict)
Это свёрнутая редакторская позиция — **второй раздел** любого отчёта,
до детального разбора по слоям.

Без него пользователь получал 30–40 замечаний, но не понимал:
- текст живой или мёртвый?
- проблема в ядре или в отделке?
- нужен rewrite или локальная правка?
- что уже работает?

Общий отзыв — это 5–10 предложений прямой редакторской прозы:
что текст пытается делать, получается ли это, главная сила,
главная поломка, глубина проблемы, что делать дальше.

### Новый модуль: overall_verdict_skill (шаг 5)
Запускается после ранних независимых проверок (ai_detection,
epistemic_contract, propulsion_macro), но **до** жанровой ветки
и языкового прохода.

Это принципиально: общий отзыв не должен быть резюме замечаний —
он должен быть позицией, построенной на первом чтении текста.

### Наполнены тощие docs
В v4 ряд документов были заглушками (228–259 байт).
В v5 полноценные операциональные тексты:
- `PARAGRAPH_DYNAMICS.md` — функции абзацев, дефекты, тест переупорядочивания
- `RHYTHM_AND_SOUND.md` — механика ритма, каденция, pressure modulation
- `LANGUAGE_PATHOLOGIES.md` — 15 категорий с механизмами
- `SENTENCE_MECHANICS.md` — каркас фразы, ударная позиция, минимальные пары
- `COHESION_AND_TRANSITIONS.md` — old-to-new flow, топиковые цепочки, типы переходов
- `METAPHOR_AND_ABSTRACTION.md` — когда метафора работает, когда ломает
- `REGISTER_AND_TONE.md` — регистровый дрейф, faux-neutrality, tone as argument
- `FICTION_MASTER.md`, `NONFICTION_MASTER.md`, `HYBRID_MASTER.md` — расширены
- `SUBTEXT_AND_MICROTENSION.md`, `DETAIL_AND_EMBODIMENT.md` — расширены

### Исправлен EXECUTION_GRAPH
Добавлено явное ветвление по segment_map для mixed/uncertain сегментов.
Прописан soft mode для uncertain доминанты.

### Исправлен MODULE_CONTEXT_POLICY
Явно описано, какие inputs получает overall_verdict_skill
и что synthesis_guard_skill не получает general_verdict.

---

## 13 несущих навыков
1. intake_router_skill
2. ai_detection_skill
3. epistemic_contract_skill
4. propulsion_macro_skill
5. **overall_verdict_skill** ← NEW
6. fiction_skill
7. nonfiction_skill
8. hybrid_skill
9. language_skill
10. sentence_skill
11. paragraph_skill
12. synthesis_guard_skill
13. revision_plan_skill

---

## Базовый пайплайн
1. intake / passport / segmentation
2. ai-detection
3. epistemic + contract
4. propulsion + macro outline
5. **general_verdict** ← NEW: строится здесь, не в конце
6. genre branch (fiction | nonfiction | hybrid)
7. language
8. sentence
9. paragraph + cohesion
10. guard / strengths / false positives
11. prioritization + revision plan

---

## Порядок разделов в отчёте

### Full Report
1. Паспорт текста
2. **Общий отзыв** ← второй, всегда
3. Ограничения вывода
4. ИИ-детекция
5. Контракт с читателем
6. Branch analysis
7. Язык
8. Фраза
9. Абзац и переходы
10. Макроархитектура
11. Сильные стороны
12. Ложноположительные риски
13. Приоритеты правки
14. План ревизии

### Short Report
1. Паспорт текста
2. **Общий отзыв** ← второй, всегда
3. 3–5 главных проблем
4. 3–5 сильных сторон
5. ИИ-детекция (сводка)
6. Порядок правки

---

## Главный принцип (не изменился)
Ни один модуль не получает весь накопленный анализ.
Каждый модуль получает только:
- raw_text
- corpus_profile
- segment_map
- профильные документы
- строго нужные upstream-объекты (structured, not prose)
