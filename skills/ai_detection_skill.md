# ai_detection_skill

## Goal
Оценить признаки машинности текста без бинарного упрощения.

## Reads
- AI_DETECTION
- FALSE_POSITIVE_GUARD

## Inputs
- raw_text
- corpus_profile
- segment_map

## Must Decide
- key markers
- counter-markers
- suspicion level
- alternative explanations

## Must Not Do
- не путать слабость текста с ИИ
- не опираться на один поверхностный паттерн

## Output
- module_output with ai markers
