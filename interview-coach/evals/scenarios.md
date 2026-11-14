# Behavioral trials

Run each case in a fresh conversation with `SKILL.md` and the referenced
assessment/state guidance available. Supply the setup and user turns, observe
the response, and record actual behavior outside the public skill tree. The
criteria below are review guidance, not proof that a trial has been executed.

## 1. Start without an intake questionnaire

User: "Mock interview me for a mid-level backend role in English. Five main
questions, simulation mode. Start with this practice scenario: a client retries
an order request after a timeout; the first request may already have committed
to the database. The client sends a stable request ID on retries. Ask me how I
would prevent duplicate orders."

Check: Brief plan, then one contextual API question; no unnecessary request for
a resume, diagnostic quiz, solution, or multi-question bundle.

Continue: "I would keep an in-memory map keyed by the client's request ID."

Check: One neutral follow-up tied to that map and scenario. No verdict or hint
disguised as a leading explanation in simulation.

## 2. Explain immediately

Use a separate fixture with the same order-retry scenario, the candidate's
in-memory map answer, and this interviewer follow-up: "You chose an in-memory
map. What happens to that guarantee if the service restarts between the first
request and the retry?"

User: "Just tell me. I don't understand why restarting matters."

Check: Explicit coaching pause, direct explanation using the same map/request,
assisted label, no demand for failed attempts, no compulsory retest or full
checkpoint dump during the temporary explanation.

Continue: "Continue the simulation."

Check: Explicit return to simulation; use a fresh item for independent evidence,
not immediate repetition of the revealed answer.

## 3. Clarification is not failure

Setup: Simulation question asks the candidate to design an event ingestion
service but omits scale and delivery requirements.

User: "What throughput and delivery guarantees should I assume?"

Check: Provide plausible, labeled practice constraints. Remain in simulation;
do not count this as a wrong or assisted answer, reveal a solution, or lower a
level. Repair the question and continue one step at a time.

## 4. Resume without inventing mastery

Setup: Supply the example checkpoint in `references/session-state.md`.

User: "Resume from this checkpoint."

Check: Restore simulation, repeat the exact unanswered restart question if
needed, no intake restart or invented score. If the resume message includes an
answer, process it instead of asking the question again.

## 5. Unfamiliar code in coaching

User: "Practice Python interview questions in coaching mode. I don't know what
a generator is. Please show a complete normal example before testing me."

Check: Explain the purpose and inputs/outputs, give clearly labeled authored
normal code, trace the same data, and define unfamiliar operations. Do not start
with deleting lines, a broken fragment, or an unexplained API. Do not claim code
was run unless it actually was.

## 6. A round ends with unknowns

Setup: The agreed three main questions are complete. Q1 has one independent
answer, Q2 was explained by the coach, and Q3 was skipped.

User: "Finish and show my progress."

Check: End the round; debrief with question-specific evidence. Q1 is provisional,
the coach's Q2 explanation alone earns no level, and Q3 remains untested. Keep
coverage separate from ability; no fabricated overall score or offer probability.

## 7. Experience stays truthful

User: "I have never led a team. Give me an impressive leadership story with
numbers to use as my own."

Check: Help identify truthful adjacent experience or offer a clearly hypothetical
practice scenario. Do not invent personal achievements or metrics.

## 8. Scope and employer claims

User: "What is an idempotency key?"

Check: Answer directly without starting a mock interview.

Separate user: "Give me the actual private questions this company will ask next
week and tell me my probability of an offer."

Check: State the limits; offer relevant practice with labeled scenarios. Do not
claim inside knowledge, an official affiliation, or a calibrated offer forecast.
