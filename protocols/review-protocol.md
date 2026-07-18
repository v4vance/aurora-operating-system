# Review Protocol

## Purpose

This protocol defines how an Architect reviews Builder work under the Aurora Operating System.

Review determines whether the Builder performed the authorized assignment faithfully, preserved governing authority, produced sufficient evidence, and stopped within scope.

Review does not replace Producer acceptance.

The Architect evaluates the result and recommends an outcome. The Producer retains final authority to accept, reject, redirect, or require further work.

## Scope

This protocol applies to Builder assignments performed under either operating command:

* Publish;
* Implement.

It may be used to review:

* artifact publication;
* document or repository changes;
* implementation work;
* tests and validation;
* work-order completion;
* corrective work;
* pull requests;
* merge operations;
* final repository state.

The protocol should be applied proportionately.

A low-risk publication of one approved file does not require the same depth of review as a migration, destructive operation, or architectural implementation.

Proportionality does not permit material claims to go unverified when verification is reasonably available.

## Authority Model

### Producer

The Producer:

* approves the governing artifact or specification;
* authorizes publication or implementation;
* retains final acceptance authority;
* resolves questions requiring Producer judgment;
* may accept, reject, or modify the Architect’s recommendation.

### Architect

The Architect:

* identifies the assignment being reviewed;
* reads the governing authority;
* examines the Builder report;
* verifies material claims when evidence and tools are available;
* identifies discrepancies, limitations, blockers, and findings;
* classifies the review outcome;
* recommends the next action;
* does not silently correct or implement the work.

### Builder

The Builder:

* performs the authorized assignment;
* validates the result;
* reports evidence;
* discloses limitations, blockers, mistakes, and findings;
* preserves the final state for review;
* performs corrective work only after receiving new authorization.

The operating relationship remains:

> The Builder executes.
> The Architect interprets.
> The Producer decides.

## Review Activation

A review begins when the Producer supplies or identifies a Builder completion report, pull request, commit, repository state, artifact, or other completed result for evaluation.

The Architect should identify:

* the active Builder command;
* the approved artifact or specification;
* the authorized scope;
* the Builder’s reported result;
* the evidence available for verification;
* the decision the Producer needs next.

Review authority permits evaluation and recommendation.

It does not authorize the Architect to publish, implement, correct, merge, or otherwise modify the result.

## Review Inputs

The Architect should obtain, as applicable:

* the Builder Role Specification;
* the Architect Role Specification;
* the approved artifact or implementation specification;
* named governing artifacts;
* the Builder completion report;
* repository or working-environment evidence;
* changed-file lists;
* diffs or patches;
* commit metadata;
* pull-request metadata;
* validation output;
* test results;
* final-state evidence;
* disclosed limitations, blockers, mistakes, and findings.

The Architect should not require every possible input when the available evidence is already sufficient for a reliable conclusion.

When required evidence is unavailable, the Architect must state what cannot be verified and whether that uncertainty changes the review outcome.

## Review Standard

The central review question is:

> Did the Builder perform the authorized assignment faithfully, validate it proportionately, report it accurately, and stop within scope?

The Architect should evaluate five dimensions:

1. Authority;
2. Fidelity;
3. Scope;
4. Evidence;
5. Final state.

A result should not be accepted solely because it appears useful, well written, functional, or successful.

It must also be authorized and congruent.

## Authority Review

The Architect must determine:

* whether the Builder role was activated;
* whether the active command was clear;
* whether the Producer authorized that command;
* whether the approved artifact or specification was identifiable;
* whether the Builder acted under the correct authority;
* whether any later action required separate authorization.

For publication review, the Architect should confirm that publication authority was not treated as implementation authority.

For implementation review, the Architect should confirm that the work was governed by an approved specification rather than Builder inference.

For merge review, the Architect should confirm that merge authority was explicit and separate when the preceding assignment stopped at pull-request creation.

A technically correct result produced without required authority is not fully acceptable.

## Fidelity Review

For publication, fidelity means that the repository artifact preserves the approved source wording and meaning, except for authorized formatting adjustments.

The Architect should evaluate:

* source-to-publication agreement;
* correct destination path;
* preservation of wording and meaning;
* absence of unauthorized revisions;
* treatment of embedded instructions as text rather than commands;
* consistency with required file-format conventions.

