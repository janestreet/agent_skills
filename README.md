# Agent skills from Jane Street

A collection of skills for AI agents and chatbots.
Each skill is a directory containing a `SKILL.md` file
with instructions for the agent.

## Skills

- **[socratic-tutor](socratic-tutor/SKILL.md)** — teaches concepts with clear
  explanations, worked examples, and one Socratic question at a time. Uses
  executable verifiers for every code-checkable learning objective, with a
  diagnostic, a skill map with levels 0-5, spaced review, and a final assessment.

## How to use

With a coding agent that supports the common `SKILL.md` format, copy the skill
directory into your agent's skills folder, then ask the agent to use it
("teach me X").

With a plain chatbot, paste the body of the skill's `SKILL.md` into the chat
(or into a custom/system prompt), followed by what you want it to do. Include the
[verifier guidance](socratic-tutor/references/verifiers.md) when executable checks
are needed. A chatbot without execution tools can teach and prepare checks, but
must leave those objectives pending verification until execution evidence exists.

For example:

> Teach me reinforcement learning. Explain the concepts using one continuous
> example, and run a verifier for every objective that code can check. I want to
> understand the subject; I do not need a walkthrough of the verifier code.

Specify your background, preferred language, target depth, and any source version
or saved checkpoint. You may answer in prose: the tutor should handle the verifier
unless writing code is itself your learning goal. When using source code as the
teaching material, the tutor should explain the normal data flow and distinguish
real source from simplified teaching examples.

## Usage notes

- **Verification is required where applicable.** Numerical results, shapes,
  program behavior, query results, and formal properties should be checked by
  actual execution, including during diagnostics, examples, review, and final
  assessment. The tutor should explain the result and its conceptual meaning,
  not just display a pass/fail label.
- **Keep claims within the check's scope.** A passing example is not a proof of
  a general rule, and a simulation does not establish a true expectation or
  guarantee convergence. Mixed objectives need both executable checks and an
  explanation of the remaining reasoning. Subjective judgments should not be
  disguised as code verification.
- **Missing tools do not mean an incorrect answer.** If a runtime or dependency
  is unavailable, the tutor should teach what it can, provide a reproducible
  check, and mark verification pending. Learner-reported output must be labeled
  as such. Code that has only been written or mentally traced has not been run.
- **Verifier code is optional reading.** Ask `show verifier` to inspect its
  assumptions, inputs, execution evidence, and limits. Running learner-supplied
  programs requires an appropriate isolated environment and execution limits;
  arbitrary code should not run with access to credentials or unrelated files.
- **Explanations are available immediately.** Ask "why", "what does that mean",
  or `just tell me`. The tutor should answer directly without requiring repeated
  failures or immediately attaching another quiz. Use `harder` or `easier` to
  adjust difficulty.
- **Progress requires independent evidence.** Tutor demonstrations and immediate
  repetition do not earn mastery. The learning roadmap describes coverage; the
  text skill map records demonstrated ability and explicitly marks untested
  items. Use `show progress` to see it.
- **Save continuity explicitly.** Use `save state`, then `resume from:` with the
  saved block in a new session, or provide an agreed project checkpoint path.
  Preserve the current example, pending question, verifier artifacts/results,
  and independent evidence. Files and chat history are not guaranteed to be
  loaded automatically in another session.

See the [verifier guidance](socratic-tutor/references/verifiers.md) for a runnable
example and scenarios for evaluating the skill's behavior. No particular runtime
is mandatory for the skill; the example uses only the Python standard library.

## Contributing

Submit changes through GitHub pull requests and follow
[CONTRIBUTING.md](CONTRIBUTING.md). Every commit requires a Developer Certificate
of Origin sign-off using your real name and email (`git commit -s`); the sign-off
and contribution become part of the public record. See [LICENSE.md](LICENSE.md)
for the repository's MIT license.
