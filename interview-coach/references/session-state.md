# Compact session checkpoint

Keep a readable state block or file; use this schema as guidance rather than
requiring a particular parser. Store only what is needed to resume. Prefer short
answer summaries over a full transcript. Keep candidate-specific files outside
the public skill checkout and out of commits.

```yaml
schema: interview-coach/v1
target: {role: backend engineer, seniority: mid-level, language: Chinese}
mode: simulation
phase: awaiting-answer
resume_mode_after_coaching: null
round: {main_question_limit: 5, followup_limit_per_question: 2}
position: {main_question: 2, followups_used: 1}
roadmap: [reasoning, implementation, trade-offs, ownership, reflection]
current_scenario: "Practice order API; client retries after a timeout."
fixed_assumptions: ["The client supplies a stable request key."]
source_refs: []
pending_question: "You proposed an in-memory request-key map. What happens to that guarantee when the service restarts?"
pending_status: unanswered
evidence:
  - id: Q2
    candidate_summary: "Proposed an in-memory map keyed by request ID."
    assistance: none
    supports: "Recognizes duplicate-request detection; restart behavior untested."
    execution: not-applicable
ability_map: []
unresolved: ["Durability of duplicate-request detection"]
next_action: "Wait for the answer to Q2 follow-up 1; keep simulation feedback deferred."
preferences: ["One question per turn"]
```

The values above are an example, not an initial score or default candidate
history. In a real checkpoint include ability levels, provisional/consolidated
status, independent evidence IDs, and any contradictory observations. Preserve
source versions, code paths, variables, shapes, and execution artifacts only when
relevant to that interview.

On resume, read the checkpoint before asking anything. Briefly orient the
candidate and repeat only an unanswered pending question when useful. If they
already answered it in their resume message, evaluate that answer and continue
instead of asking again. For a paused solution explanation, wait for the user's
continuation and choose a fresh assessment item. Preserve assistance labels.
Do not repeat diagnostic or intake steps already captured.

If essential state is absent, identify the specific missing field and ask only
for what is necessary. Keep known progress; do not invent the previous question,
answers, timing, or scores. Record later corrections over stale checkpoint values.
