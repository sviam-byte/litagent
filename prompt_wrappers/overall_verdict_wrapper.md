# overall_verdict_wrapper

## Wrapper Purpose
Запустить `overall_verdict_skill` как ранний модуль редакторской позиции.

Этот модуль:
- не ждёт branch/language/sentence/paragraph outputs;
- не должен строить verdict из чужих prose-summary;
- работает на основе текста + compact signal objects.

---

## Injected Docs
- `GENERAL_VERDICT`
- `FALSE_POSITIVE_GUARD`
- `CORE_SYSTEM`
- `DATA_CONTRACTS`

---

## Inputs
- `raw_text`
- `corpus_profile`
- `segment_map`
- `ai_signal`
- `epistemic_signal`
- `propulsion_signal`

---

## Instruction
1. Прочитай только указанные документы.
2. Не используй скрыто накопленный анализ из других модулей.
3. Не жди downstream-модулей: их результаты не входят в твой вход.
4. Работай на основе:
   - текста,
   - ограничений корпуса,
   - карты сегментов,
   - трёх signal objects.
5. Не используй prose-summary от upstream-модулей.
6. Сформируй `general_verdict` как раннюю редакторскую позицию.
7. Verdict должен быть:
   - прозаическим,
   - прямым,
   - конкретным,
   - 5–10 предложений,
   - не превращённым в список микрозамечаний.
8. Если корпус фрагментарный, segmentation uncertain или сигналы противоречат друг другу:
   - снизь confidence,
   - добавь соответствующий caution.

---

## Output
Возвращай `module_output`, где:
- `module_name = "overall_verdict_skill"`
- `summary` — краткая служебная строка
- `findings` — пусто или минимально
- `strengths` — опционально пусто
- `cautions` — при необходимости
- `handoff_notes` — кратко
- главный полезный объект: `general_verdict`

---

## Must Not Do
- Не ссылаться на branch analysis.
- Не ссылаться на language/sentence/paragraph findings.
- Не писать verdict как резюме ещё несуществующего полного разбора.
- Не выдавать уровень уверенности выше, чем позволяют corpus limits.
