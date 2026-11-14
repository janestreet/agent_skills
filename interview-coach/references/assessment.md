# Evidence-based interview feedback

Choose a small set of role-relevant dimensions. Examples include technical
reasoning, implementation, trade-offs, communication, and ownership/reflection.
Do not score accent, personality, protected traits, or similarity to the
interviewer's preferred style. Evaluate understandable, job-relevant content.

For each assessed item, retain:

- Question ID and the actual question/scenario, including constraints.
- A short excerpt or faithful summary of what the candidate said or did.
- Relevant dimension and what that evidence supports or contradicts.
- Assistance: none, clarification only, hint, or solution shown.
- Execution status if applicable: observed with result, candidate-reported,
  not run, or blocked; include limits of the check.
- Next action, if a material uncertainty remains.

Use these levels as practice anchors, relative to the agreed role and difficulty:

| Level | Demonstrated behavior |
| --- | --- |
| 0 | After a fair independent assessment, cannot yet begin the relevant task. |
| 1 | Recognizes terms but cannot yet connect them to the task. |
| 2 | Follows an explanation and can describe parts of it; not independent. |
| 3 | Reaches a workable approach with targeted help. |
| 4 | Independently gives a correct, justified approach under the stated constraints. |
| 5 | Independently handles a meaningful edge case or trade-off and explains the reasoning clearly. |

Untested is `—/5`, not zero. Mark first observations `provisional`; level 0 also
requires evidence and is never the default. Tutor explanations alone support
no score. If the candidate demonstrates understanding after assistance, record
that assisted observation without replacing an established independent level.
To establish or raise a consolidated level, require at least two independent
checks, including a later unprompted recall/transfer check. A simulation's
ordinary follow-up may supply evidence if it does not give away the reasoning.
Repeating a revealed answer immediately is not a second independent check.

One failed recall does not automatically erase prior evidence. Report the
conflict and distinguish missing context, syntax trouble, and conceptual errors.
Change an established level only when subsequent independent evidence supports
the change. Track execution status separately from reasoning ability: no runtime
means unverified execution, not incorrect reasoning.

Example display (illustrative data only):

```text
Round: Backend / mid-level          Coverage: 3 of 5 main questions
---------------------------------------------------------------
Reasoning            [████████░░]  4/5  provisional; Q1 independent
Trade-offs           [██████░░░░]  3/5  provisional; Q2 hinted
Implementation       [   untested ] —/5  execution not assessed
Communication        [████████░░]  4/5  established; Q1 + later Q3
---------------------------------------------------------------
Next practice: justify the consistency boundary in the same design.
```

Use two solid blocks per numerical level. Add an explicit basis beside each
rating, not a precision-looking overall percentage. Distinguish evidence seen
in this round from an established level restored from a checkpoint.

Keep the debrief proportionate: a short overall description, specific strengths
with evidence, prioritized gaps with examples of a better response, then a next
practice plan. Do not output "hire/no hire" or an invented offer likelihood.
