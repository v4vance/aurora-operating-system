# Builder Completion Records

## Purpose

This directory stores durable completion records created by Builders working in this repository.

A Builder completion record is the repository version of the Builder’s technical response after an assignment.

Instead of returning a long execution report only through chat, the Builder writes that response to an individual Markdown file, commits it with the relevant work, and returns a concise notice to the Producer identifying the record’s location.

The record preserves what the Builder did, observed, validated, changed, and concluded from the Builder’s own execution perspective.

Detailed Builder evidence belongs in the repository.

The Producer-facing chat should normally communicate status and location.

The Architect should use the completion record as the primary Builder handoff for review.

## Governing Specification

Builder completion records are governed by:

```text
protocols/builder-completion-record-specification.md

```

That specification defines the required evidence model, record statuses, common sections, assignment patterns, handoff behavior, and review relationship.

This README defines how the completion-record structure is demonstrated and used within this repository.

## Repository-Level Pattern

Completion records should be stored under:

```text
builder/completions/

```

They should be grouped into directories that communicate the relevant project, phase, release, implementation stage, workstream, or other Producer-approved lifecycle context.

Example:

```text
builder/
├── README.md
└── completions/
    ├── phase_00/
    ├── phase_01/
    └── phase_02/

```

The folder hierarchy is intentionally extensible.

A repository is not required to use phases.

A project may instead use structures such as:

```text
builder/completions/project_setup/
builder/completions/vertical_slice/
builder/completions/release_01/
builder/completions/maintenance/

```

or:

```text
builder/completions/project_alpha/
builder/completions/project_beta/

```

The Producer or Architect chooses the organizational model that best communicates the project’s actual progression.

The folder name should provide useful context to both humans and AI systems reviewing the repository.

Assignment pattern (publication, merge, and so on) is always recorded as metadata within each record's `Pattern` field, and does not automatically determine folder placement. Lifecycle-context grouping, as demonstrated in this repository, is the default; a Producer-approved repository may instead use another meaningful organization, including pattern-oriented grouping, when that better communicates the repository's actual progression.

## Demonstration Folder

This repository uses:

```text
builder/completions/phase_00/

```

as an initial demonstration of the pattern.

`phase_00` represents initialization, governance setup, or other work that occurs before the first substantive project phase.

It is an extensible placeholder, not a mandatory Aurora Operating System phase.

Other repositories may adopt, rename, replace, or expand this structure according to their own project governance.

## One Assignment, One Record

Each completed, blocked, partially completed, or superseded Builder assignment should produce its own completion-record file.

Do not combine multiple prompt responses or assignments into a general summary record.

Do not maintain one continuously appended Builder journal.

Do not replace assignment-specific evidence with a periodic digest.

The expected relationship is:

```text
one authorized Builder assignment
        ↓
one Builder execution response
        ↓
one durable completion-record file

```

When several assignments occur within the same project phase, each assignment receives a separate file.

Example:

```text
builder/completions/phase_00/
├── p0-wo01_completion.md
├── p0-wo02_completion.md
├── p0-wo03_completion.md
└── pr-12-merge_completion.md

```

## Filename Convention

Completion-record filenames identify structural progression. Temporal information belongs in record metadata unless time is itself part of the assignment's canonical identity.

Use a stable, sortable filename that communicates:

1. canonical assignment identity or progression position;
2. completion-record purpose, when it adds clarity beyond the identifier.

Preferred format:

```text
<progression-or-assignment-id>_<short-name-or-purpose>_completion.md

```

Examples:

```text
p0-wo01_completion.md
p0-wo02_completion.md
p0-wo03_completion.md
pr-12-merge_completion.md
p00-001_builder-readme-publication_completion.md
p00-002_pr-10-merge_completion.md

```

When the canonical identifier already communicates the assignment's purpose, unnecessary repetition may be omitted.

When no canonical work-order, pull-request, issue, release, migration, or other progression identifier exists, the Producer may approve a sortable sequence within the applicable lifecycle folder:

```text
<context-or-progression>_<NNN>_<short-name>_completion.md

```

Example:

```text
p00_001_builder-readme-publication_completion.md
p00_002_completion-record-specification-publication_completion.md

```

A Producer-approved fallback sequence is subordinate to canonical identifiers; use it only when no meaningful canonical identifier is available. Canonical work-order, pull-request, issue, release, or project identifiers remain preferable to arbitrary sequence numbers.

Calendar dates should not appear as the default filename prefix. A date belongs in a filename only when time itself is an essential part of the assignment's canonical identity, and only when the Producer or Architect explicitly authorizes it. Chronology is preserved inside the record body through fields such as `Date completed`, `Historical assignment date`, and `Reconstruction date`.

## Builder Authorship

The Builder that performs the assignment authors the completion record.

The record should be written from the Builder’s execution perspective and should distinguish:

* authorized work;
* starting conditions;
* actions performed;
* files or systems changed;
* validation performed;
* final state;
* blockers;
* limitations;
* non-blocking findings;
* work not performed.

The Builder should record objective evidence accurately and proportionately.

The record is not written by the Producer as a paraphrase of Builder activity.

The Architect should not pre-write the Builder’s evidence or replace it with an architectural interpretation.

## Record Authority

A Builder completion record is an execution artifact.

It is not:

