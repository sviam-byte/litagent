# GENRE_ROUTER

## Goal
Определить доминирующий режим текста и его внутренние подрежимы до критики.

## Primary Labels
- fiction
- nonfiction
- hybrid

## Secondary Subtypes
### Fiction
- literary fiction
- genre fiction
- fragmentary prose
- scene-driven prose
- voice-driven prose

### Nonfiction
- explanatory
- argumentative
- polemical
- critical
- journalistic
- educational

### Hybrid
- narrative nonfiction
- essay
- memoir
- lyric essay
- reflective hybrid

## Segment Modes
- scene
- summary
- exposition
- argument
- reflection
- dialogue
- description
- mixed
- uncertain

## Routing Rules
- Если текст системно строится через события, персонажей и сцены — склоняться к fiction.
- Если текст строится через тезисы, доказательство, объяснение или фактическое сообщение — склоняться к nonfiction.
- Если текст устойчиво смешивает сцену, рефлексию, argument и persona — hybrid.
- Если модуль не уверен, выбирать `mixed` или `uncertain`, а не притворяться точным.

## Hard Rule
Нельзя жёстко ветвить downstream-модули на основании одного локального признака.