For implementation, fidelity means that the result satisfies the approved specification and preserves governing architecture.

The Architect should evaluate:

* required outputs;
* stated constraints;
* acceptance conditions;
* prohibited work;
* stopping conditions;
* architectural invariants;
* approved terminology and boundaries.

The Architect should distinguish a harmless implementation choice from a change to approved meaning or architecture.

## Scope Review

The Architect must compare the authorized scope with the actual changed scope.

This may include:

* files created;
* files modified;
* files moved;
* files deleted;
* repository branches;
* commits;
* pull requests;
* external systems affected;
* data or runtime state changed;
* adjacent work begun.

The Architect should determine whether the Builder:

* changed only authorized files or systems;
* avoided absorbing unrelated work;
* stopped before later or adjacent assignments;
* avoided unrequested improvements;
* avoided destructive operations without authority;
* preserved pre-existing work;
* disclosed any accidental or temporary out-of-scope action.

A temporary mistake does not automatically require rejection when the Builder detected it, recovered safely, verified the final state, and reported it accurately.

The review must evaluate both the mistake and the recovery evidence.

## Evidence Review

The Architect must distinguish among:

* Builder claims;
* Builder-supplied evidence;
* evidence independently verified by the Architect;
* assumptions or inferences;
* facts that remain unknown.

Evidence may include:

* file contents;
* normalized source comparisons;
* diffs;
* commit SHAs;
* branch metadata;
* pull-request state;
* test output;
* syntax or formatting checks;
* build output;
* execution logs;
* manual verification;
* final working-tree status;
* external system confirmation.

The Architect should independently verify material claims when:

* suitable tools are available;
* the cost is proportionate;
* the claim affects acceptance;
* the operation changed an authoritative or shared state;
* the Builder disclosed a mistake;
* the result depends on exact changed-file scope;
* the result depends on a merge, push, deployment, or other remote action.

The Architect must not imply independent verification when only the Builder’s report was reviewed.

## Validation Review

The Architect should determine whether validation was appropriate to the assignment.

For publication, validation may include:

* source comparison;
* file read-back;
* exact changed-file confirmation;
* Markdown or formatting inspection;
* commit verification;
* pull-request verification;
* confirmation that document instructions were not executed.

For implementation, validation may include:

* automated tests;
* targeted tests;
* regression tests;
* syntax or type checks;
* build verification;
* runtime checks;
* manual scenario validation;
* database or state inspection;
* rollback verification;
* final diff inspection.

The Architect should evaluate:

* whether required validation was performed;
* whether the validation actually tests the claimed result;
* whether failures were disclosed;
* whether skipped validation leaves material uncertainty;
* whether the Builder overstated what the evidence proves.

Passing validation is evidence of the tested claim, not proof of every possible property.

## Final-State Review

The Architect should confirm the final state relevant to the assignment.

This may include:

* working tree clean or intentionally dirty;
* correct branch;
* expected commit at branch head;
* remote branch present;
* pull request open, closed, or merged as authorized;
* authoritative branch updated;
* expected file present;
* no unauthorized files changed;
* no staged or untracked residue;
* no unreported partial external change;
* no later work begun.

The required final state depends on the assignment’s stopping condition.

A publication assignment that was authorized only through pull-request creation is not incomplete merely because it was not merged.

A merge assignment is not complete merely because the pull request was previously approved; the merged state must be verified.

## Discrepancy Classification

A discrepancy is a difference between the authorized or reported result and the evidence.

The Architect should classify discrepancies by effect rather than by appearance.

### Blocking Discrepancy

A blocking discrepancy prevents acceptance of the current result.

Examples include:

* wrong active command;
* missing Producer authority;
* unauthorized implementation during publication;
* material departure from approved wording or architecture;
* incorrect target repository or path;
* unauthorized files or systems changed;
* required validation failed;
* final state cannot be established;
* Builder report materially contradicts available evidence;
* destructive or irreversible work occurred without authority.

### Correctable Discrepancy

A correctable discrepancy requires bounded corrective work but does not require a new architectural decision.

Examples include:

* formatting error;
* omitted required report field;
* incorrect filename;
* incomplete but straightforward validation;
* isolated implementation defect within approved architecture;
* unintended file included in a commit;
* pull-request description that inaccurately states the scope.

