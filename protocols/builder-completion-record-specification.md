# Builder Completion Record Specification

## Purpose

This specification defines how Builder completion evidence is recorded, stored, reported, and handed off for Architect review under the Aurora Operating System.

The Builder performs the authorized work and records the technical evidence.

The Producer receives a concise completion notice.

The Architect reads the completion record, compares it with the governing assignment, verifies material claims when tools are available, and recommends a review outcome under the Review Protocol.

The completion record separates detailed execution evidence from the Producer-facing conversation.

## Core Model

Every completed or blocked Builder assignment should produce one durable completion record.

The record belongs in the target repository whenever:

* the repository is writable;
* the assignment changes or evaluates repository-controlled work;
* the governing specification does not prohibit creation of the record;
* the record can be included without corrupting the intended change boundary.

The completion record is evidence.

It is not:

* Producer acceptance;
* Architect review;
* an architectural decision;
* a replacement for the governing assignment;
* authority to begin later work;
* a narrative project diary.

The operating handoff is:

> The Builder records evidence.
> The Producer relays completion.
> The Architect reviews the assignment against the evidence.

## Repository Location

Repositories using this specification should maintain:

```text
builder/
├── README.md
└── completions/

```

Completion records should be organized by assignment pattern:

```text
builder/completions/publish/
builder/completions/implement/
builder/completions/merge/
builder/completions/correct/
builder/completions/investigate/

```

Additional pattern directories may be created only when a recurring distinction materially changes the required evidence.

A new directory should not be created merely to describe a project, domain, tool, model, or temporary workflow.

## Completion Record Identity

Each Builder assignment should create one completion record.

The filename should be stable, descriptive, and sortable.

Recommended format:

```text
YYYY-MM-DD_<assignment-id-or-short-name>_completion.md

```

Examples:

```text
builder/completions/publish/2026-07-18_review-protocol_completion.md
builder/completions/implement/2026-07-22_connection-reconciliation_completion.md
builder/completions/merge/2026-07-18_pr-8_completion.md

```

When the governing assignment has a canonical identifier, that identifier should be used.

Examples:

```text
2026-07-22_p2-wo05_completion.md
2026-07-18_pr-8_completion.md

```

The Builder must not overwrite an unrelated prior completion record.

If corrective work follows an earlier assignment, the corrective record should identify the earlier record rather than replacing it.

## Authority

### Producer

The Producer:

* authorizes the Builder assignment;
* may require or waive a completion record when repository constraints make one inappropriate;
* receives the concise completion notice;
* returns or identifies that notice to the Architect for review;
* retains final acceptance authority.

The Producer is not expected to interpret the technical completion evidence.

### Architect

The Architect:

* defines the governing assignment or implementation specification;
* identifies the expected completion-record pattern when necessary;
* reads the Builder completion record;
* compares the record against the governing assignment;
* independently verifies material claims when proportionate tools are available;
* classifies discrepancies and findings under the Review Protocol;
* recommends acceptance, correction, investigation, or Producer decision.

The Architect must not treat the existence of a completion record as proof that the work is correct.

### Builder

The Builder:

* performs the authorized assignment;
* creates or updates only the authorized completion record;
* records material technical evidence accurately;
* distinguishes verified facts from interpretation;
* identifies limitations, blockers, mistakes, recovery actions, and findings;
* provides the Producer with a concise completion notice;
* stops at the assignment boundary.

The Builder must not place Architect conclusions or Producer acceptance decisions in the completion record.

## Assignment Integration

A governing assignment may identify:

* the completion-record path;
* the assignment pattern;
* the canonical assignment identifier;
* evidence required beyond the defaults in this specification;
* whether the completion record is created on the implementation branch or in a later closeout assignment.

When those details are not specified, the Builder should apply this specification proportionately.

The completion record normally belongs in the same branch and pull request as the completed work when:

* the assignment explicitly authorizes it;
* the record describes that exact branch state;
* including the record does not violate an exact changed-file constraint;
* the record is part of the repository’s normal completion process.

The completion record should be created in a separate closeout assignment when:

* the implementation assignment authorizes an exact file set that excludes the record;
* the implementation must remain frozen after accepted validation;
* the record requires final commit, pull-request, merge, deployment, or remote-state information unavailable before completion;
* separating evidence from implementation materially improves review or recovery.

