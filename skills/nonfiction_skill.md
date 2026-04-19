# NONFICTION_SKILL

## Purpose
Проверка, есть ли мысль, доказательство, объяснение и честный контракт с читателем.

---

## Reads
- `docs/nonfiction/NONFICTION_MASTER.md`
- `docs/nonfiction/THESIS_AND_ARGUMENT.md`
- `docs/nonfiction/EXPLANATION.md`
- `docs/nonfiction/SOURCING_AND_EVIDENCE.md`
- `docs/nonfiction/NONFICTION_PERSONA.md`
- `docs/nonfiction/NONFICTION_ARCHITECTURE.md`

---

## Must Decide
- governing_question
- central_claim
- subclaims
- claim_evidence_balance
- overclaim_zones
- explanation_gap_zones
- sourcing_risk
- persona_risk

---

## Must Not Do
- не путать explanatory text с polemical text
- не считать отсутствие контраргумента дефектом во всех режимах
- не называть «нет тезиса», если текст intentionally exploratory essay without claim, без caution

---

## Output Schema
- `module_output`
- `branch_analysis`
- findings.level ∈ `{semantic, epistemic, structural}`

---

## Severity Rules
- critical: отсутствует центральный тезис или маршрут аргумента развален
- high: repeated overclaim / evidence failure
- medium: local explanation gaps
- low: isolated imprecision

---

## Confidence Rules
- high при повторяемости дефекта в разных сегментах
- medium при нескольких убедительных примерах
- low при единичных местах, thin evidence или fragment

---

## False Positive Rules
- не снижать explanatory текст за отсутствие полемики
- не требовать ссылок в личном эссе без фактических претензий
- при mixed/uncertain сегментации помечать caution вместо жёсткого диагноза

---

## Handoff
- основные логические дефекты
- ключевые зоны риска доверия
- где нужен reroute на hybrid-mode