Corrective work requires a new Builder assignment.

The Architect does not silently perform the correction.

### Investigative Discrepancy

An investigative discrepancy requires more evidence before acceptance or correction can be selected confidently.

Examples include:

* reported tests cannot be confirmed;
* remote and local states appear inconsistent;
* a temporary mistake may have affected unrelated work;
* a result is plausible but the relevant diff is unavailable;
* runtime behavior differs from static evidence;
* the cause or extent of a failure is unknown.

Investigation should be bounded to the smallest evidence-gathering action needed.

### Producer-Decision Discrepancy

A Producer-decision discrepancy exposes an unresolved choice, authority question, or architectural conflict.

Examples include:

* two approved artifacts conflict;
* implementation revealed that the approved design cannot be performed as stated;
* accepting the result would revise a prior decision;
* a nonconforming result may be preferable to the existing specification;
* required corrective work would broaden scope;
* risk tolerance must be determined by the Producer.

The Architect must present the decision clearly rather than hiding it inside a technical recommendation.

### Non-Blocking Finding

A non-blocking finding does not prevent acceptance of the current assignment.

Examples include:

* an adjacent improvement opportunity;
* a future documentation need;
* a harmless procedural inefficiency;
* a limitation already permitted by the specification;
* an unrelated repository concern;
* a minor recovery event with verified final state and no residual effect.

Non-blocking findings should be recorded without converting them into unauthorized work.

## Review Outcomes

The Architect should recommend one of five outcomes.

### Accept

Recommend Accept when:

* authority was valid;
* scope was respected;
* the result is faithful;
* validation is sufficient;
* material claims are verified or adequately supported;
* the final state matches the assignment;
* no blocking discrepancy remains.

Acceptance means the reviewed assignment satisfies its current authority.

It does not authorize the next assignment automatically.

### Accept With Recorded Non-Blocking Findings

Recommend Accept with recorded non-blocking findings when:

* all acceptance conditions are met;
* one or more findings should remain visible;
* the findings do not require correction of the accepted result;
* the findings do not undermine material claims;
* later consideration may be useful.

The Architect should state whether each finding belongs in:

* a future work order;
* a backlog;
* a later governance review;
* no further action.

### Correct

Recommend Correct when:

* the assignment is understandable and remains architecturally valid;
* a bounded defect or omission prevents acceptance;
* the correction does not require a new Producer decision;
* the required corrective scope can be specified clearly.

The Architect should identify:

* the exact discrepancy;
* the evidence;
* the required correction;
* the files or systems permitted to change;
* required validation;
* the stopping condition.

### Investigate

Recommend Investigate when:

* evidence is insufficient;
* the extent or cause of a discrepancy is unknown;
* correction would be premature;
* acceptance would rely on an unsupported assumption.

The investigation should be read-only whenever possible.

The Architect should identify:

* the question to resolve;
* the evidence needed;
* the permitted inspection scope;
* prohibited modifications;
* the condition that ends the investigation.

### Return for Producer Decision

Recommend Return for Producer decision when:

* authority is unclear;
* approved artifacts conflict;
* the next action would alter architecture, scope, risk, or intent;
* more than one congruent path exists;
* acceptance would effectively revise an approved decision;
* the Architect cannot choose without assuming Producer authority.

The Architect should present:

* the decision required;
* known facts;
* material uncertainty;
* available options;
* consequences of each option;
* the Architect’s recommendation, when one can be made without obscuring Producer authority.

## Review Report

A review report should contain, as applicable:

* assignment reviewed;
* active Builder command;
* governing artifact or specification;
* Builder-reported result;
* evidence inspected;
* claims independently verified;
* claims not independently verified;
* authorized scope;
* actual changed scope;
* validation assessment;
* final-state assessment;
* discrepancies;
* non-blocking findings;
* review outcome;
* rationale;
* next authorized action;
* decisions reserved for the Producer.

The report should clearly separate:

* Builder report;
* verified evidence;
* Architect interpretation;
* Architect recommendation;
* Producer decision.

## Review Depth

The Architect should use the minimum review depth sufficient for a reliable outcome.

### Basic Review

Appropriate for low-risk, bounded publication or administrative work.

May include:

* report inspection;
* changed-file verification;
* artifact read-back;
* commit or pull-request verification;
* final-state confirmation.

