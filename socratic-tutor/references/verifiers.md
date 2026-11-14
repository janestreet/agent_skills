# Verifier guidance

Use this reference when turning a learning objective into an executable check.
The tutor owns the checker; the learner owns the answer. Teach the subject clearly
even when the checking machinery stays out of the conversation.

## Choose what to check

State the objective, the concrete claim, its inputs and assumptions, and what
would count as success. Apply code verification to every checkable component,
including components of answers expressed in natural language. Keep conceptual
reasoning as a separate assessment dimension.

| Objective | Executable evidence | What it does not establish |
| --- | --- | --- |
| Compute a discounted return | Compare submitted values with an independent finite sum | Understanding why past rewards are excluded |
| Predict a tensor shape | Run the pinned operation on the stated shapes | Correct values, or behavior of an unexecuted model |
| Write a query | Execute against a fixture and compare results, accounting for duplicates and ordering | Correctness for all possible databases |
| Explain an exploration rule | Enumerate branch probabilities under stated assumptions | Whether a policy will converge in an unknown environment |
| Evaluate an open-ended explanation | Check any executable subclaims; assess the rest with explicit reasoning criteria | Semantic correctness from keyword matching |

Prefer a trusted reference or an independently derived oracle. A checker that
compares an implementation to itself, evaluates an LLM's opinion, or simply
returns success does not provide independent evidence. Test a known correct
answer and a plausible misconception before relying on the checker. Add relevant
cases if the objective is a general rule rather than one numerical prediction.

Accept equivalent valid answers. Set numerical tolerances from the scale and
precision of the task; reject non-finite values where the expected result is
finite. Record versions, seeds, and relevant runtime settings. A fixed seed makes
an experiment reproducible, not a proof. Prefer exact enumeration when it answers
the question better than a noisy simulation.

Preserve the submitted answer before converting it into data. If an answer is
ambiguous or incomplete, ask for the missing meaning; do not complete it silently
and credit the learner for the repaired version. Never evaluate prose as code.

## Worked example: discounted return

This is a small synthetic teaching example, not a production RL implementation.
It checks a finite, truly terminated episode, not an externally truncated one.
No third-party packages are required.

Explain the concept before asking the learner to apply it: a return measures the
current reward plus discounted future rewards from a particular step. Let `r[t]`
be the reward after action `t`, and let `gamma` be the discount factor. For a
terminated episode of length `T`,

```text
G[t] = sum(gamma ** (k - t) * r[k] for k from t to T - 1)
```

In one continuous example, taking a key costs 1 point, walking to the chest earns
0, and opening it earns 10 and ends the episode. Thus `rewards = [-1, 0, 10]`.
With `gamma = 0.9`, the returns are `[7.1, 9.0, 10.0]`. The middle value excludes
the already-paid key cost and includes the current reward and discounted next
reward. These are episode samples, not expected values across random episodes.

The following code verifies a **tutor-provided worked example**. It is not evidence
of learner mastery. In an assessment, first ask for and preserve the learner's
answer, then replace `candidate` with that answer; do not disclose the expected
values beforehand. The learner need not read this code.

