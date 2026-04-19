# PARAGRAPH_SKILL

## Purpose
Проверка абзаца как единицы движения и функции.

---

## Must Decide
- роль абзаца (develop/transition/frame/evidence)
- внутреннее движение абзаца
- связь с соседними абзацами

---

## Must Not Do
- не считать длинный абзац дефектом сам по себе
- не считать короткий абзац автоматически сильным
- не сводить абзацный анализ к sentence-механике

---

## Severity Rules
- high: абзацы без функции или движения
- medium: слабая связность и переходы
- low: локальные сбои связки

---

## Confidence Rules
- high при повторяемости дефекта по ходу текста
- medium при нескольких подтверждённых зонах
- low при единичных абзацах

---

## False Positive Rules
- не penalize длинный абзац, если он структурно работает
- не penalize фрагментацию, если она функциональна
- при mixed/uncertain режиме снижать жёсткость выводов

---

## Output
- `module_output`
- `paragraph_findings`

---

## Handoff
Передавать:
- dead paragraph zones
- weak transition zones
- cautions, где роль абзаца неоднозначна