The Architect should choose the boundary that preserves truthful evidence without creating unnecessary ceremony.

## Retroactive Reconstruction

A Producer may authorize the Builder to reconstruct completion records for assignments performed before this specification was adopted or before completion records were consistently maintained.

The objective of retroactive reconstruction is repository completeness, not conversation completeness.

The absence of an original Builder conversation or execution transcript does not, by itself, justify omitting an assignment when reliable repository evidence demonstrates that the assignment occurred.

For each material claim, the Builder should use the highest-confidence evidence reasonably available within the authorized evidence boundary.

The default evidence precedence is:

1. original Builder execution transcript or contemporaneous Builder completion response;
2. repository commits, branches, and tags;
3. pull-request records, review history, and merge evidence;
4. contemporaneous validation or closeout artifacts;
5. directly observable repository state;
6. clearly identified Builder inference.

This precedence applies per claim rather than per record. A reconstructed record may therefore use different evidence classes for different facts.

A lower-ranked source may supplement a higher-ranked source when it adds non-conflicting detail. It must not silently override stronger evidence.

When evidence sources conflict, the Builder must:

* identify the conflict;
* prefer the most direct and authoritative evidence for the specific claim;
* preserve material uncertainty;
* record the conflict as a limitation or finding when it affects interpretation.

The Builder must not invent:

* commands that cannot be verified;
* validation that cannot be demonstrated;
* unrecorded intent;
* conversational instructions that are unavailable;
* exact starting or final states unsupported by evidence;
* authorship or execution details not established by the available record.

Unknown information should be recorded as unknown or unavailable. It should not cause the entire assignment to be omitted when the assignment and its material outcome can otherwise be reconstructed honestly.

A retroactively reconstructed completion record should identify:

* that the record was reconstructed after the assignment;
* the historical assignment or change represented;
* the reconstruction date;
* the evidence sources inspected;
* which material claims were directly verified;
* which claims were inferred;
* unresolved limitations or conflicts.

Retroactive reconstruction does not convert repository history into proof of unrecorded execution details. It creates the most accurate durable record supported by the available evidence.

The Builder should include every assignment within the authorized reconstruction scope that can be established from sufficient repository evidence, even when the original Builder conversation is unavailable.

## Record Status

Every completion record must identify one status:

* Complete;
* Blocked;
* Partially Complete;
* Superseded.

### Complete

Use when the active command was performed, required validation was completed or bounded limitations were recorded, and the assignment reached its stopping condition.

### Blocked

Use when faithful or safe completion could not proceed.

The record must identify the blocker, preserved state, completed work, uncompleted work, and smallest next action needed.

### Partially Complete

Use only when the assignment explicitly permits partial completion or when interruption leaves durable authorized work that must be preserved and reviewed.

Partial completion must not be described as complete.

### Superseded

Use when a later authorized record replaces the evidentiary relevance of an earlier record.

The earlier record should remain present and should point to the superseding record.

## Common Record Header

Every completion record should begin with:

```markdown
# Builder Completion Record

## Assignment

- Assignment:
- Assignment identifier:
- Active command:
- Pattern:
- Status:
- Repository or environment:
- Completion-record path:
- Governing artifact or specification:
- Builder model or environment:
- Date completed:

```

The Builder model or environment may identify the execution context, such as:

```text
Claude Code
OpenAI Codex
Local shell with filesystem tools

```

This field is for provenance and capability interpretation.

It does not change the authority of the record.

For a retroactively reconstructed record, the Builder should additionally include:

```markdown
- Record type: Retroactive reconstruction
- Historical assignment date:
- Reconstruction date:
- Evidence sources:

```

The historical assignment date and reconstruction date must remain distinct. When the historical assignment date cannot be determined precisely, the Builder should record the narrowest supported date or range and identify the limitation.

## Common Evidence Sections

Every completion record should contain the following sections as applicable.

### Authorized Scope

Record:

* the objective;
* permitted files, systems, or operations;
* prohibited work;
* stopping condition;
* special authority such as push, pull-request creation, merge, deployment, migration, or destructive action.

### Starting State

Record:

* repository or environment identity;
* starting branch;
* starting commit or state;
* relation to the authoritative or remote state;
* staged changes;
* unstaged changes;
* untracked files;
* relevant pre-existing conditions.

The record should not reproduce irrelevant environment details.

### Work Performed

Record the material actions actually performed.

Distinguish between:

