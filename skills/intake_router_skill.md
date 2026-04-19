# intake_router_skill

## Goal
Выполнить intake + corpus profiling + genre routing + initial segmentation.

## Reads
- CORE_SYSTEM
- DATA_CONTRACTS
- GENRE_ROUTER

## Inputs
- raw_text
- metadata_if_any

## Must Decide
- full text or fragment
- probable text type
- dominant mode
- secondary modes
- initial segment map
- analysis limits

## Must Not Do
- не критиковать стиль
- не ставить глобальный диагноз качества

## Output
- corpus_profile
- segment_map
- handoff_notes
