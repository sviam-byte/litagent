# EXECUTION_GRAPH

## Linear Graph
```
intake_router_skill
  → corpus_profile
  → segment_map
  → dominant_mode (fiction | nonfiction | hybrid | uncertain)

ai_detection_skill
  ← raw_text, corpus_profile, segment_map
  → ai_findings

epistemic_contract_skill
  ← raw_text, corpus_profile, segment_map
  → claim_map, contract_notes

propulsion_macro_skill
  ← raw_text, corpus_profile, segment_map
  → energy_map, macro_notes

overall_verdict_skill                    ← NEW: runs here, not at the end
  ← raw_text, corpus_profile, segment_map
  ← ai_findings.summary
  ← claim_map.summary, contract_notes.summary
  ← energy_map.summary
  → general_verdict

GENRE BRANCH (choose one or more by segment):
  fiction_skill
    ← raw_text, corpus_profile, segment_map
    → fiction_analysis

  nonfiction_skill
    ← raw_text, corpus_profile, segment_map
    → nonfiction_analysis

  hybrid_skill
    ← raw_text, corpus_profile, segment_map
    → hybrid_analysis

language_skill
  ← raw_text, corpus_profile, segment_map
  → language_findings

sentence_skill
  ← raw_text, corpus_profile, segment_map
  → sentence_findings

paragraph_skill
  ← raw_text, corpus_profile, segment_map
  → paragraph_findings

synthesis_guard_skill
  ← raw_text, corpus_profile, segment_map
  ← [selected: ai_findings, branch_analysis, language_findings,
      sentence_findings, paragraph_findings, macro_notes]
  → strengths, cautions, conflict_notes

revision_plan_skill
  ← [selected upstream outputs]
  → priority_buckets, revision_plan, final_report_draft
```

## Branching Rules

### If dominant_mode == fiction
Run: fiction_skill on full text.

### If dominant_mode == nonfiction
Run: nonfiction_skill on full text.

### If dominant_mode == hybrid
Run: hybrid_skill on full text.
Additionally: if segment_map shows distinct fiction AND nonfiction segments,
run fiction_skill and nonfiction_skill on their respective segments.

### If dominant_mode == uncertain
Run: hybrid_skill in soft mode.
Flag all branch findings with false_positive_risk = high.

## Isolation Rule
Each module reads raw_text independently.
No module receives prose summaries of other modules' full outputs.
Summaries passed between modules must be structured objects, not free text.
