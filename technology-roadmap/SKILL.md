---
name: "technology-roadmap"
description: "Quantitative technology roadmapping when the user asks for a technology roadmap, R&D direction, or technology strategy: answer Olivier de Weck's ATRA four questions in order — evidence-scored maturity per building block, scenario enumeration, portfolio allocation by risk tolerance, and committed phases with KPIs and kill criteria. Trigger phrases: 'technology roadmap', 'roadmap for X', 'technology strategy', 'R&D plan', 'where should we invest', 'ATRA'. Not for sprint backlogs, feature roadmaps, or plans under one quarter."
---

# Technology Roadmap (ATRA)

Build a technology roadmap by answering Olivier de Weck's four questions in order
(Advanced Technology Roadmap Architecture, MIT). Each question has a completion
criterion — do not move on until it is met. Deliver one document with four
sections plus two appendices.

## Q1 — Where are we today? (measure, don't remember)

1. Inventory the building blocks of the system or topic (aim for 5-10 blocks).
2. Score each block's maturity 0-5:

       0 none · 1 blueprint written · 2 demo working · 3 verified in a controlled
       environment · 4 running as a production pilot · 5 stable in production

3. Every score must cite evidence — a link, a log line, a date, or a number. No
   evidence means score 0. Never score from memory or impressions.
4. Trace history: for the core technology, list what already existed and when it
   appeared. Treat novelty as an illusion until proven otherwise; as de Weck puts
   it, "technology does not move as fast as many people believe".

Done when: a table of blocks with evidence-backed scores, plus a short history
trace of the core technology.

## Q2 — Where could we go? (enumerate, don't choose)

1. List at least three distinct scenarios spanning ambition levels (conservative /
   full build / frontier). One line each, with what the scenario assumes.
2. List the cross-cutting uncertainties that apply to every scenario (vendor
   availability, price curves, single points of failure, regulation).
3. Do not rank or evaluate scenarios in this step — Q2 enumerates, Q3 decides.

Done when: every scenario has a one-line description and its assumptions, and the
uncertainties are listed separately.

## Q3 — Where should we go? (allocate like a portfolio)

ATRA applies Markowitz portfolio theory to R&D selection. Treat effort as an
investment portfolio:

1. Allocate percentages across four asset classes:

   - bonds — stabilizing the foundation (operations, backups, runbooks, security)
   - index funds — replicating proven patterns at moderate scale
   - growth — extending what already works toward the chosen goal
   - speculative — frontier experiments, hard-capped at 5-10%

2. Tie every allocation to Q1 scores and the user's stated risk tolerance. Higher
   risk tolerance shifts weight from bonds toward growth; speculative never
   exceeds its cap.
3. State a rebalancing rule: re-run all four questions on a fixed cadence
   (e.g. quarterly).

Done when: percentages sum to 100 and each has a one-line rationale referencing
Q1 evidence.

## Q4 — Where are we going? (commit with kill criteria)

1. Convert the chosen direction into 3-5 phases with target dates (G0, G1, ...).
2. Give every phase: concrete work items, at least one measurable KPI (a number,
   not a feeling), and one kill-or-pivot criterion ("if X happens, stop and
   reassess").
3. Split the horizon: durable rails (policy, architecture, patterns) are planned
   in years; swappable cars (tools, models, vendors) are planned in quarters and
   must be replaceable.

Done when: every phase has a date, a KPI, and a kill criterion.

## Appendices (always include)

- History appendix — a dated timeline of how the current state came to be. ATRA
  requires tracing history before projecting forward.
- Risk register — known risks with likelihood, impact, and the mitigation already
  present in the design.

## Verify before delivering

- Every Q1 score cites evidence.
- Portfolio percentages sum to 100; speculative is under its cap.
- Every phase has a KPI and a kill criterion.
- The footer states the rebalancing cadence: a roadmap is a living asset, re-run
  when new evidence arrives — not wallpaper.

## Source

Olivier L. de Weck, "Technology Roadmapping and Development: A Quantitative
Approach to the Management of Technology" (Springer, 2022); MIT News, "3
Questions: Technology roadmapping in teaching and industry" (2024);
roadmaps.mit.edu.