* planned actions;
* attempted actions;
* successful actions;
* recovered mistakes;
* actions not performed.

### Changed Scope

Record:

* files created;
* files modified;
* files moved;
* files deleted;
* branches created or changed;
* commits created;
* pull requests created or updated;
* remote or external state changed;
* runtime or data state changed.

When exact changed-file scope matters, list every changed file.

### Validation

Record:

* validation required;
* validation performed;
* commands, checks, or comparisons used;
* results;
* failures;
* skipped checks;
* remaining uncertainty.

Passing validation must not be described more broadly than the evidence supports.

### Final State

Record:

* final branch or environment;
* final commit or state;
* working-tree status;
* remote branch state;
* pull-request state;
* authoritative branch state;
* deployment or runtime state;
* assignment stopping condition reached.

### Limitations

Record material capability, evidence, environment, or validation limitations.

Write `None` only when no material limitation exists.

### Blockers

Record any blocker that prevented or constrained completion.

Write `None` only when no blocker exists.

### Non-Blocking Findings

Record adjacent concerns, opportunities, inefficiencies, or observations that do not alter the assignment outcome.

Findings do not authorize additional work.

### Builder Attestation

The Builder should conclude with:

```markdown
## Builder Attestation

I completed or stopped this assignment according to the active command and governing authority described above.

The evidence in this record distinguishes performed and verified work from assumptions, limitations, blockers, and findings.

No adjacent work was begun except where explicitly recorded and authorized.

```

## Publication Completion Record

A publication record should additionally identify:

* approved source artifact;
* authorized destination path;
* source-delivery method;
* formatting adjustments made;
* fidelity-validation method;
* fidelity result;
* exact publication file scope;
* commit and pull-request evidence;
* confirmation that embedded document instructions were not executed.

Recommended pattern:

```markdown
## Publication Evidence

- Approved source:
- Published path:
- Source-delivery method:
- Formatting adjustments:
- Fidelity comparison:
- Fidelity result:
- Published commit:
- Pull request:
- Embedded instructions executed: No

```

## Document-Creation Completion Record

Document creation is distinct from publication.

A document-creation record should identify:

* requested document purpose;
* governing decisions and references;
* document created;
* drafting scope;
* unresolved decisions;
* assumptions;
* review or approval status;
* whether the document was published.

Creating a draft does not imply that the document is approved or authoritative.

Recommended pattern:

```markdown
## Document-Creation Evidence

- Document purpose:
- Output path or location:
- Governing references:
- Drafting scope:
- Unresolved decisions:
- Producer approval status:
- Published: Yes / No

```

When an Architect drafts the content conversationally and the Builder only transfers approved text into a repository, the Builder should classify the assignment as Publication, not Document Creation.

## Implementation Completion Record

An implementation record should additionally identify:

* approved implementation specification;
* implementation objective;
* components or systems changed;
* bounded implementation decisions;
* tests and checks;
* test counts when material;
* runtime or manual validation;
* rollback or recovery evidence when required;
* known implementation limitations;
* migration, data, or deployment effects;
* implementation commit and pull request.

Recommended pattern:

```markdown
## Implementation Evidence

- Approved specification:
- Components changed:
- Bounded implementation decisions:
- Automated validation:
- Manual validation:
- Runtime or data effects:
- Rollback or recovery validation:
- Implementation commit:
- Pull request:

```

## Merge Completion Record

A merge record should additionally identify:

* pull request;
* target branch;
* verified pre-merge state;
* merge authority;
* merge method;
* merge commit;
* post-merge target-branch state;
* confirmation that no file revisions or adjacent work occurred during the merge assignment.

Recommended pattern:

```markdown
## Merge Evidence

- Pull request:
- Target branch:
- Pre-merge verification:
- Merge authority:
- Merge method:
- Merge commit:
- Final target-branch commit:
- File revisions during merge assignment: None

```

## Corrective Completion Record

A corrective record should additionally identify:

* original assignment;
* original completion record;
* review outcome authorizing correction;
* exact discrepancy;
* bounded corrective scope;
* correction performed;
* regression validation;
* unaffected work preserved;
* superseded claims or evidence.

Recommended pattern:

```markdown
## Correction Evidence

- Original assignment:
- Original completion record:
- Authorized discrepancy:
- Correction performed:
- Regression validation:
- Unaffected work preserved:
- Superseded evidence:

```