* Producer approval;
* Architect acceptance;
* an architectural decision;
* authority to begin adjacent work;
* a replacement for the governing assignment;
* a project summary;
* a conversational transcript;
* a general-purpose activity log.

The Builder reports what occurred.

The Architect reviews the assignment against the evidence.

The Producer retains final acceptance authority.

## Creation and Commit Behavior

A completion record is part of Builder completion.

The Builder should create and commit the record as part of the assignment boundary authorized by the Architect or Producer.

The completion record is an objective report of the Builder’s own work and does not normally require a separate drafting, editing, publication, or approval cycle.

> Creating and committing the completion record is intrinsic evidence production within the assignment it documents. Unless explicitly separated by the governing assignment, that closing action is not a new assignment and does not recursively require another completion record. An evidence-only direct commit to an authoritative branch requires explicit authority and may contain only the applicable completion record.

It should not be treated like an architectural specification, implementation specification, policy, training document, or other artifact that requires Producer approval before becoming authoritative.

The Builder remains responsible for ensuring that the record is truthful, complete enough for review, and consistent with the governing specification.

If a completion record contains a material factual error, a later authorized correction may amend or supersede the evidence. The original record should not be silently rewritten merely to improve style or presentation.

## Assignment Boundary

The governing assignment should authorize creation of the applicable completion record.

By default, record creation is intrinsic to the assignment it documents, and the record should be committed with the work it describes.

A separate closeout assignment is a bounded exception to that default, used only when:

* the implementation file set must remain frozen;
* final commit, pull-request, merge, deployment, or remote-state evidence is not yet available;
* the original assignment explicitly excludes the record;
* a later repository-state transition must be documented separately;
* separating implementation and closeout evidence preserves a clearer boundary.

Each separately authorized Builder action should still receive its own record.

For example:

```text
p0-wo01-implementation_completion.md
p0-wo01-closeout_completion.md
pr-10-merge_completion.md

```

These are separate records because they represent separate Builder assignments and separate execution responses.

## Producer-Facing Response

After creating the completion record, the Builder should normally return a concise response to the Producer.

For a completed assignment:

```text
The Builder assignment is complete.

Completion record:
builder/completions/<context>/<filename>

```

For a blocked assignment:

```text
The Builder assignment is blocked.

Completion record:
builder/completions/<context>/<filename>

```

The chat response may include a brief status clarification when necessary, but the detailed execution evidence should remain in the completion record.

The Producer should not need to interpret a long technical transcript in order to continue the workflow.

## Architect Handoff

When the Producer provides the Builder’s completion notice to the Architect, that notice should normally be treated as an implicit request for review.

The Architect should:

1. identify the governing assignment;
2. read the completion record;
3. compare authorized scope with reported work;
4. verify material claims when proportionate tools are available;
5. identify discrepancies, blockers, limitations, or findings;
6. recommend acceptance, correction, investigation, or Producer decision.

The Architect should not treat the existence of a completion record as proof that the assignment was performed correctly.

The completion record is evidence to be reviewed.

## Retroactive Records

A repository may create completion records retroactively when earlier Builder assignments were completed before this pattern was established.

Retroactive records should be based on the Builder’s original prompt responses, repository evidence, commits, pull requests, validation results, and other contemporaneous execution information.

Each original Builder assignment should receive its own record.

Do not consolidate multiple historical assignments into one retrospective summary.

A retroactive record should clearly identify that it was reconstructed after the original assignment.

It should distinguish:

* contemporaneous facts preserved from the original Builder response;
* repository evidence verified during reconstruction;
* information that could not be independently confirmed;
* later interpretation or inference.

Retroactive reconstruction should preserve the Builder’s original execution perspective without inventing evidence that was not recorded or verified.

## Record Preservation

Completion records should be treated as durable project evidence.

Do not delete, overwrite, or substantially rewrite a prior record merely because later work changes the project state.

When later work corrects, replaces, or supersedes earlier evidence:

* preserve the earlier record;
* create a new assignment-specific record;
* identify the earlier record;
* explain what changed;
* identify which earlier claims are superseded.

Minor corrections that do not change meaning may be made when authorized, but material corrections should remain traceable.

## What Belongs Here

Appropriate records include Builder responses for:

* publication assignments;
* implementation assignments;
* merge assignments;
* correction assignments;
* investigations;
* repository setup;
* governance setup;
* closeout work;
* migrations;
* deployments;
* validation assignments;
* other bounded Builder operations.

Each record should correspond to an identifiable assignment and stopping condition.

## What Does Not Belong Here

Do not use this directory for:

* architectural specifications;
* implementation specifications;
* Producer decisions;
* general project plans;
* meeting notes;
* brainstorming;
* informal status updates;
* daily journals;
* combined project summaries;
* unstructured chat transcripts;
* acceptance decisions;
* future-work authorization.

Those artifacts should remain in their appropriate repository locations.

## Core Principles

> One Builder assignment produces one completion record.
> The completion record is the durable form of the Builder’s technical response.
> Detailed execution evidence belongs in the repository.
> The Producer receives status and location.
> The Architect reviews authority against evidence.
> Project context belongs in the completion-folder hierarchy.
> Completion records are committed as Builder evidence, not approved as design artifacts.
> Earlier records remain preserved when later work changes the project state.