Save this block as `verify_return.py` in the lesson workspace and run
`python verify_return.py` (or the environment's Python command):

```python
from math import fsum, isclose, isfinite


def check_returns(rewards, gamma, candidate):
    # Finite terminated episodes, numeric data, and 0 <= gamma <= 1 only.
    if not isfinite(gamma) or not 0 <= gamma <= 1:
        raise ValueError("gamma must be finite and between 0 and 1")
    if not all(isfinite(reward) for reward in rewards):
        raise ValueError("rewards must be finite")
    # Direct finite sums provide an oracle independent of a backward recurrence.
    expected = [
        fsum(gamma ** (k - t) * rewards[k] for k in range(t, len(rewards)))
        for t in range(len(rewards))
    ]
    passed = len(candidate) == len(expected) and all(
        isfinite(actual) and isclose(actual, reference, rel_tol=1e-9, abs_tol=1e-9)
        for actual, reference in zip(candidate, expected)
    )
    return passed, expected


# Checker controls: valid answers, a plausible misconception, and boundary cases.
controls = [
    ([-1, 0, 10], 0.9, [7.1, 9, 10], True),
    ([-1, 0, 10], 0.9, [7.1, 7.1, 7.1], False),
    ([-1, 0, 10], 0.9, [7.1], False),
    ([-1, 0, 10], 0.9, [float("nan"), 9, 10], False),
    ([-1, 0, 10], 0, [-1, 0, 10], True),
    ([-1, 0, 10], 1, [9, 10, 10], True),
    ([2], 0.9, [2], True),
    ([], 0.9, [], True),
]
for rewards, gamma, answer, should_pass in controls:
    passed, _ = check_returns(rewards, gamma, answer)
    if passed != should_pass:
        raise RuntimeError("Verifier control failed; do not grade the learner")
print("checker controls: passed")

rewards = [-1, 0, 10]
gamma = 0.9
candidate = [7.1, 9.0, 10.0]  # Tutor-provided demonstration, not a learner answer.
passed, expected = check_returns(rewards, gamma, candidate)
print("status:", "pass" if passed else "fail")
print("candidate:", candidate)
print("reference:", expected)
print("scope: one finite terminated episode; rel_tol=abs_tol=1e-9")
raise SystemExit(0 if passed else 1)
```

This checker accepts only the numeric data described above; it is not a parser
for arbitrary learner messages. A malformed input or failed control is a checker
or input-handling problem, not evidence of a conceptual error. Retain the actual
run output and interpreter version. Do not describe the expected output of this
document as an observed execution.

After a successful run, explain that each entry includes the rewards from its
own step onward. If the learner instead assigns `7.1` to every step, the mismatch
is useful evidence about confusing the episode's initial return with each later
step's return. Explain that distinction; do not just report that a test failed.

## Report useful evidence

Keep the learner-facing report short: the submitted answer, outcome, what was
checked, and what the result means for the concept. Checker source is optional
unless requested. Preserve a reproducible snippet or artifact with:

- Objective and the original answer, including whether it was independent,
  assisted, or a tutor demonstration.
- Fixture, assumptions, oracle/property, comparison rule, and checker controls.
- Command/tool, relevant versions and settings, actual output, and outcome.
- Limits of the check, conceptual feedback, and remaining assessment needs.

Use **pass** or **fail** only when a working check decided the claim. Use
**blocked** when execution could not complete (for example, a missing package),
and **inconclusive** when execution completed but does not settle the claim (for
example, a statistical interval too broad to distinguish predictions). Record
blocked and inconclusive objectives as pending verification, not as student
failures. A qualitative judgment should be explicitly labeled as such.

Use the existing authorized runtime with bounded resources. When executing
learner-supplied programs, use an appropriate sandbox, time limits, and isolation
from secrets, unrelated files, and network effects. If that is unavailable,
inspect the answer, teach the concept, and leave execution pending. Data-only
checks such as the example do not require running learner code.

## Behavioral evaluation scenarios

These are scenarios for reviewing tutor behavior, not a universal automated test
suite or proof that a model will always follow the skill.

- **Prose numerical answer:** The learner submits return values in words. The
  tutor faithfully converts the values, runs a checker, and explains the return
  concept without turning the lesson into a Python tutorial.
- **Mixed objective:** With two actions, a unique greedy action, and a uniform
  random branch, the learner says epsilon `0.1` means a `0.1` probability of the
  non-greedy action. The tutor executes the probability computation and explains
  why the random branch may choose the greedy action too. This numerical check
  does not establish understanding of exploration or convergence.
- **Explanation request:** The learner asks why a later step's return excludes
  earlier costs. The tutor directly explains using the same episode, without
  requiring another attempt or appending an obligatory quiz.
- **Missing runtime:** A pinned model operation needs a package that is absent.
  The tutor marks it blocked, teaches the concept, and supplies a reproducible
  check. An auxiliary formula check must not be reported as running that model.
- **Non-checkable claim:** The learner discusses an open-ended design tradeoff.
  The tutor uses explicit conceptual criteria and checks any executable subclaims
  without using keyword matches as a semantic oracle.
- **Faulty checker:** The known incorrect control passes. The tutor repairs the
  verifier before grading; the learner's level does not decrease.
- **Resume and mastery:** A checkpoint contains a demonstrated example, a pending
  question, and unchanged scores. The tutor resumes that question without a new
  diagnostic or crediting its own earlier demonstration as independent evidence.
