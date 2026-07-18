# The Congruence Principle

## Definition

**Congruence** is the degree to which a project's interpretations, plans,
actions, and outputs remain faithful to the Producer's actual intent,
governing context, and desired outcome.

Congruence is not about whether work gets done, or whether it gets done
smoothly. It is about whether the work being done is the right work.

## Congruence is not coordination

Coordination and congruence are often confused, but they answer different
questions:

- **Coordination** concerns whether participants work together
  effectively — whether communication flows, whether tasks are handed off
  cleanly, whether people and systems are in sync with one another.
- **Congruence** concerns whether they are pursuing and producing the
  right thing in the first place.

A project can be highly coordinated and poorly congruent at the same
time. Everyone can be aligned, responsive, and efficient while building
toward a misunderstood goal. This condition can be described as
**efficiently producing the wrong result** — the process looks healthy
right up until the output is measured against what was actually intended.

## Why AI systems are especially vulnerable

AI systems are particularly exposed to this failure mode because they can
produce fluent, internally consistent, well-structured output from an
incomplete or mistaken interpretation of intent. Coherence is not evidence
of correctness. A confident, polished answer to the wrong question is
still the wrong answer, and its polish can make the error harder to
notice, not easier.

This is why congruence has to be actively protected rather than assumed.

## Responsibility for congruence

- The **Architect** is responsible for protecting congruence — interpreting
  the Producer's intent carefully, surfacing ambiguity, and shaping
  structure and instructions that stay faithful to that intent.
- The **Builder** is responsible for implementing the authorized
  interpretation rather than redefining it. The Builder may raise
  questions or flag concerns, but does not silently substitute its own
  judgment about goals for the Producer's.
- The **Producer** remains the final authority on intended outcomes. When
  there is doubt about what is actually wanted, the Producer's judgment
  resolves it.

## Operating heuristic

**If knowledge is expected to outlive the current conversation, it belongs
in an artifact rather than only in a prompt.**

Prompts express what is unique to the current assignment. Artifacts
preserve what should remain true across assignments. When the same
explanation, constraint, or piece of context has to be repeated across
multiple conversations, that repetition is usually a signal — it often
means an artifact is missing or inadequate, and the knowledge is being
carried in memory instead of being written down where it can be relied
upon.

## Congruence in review

Reviewing a project's work should not stop at checking correctness —
whether the output is accurate, functional, or well-made. It should also
test continuing faithfulness to Producer intent: does this output still
serve the outcome the Producer actually wants, or has the work drifted
into solving a nearby but different problem?

## Scope

This principle is domain-neutral. It applies equally to software
development, writing, training, research, and creative production, and to
any other undertaking where an interpretation of intent stands between a
request and a result.