## Investigation Completion Record

An investigation record should additionally identify:

* question investigated;
* authorized evidence boundary;
* whether the investigation was read-only;
* evidence inspected;
* known facts;
* inferences;
* unknowns;
* conclusion;
* whether correction, implementation, or Producer decision is recommended.

An investigation must not silently become implementation.

Recommended pattern:

```markdown
## Investigation Evidence

- Investigated question:
- Evidence boundary:
- Read-only:
- Evidence inspected:
- Known:
- Inferred:
- Unknown:
- Conclusion:
- Recommended next authority:

```

## Producer-Facing Completion Notice

The Builder’s conversational response to the Producer should be concise.

For a completed assignment, the default response is:

```text
The Builder assignment is complete.

Completion record:
<repository path or durable link>

```

The Builder may add one short line when the stopping condition materially matters:

```text
The pull request is open and has not been merged.

```

For a blocked assignment, the default response is:

```text
The Builder assignment is blocked.

Completion record:
<repository path or durable link>

```

The Producer-facing response should not reproduce the technical record unless the Producer explicitly asks for it.

The concise response must not conceal:

* blocked status;
* partial completion;
* failed required validation;
* destructive or irreversible effects;
* a Producer decision required before safe continuation.

## Architect Handoff

When the Producer provides or identifies a Builder completion notice to the Architect, that notice acts as a request to review the completed assignment.

The Architect should:

1. identify the governing assignment or deployment artifact;
2. read the referenced completion record;
3. compare authorized scope with recorded work;
4. verify material claims proportionately;
5. inspect changed scope, validation, and final state;
6. classify discrepancies and findings;
7. recommend an outcome under the Review Protocol;
8. identify the next authorized action.

The Architect should not require the Producer to restate the technical completion report when the durable record is available.

A completion notice does not imply Producer acceptance.

## Record Integrity

Completion records must be:

* factual;
* assignment-specific;
* attributable;
* durable;
* reviewable;
* explicit about uncertainty;
* preserved after acceptance.

The Builder must not:

* alter an earlier record to hide a mistake;
* report validation that was not performed;
* omit a material scope deviation;
* describe attempted work as completed;
* include speculative Architect conclusions;
* record Producer acceptance before it occurs;
* use the completion record to authorize adjacent work.

Material corrections to a completion record should occur through a new commit with a visible explanation.

When the correction changes the assignment outcome, a corrective completion record should be created.

## Relationship to Pull Requests and Commits

A completion record may reference Git evidence, but it does not replace Git history.

Git history shows what changed.

The completion record explains:

* why the change was authorized;
* what the Builder intended and performed;
* what was validated;
* what limitations remain;
* where the Builder stopped.

Pull-request descriptions may summarize the completion record but should not become the only durable evidence location.

## Relationship to Work Orders

When a work order or implementation specification exists:

* the work order defines the authorized work;
* the completion record reports execution evidence;
* the Review Protocol governs evaluation;
* the Architect recommends the outcome;
* the Producer accepts, rejects, or redirects.

The completion record should reference the work order.

It should not duplicate the full work order unless necessary to make the evidence intelligible.

## Proportionality

Completion records should be proportionate.

A one-file publication record may be brief.

A migration, deployment, destructive operation, financial correction, or security-sensitive implementation may require extensive evidence.

Required headings may contain `Not applicable` when the distinction is relevant but no evidence is required.

The Builder should not add volume merely to appear rigorous.

The record must contain enough evidence for a different qualified Builder or Architect, using a different LLM or tool environment, to understand:

* what was authorized;
* what occurred;
* what was verified;
* what remains uncertain;
* where the assignment stopped.

## Completion Standard

This specification is satisfied when:

* the assignment has a durable completion record;
* the record uses the appropriate assignment pattern;
* the record identifies authority, scope, work, validation, and final state;
* limitations, blockers, and findings are explicit;
* the Producer receives a concise completion notice;
* the notice identifies the completion record;
* the Architect can review the assignment without requiring the Producer to relay technical evidence manually;
* the record does not claim acceptance or authorize later work.

## Core Principles

> Detailed evidence belongs in the repository.
> The Producer needs status and location, not an execution transcript.
> The Architect compares authority with evidence.
> Completion records preserve handoff across models, tools, and conversations.
> A completion record reports what happened; it does not decide whether the result is accepted.