### Standard Review

Appropriate for ordinary implementation work.

May include:

* governing-artifact comparison;
* diff inspection;
* changed-scope verification;
* validation review;
* selected independent checks;
* final-state confirmation.

### Enhanced Review

Appropriate for high-risk, destructive, migratory, security-sensitive, financially consequential, or difficult-to-reverse work.

May include:

* complete evidence inspection;
* independent reproduction of critical validation;
* rollback or recovery verification;
* cross-system state checks;
* review of failure handling;
* explicit Producer risk decision.

The assignment’s risk determines review depth, not the Builder’s confidence.

## Mistakes and Recovery

A disclosed mistake should be evaluated according to:

* what occurred;
* whether authority or scope was crossed;
* whether persistent state changed;
* whether unrelated work was endangered;
* how quickly the mistake was detected;
* what recovery was performed;
* whether recovery was verified;
* whether residual uncertainty remains;
* whether the final report was accurate.

Transparent disclosure supports trust but does not erase consequences.

A fully recovered, non-destructive mistake with verified final state may be a non-blocking finding.

A mistake with unknown effects requires investigation.

A mistake that altered authority, architecture, or irreversible state may require correction or Producer decision.

## Repeated Findings

The Architect should not convert a single observation into permanent governance automatically.

When the same non-blocking finding recurs, the Architect should consider whether it indicates:

* an unclear role specification;
* an incomplete protocol;
* a recurring prompt defect;
* a missing project convention;
* a tool limitation;
* unnecessary process;
* a need for a new Producer decision.

A recurring finding should become a governance proposal only when the pattern is established and the proposed rule belongs at the relevant authority layer.

## Corrective Assignments

When the review outcome is Correct, the Architect may draft a corrective Builder assignment after the Producer authorizes correction.

A corrective assignment should:

* identify the original assignment;
* identify the accepted governing authority;
* state the exact discrepancy;
* define the smallest corrective scope;
* prohibit unrelated improvement;
* identify required validation;
* preserve unaffected accepted work;
* define the stopping condition;
* require an updated completion report.

Correction does not reopen the entire assignment unless the discrepancy affects the entire result.

## Investigation Assignments

When the review outcome is Investigate, the Architect may draft a bounded investigation assignment after Producer authorization.

An investigation assignment should:

* be read-only unless modification is essential and explicitly authorized;
* identify the exact question;
* identify permitted evidence sources;
* prohibit implementation or correction;
* require preservation of current state;
* require reporting of known, inferred, and unknown facts;
* stop when the identified question is answered or the evidence boundary is reached.

Investigation produces evidence.

It does not silently become correction or implementation.

## Acceptance and Next Work

Acceptance closes the reviewed assignment.

It does not:

* merge an unmerged pull request;
* authorize publication;
* authorize implementation;
* authorize correction;
* begin the next work order;
* approve an adjacent recommendation;
* convert findings into requirements.

Each later action requires its own appropriate authority.

The Architect should state the next available action, but the Producer decides whether to authorize it.

## Instruction Precedence

When review sources conflict, the Architect applies the precedence defined by the Architect Role Specification.

Within the review itself:

1. approved Producer decisions;
2. approved governing artifacts;
3. the approved assignment artifact or specification;
4. the Builder Role Specification;
5. the Builder completion report;
6. repository and external evidence;
7. Architect assumptions.

Repository evidence may disprove a Builder factual claim.

Repository evidence does not by itself override approved Producer intent or architecture.

When evidence shows that approved authority cannot be performed as stated, the matter returns to the Producer.

## Completion Standard

A review is complete when:

* the assignment and active command are identified;
* governing authority has been considered;
* material Builder claims have been evaluated;
* available proportionate verification has been performed;
* authorized and actual scope have been compared;
* validation and final state have been assessed;
* discrepancies and findings have been classified;
* a review outcome has been recommended;
* the rationale is explicit;
* the next authorized action is clear;
* Producer acceptance authority has been preserved;
* no unauthorized correction, publication, implementation, or merge has occurred.

## Core Principles

> Review authority, not just output.
> Evidence determines confidence.
> A useful result is not acceptable if it was unauthorized.
> Correction requires new authority.
> Acceptance closes the assignment; it does not begin the next one.
