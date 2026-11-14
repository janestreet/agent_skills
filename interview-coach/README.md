# Interview Coach

Practice with an interviewer who listens to your answer and asks a relevant
follow-up. Switch to coaching when you need an explanation, then return to the
round with a clear record of what you demonstrated independently.

This is a candidate-facing interview preparation skill, adapted from
[socratic-tutor](../socratic-tutor/SKILL.md). It supports technical, system design,
project, and behavioral practice. It does not represent any employer's interview
process or predict offers.

## Try it

Copy the `interview-coach` directory into the skills directory supported by your
agent. Invoke `$interview-coach` where supported, or ask the agent to use it:

> Run a mid-level backend engineer mock interview. Use five main questions,
> ask one at a time, and save feedback for the end. Start with API reliability.

> Help me practice an ML engineer interview in coaching mode. Explain in Chinese
> with English technical terms. Keep the same example through follow-up questions.

> Rehearse behavioral interview questions about project ownership. Follow up on
> my actual experience and tell me where my answers lack supporting evidence.

For a chatbot without skill-file loading, paste the body of
[SKILL.md](SKILL.md), [assessment.md](references/assessment.md), and
[session-state.md](references/session-state.md) as instructions. It can conduct
the conversation without execution tools; code execution stays unverified until
there is actual execution evidence.

## What changes from Socratic tutoring?

| Interview need | Behavior |
| --- | --- |
| A realistic round | Default simulation defers scores, hints, and solutions until the debrief. |
| Useful follow-ups | Each probe connects to the candidate's actual answer and the same scenario. |
| Help when stuck | `coach`, `hint`, or `just tell me` provides help immediately and labels it assisted. |
| Fair assessment | Missing prompt context is repaired; assisted answers and untested skills stay distinct. |
| An end point | Finish at the agreed question budget or say `finish`; mastery is not a prerequisite. |
| Continuity | `save state` preserves the pending question, assumptions, mode, and evidence for `resume from:`. |

The skill incorporates practical feedback about disconnected questions,
unexplained terminology, incomplete code snippets, premature trick questions,
and grading an explanation as if it were independent performance. Its coaching
mode uses complete, continuous examples; simulation keeps the solution hidden
until the candidate requests assistance or the round ends.

## A short example

This is an authored demonstration, not a recorded session or an employer question.

**Interviewer:** In this practice scenario, a client retries an order request
after a timeout. How would you prevent the retry from creating a second order?

**Candidate:** I would keep an in-memory map of request IDs and return the prior
result if the request ID has already been processed.

**Interviewer:** You chose an in-memory map. What happens to that guarantee if
the service restarts between the first request and the retry?

**Candidate:** Just tell me the answer.

**Coach:** Pausing simulation for coaching. A restart loses the map, so the retry
can create another order. For a database-backed design, persist the request key
with a unique constraint and commit it with the order in one transaction. A retry
can return the recorded result. Define what happens when the same key arrives
with a different payload, and handle concurrent attempts consistently. The
guarantee covers the database transaction; external side effects need their own
coordination. This item is now assisted; we will use a fresh item for later
independent assessment.

## Progress and limitations

The roadmap shows coverage. A separate text ability map shows 0-5 evidence levels
with `█` / `░` bars, provisional ratings, and untested items. Scores are practice
feedback, not validated psychometric measurements or hiring predictions.

Model behavior varies. [Behavioral scenarios](evals/scenarios.md) let maintainers
check the important decisions with observable responses; they are not an
automatic benchmark or a guarantee that every model follows every instruction.
No runtime or network service is required to conduct a conversational round.

## Origin and development

Developed by [ZikiiSan](https://github.com/ZikiiSan) as an interview-focused
adaptation of [Jane Street's agent_skills](https://github.com/janestreet/agent_skills).
The [development branch](https://github.com/ZikiiSan/agent_skills/tree/feat/interview-coach)
contains the candidate-facing version and examples. To follow this adaptation,
you can star [ZikiiSan/agent_skills](https://github.com/ZikiiSan/agent_skills).
This adaptation is independent and does not imply endorsement by Jane Street.

Distributed under the [MIT license](LICENSE.md), preserving the upstream notice
inside this folder when it is installed separately. Repository contributions
follow [CONTRIBUTING.md](../CONTRIBUTING.md).
