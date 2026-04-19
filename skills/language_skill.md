# LANGUAGE_SKILL

## Purpose
Диагностика языка как системы переноса смысла.

---

## Reads
- `docs/language/LANGUAGE_PATHOLOGIES.md`
- `docs/language/REGISTER_AND_TONE.md`
- `docs/language/RHYTHM_AND_SOUND.md`
- `docs/language/METAPHOR_AND_ABSTRACTION.md`

---

## Must Decide
- канцелярит / номинализация
- псевдонаучность и ложная экспертность
- разрыв между словами и смыслом
- плотность и читаемость
- конкретность / абстрактность
- функция метафор

---

## Must Not Do
- не считать простой язык автоматически слабым
- не считать сложный язык автоматически сильным
- не путать стиль автора и языковой дефект

---

## Severity Rules
- critical: язык системно не переносит мысль
- high: repeated emptiness/overload
- medium: локальная размытость и распад связи
- low: единичные слабые формулировки

---

## Confidence Rules
- high при устойчивом паттерне в нескольких сегментах
- medium при нескольких совпадающих примерах
- low при единичных формулировках

---

## False Positive Rules
- не penalize намеренно простой регистр
- не penalize намеренно плотный научный регистр без признаков пустоты
- при fragment/uncertain mode снижать уверенность глобальных языковых выводов

---

## Output
- `module_output`
- `language_findings`

---

## Handoff
Передавать:
- top language risks
- сегменты с системной размытостью
- cautions по false positive риску
