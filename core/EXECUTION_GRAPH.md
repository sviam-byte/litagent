# EXECUTION_GRAPH

## Linear Graph

```text
intake_router_skill
  ← raw_text, metadata_if_any
  → corpus_profile
  → segment_map
  → handoff_notes

ai_detection_skill
  ← raw_text, corpus_profile, segment_map
  → ai_findings
  → ai_signal

epistemic_contract_skill
  ← raw_text, corpus_profile, segment_map
  → claim_map
  → contract_notes
  → epistemic_signal

propulsion_macro_skill
  ← raw_text, corpus_profile, segment_map
  → energy_map
  → macro_notes
  → propulsion_signal

overall_verdict_skill
  ← raw_text, corpus_profile, segment_map
  ← ai_signal
  ← epistemic_signal
  ← propulsion_signal
  → general_verdict

GENRE BRANCH (one or more, depending on routing):
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
  ← dominant_mode_label
  → language_findings

sentence_skill
  ← raw_text, corpus_profile, segment_map
  ← dominant_mode_label
  → sentence_findings

paragraph_skill
  ← raw_text, corpus_profile, segment_map
  ← dominant_mode_label
  → paragraph_findings

synthesis_guard_skill
  ← raw_text, corpus_profile, segment_map
  ← ai_findings
  ← branch_analysis
  ← language_findings
  ← sentence_findings
  ← paragraph_findings
  ← macro_notes
  → strengths
  → cautions
  → conflict_notes

revision_plan_skill
  ← general_verdict
  ← branch_analysis
  ← language_findings
  ← sentence_findings
  ← paragraph_findings
  ← strengths
  ← cautions
  ← conflict_notes
  → priorities
  → revision_plan
  → final_report_draft
```

## Branching Rules
If dominant_mode == fiction

Run:

fiction_skill on full text
or on routed fiction-heavy segments if segment_map strongly supports this.
If dominant_mode == nonfiction

Run:

nonfiction_skill on full text
or on routed nonfiction-heavy segments if needed.
If dominant_mode == hybrid

Run:

hybrid_skill on full text

Optionally also run:

fiction_skill on fiction-heavy segments
nonfiction_skill on nonfiction-heavy segments
If dominant_mode == uncertain

Run:

hybrid_skill in soft mode

And mark downstream branch findings with caution:

segmentation_uncertain
Isolation Rule

Each module reads raw_text independently.

No module receives:

cumulative prose summaries
final diagnosis prose from another module
irrelevant dumps of findings

Only structured outputs and signal objects may travel downstream.

Early Verdict Rule

overall_verdict_skill runs before branch/language/sentence/paragraph modules.

Reason:

it is an early editorial position,
not a prose recap of the full diagnostic tree.
Soft Routing Rule

If segment_map contains many mixed or uncertain segments:

avoid hard branch claims
prefer hybrid_skill
downgrade certainty of branch-specific findings
