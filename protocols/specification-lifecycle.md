# Specification Lifecycle

## Purpose

This protocol defines how an idea becomes authorized work under the Aurora Operating System.

It separates discussion, architectural interpretation, Producer approval, repository publication, Builder execution, review, and acceptance.

The objective is to prevent drafts, conversations, and unapproved AI output from being mistaken for authoritative instructions.

## Core distinction

> The prompt activates the role.
> The specification authorizes the work.

A prompt is a temporary invocation delivered to a person or AI system.

A specification is a durable artifact that records the approved interpretation of the work.

Repeated operating rules belong in role or protocol artifacts. The current prompt should contain only the invocation, the specification location, and assignment-specific direction.

## Lifecycle states

A specification may pass through the following states:

1. **Proposed**
2. **Drafted**
3. **Under Producer Review**
4. **Approved**
5. **Published**
6. **Assigned**
7. **Implemented**
8. **Reviewed**
9. **Accepted**
10. **Superseded or Archived**

These states describe authority and progress. They are not interchangeable.

## 1. Proposed

A need, objective, problem, or desired change has been identified.

At this stage:

* the Producer's intent may still be incomplete;
* multiple interpretations may exist;
* no implementation is authorized;
* exploratory discussion is allowed.

A proposal may exist only in conversation, notes, or an issue.

## 2. Drafted

The Architect converts the Producer's intent into a draft specification.

A draft should identify:

* objective;
* scope;
* exclusions;
* governing artifacts;
* required outputs;
* constraints;
* validation expectations;
* acceptance conditions;
* known uncertainties.

A draft is an architectural interpretation, not authorization.

The Builder must not execute a draft unless the Producer explicitly authorizes provisional execution.

## 3. Under Producer Review

The Producer reviews the draft for congruence.

The review should ask:

* Does this describe the outcome actually wanted?
* Is anything important missing?
* Has the scope expanded unnecessarily?
* Are the exclusions correct?
* Are the validation requirements proportionate?
* Are unresolved decisions visible?
* Would successful execution satisfy the Producer's intent?

The Architect may revise the draft in response to Producer review.

## 4. Approved

A specification becomes approved when the Producer explicitly accepts its substantive content.

Approval may occur before repository publication.

Approval should be clear enough that another participant can distinguish an approved specification from an unfinished draft.

Examples include:

* an explicit Producer statement in the working conversation;
* an approval record in a project artifact;
* a repository status field changed to `Approved`;
* a reviewed pull request containing the specification.

Approval is an authority decision, not merely a file state.

## 5. Published

Publication places the approved specification into its authoritative artifact location.

Publication may be performed by:

* the Producer directly;
* the Architect, when the environment has write authority and the Producer has authorized publication;
* the Builder under a specification-publication assignment.

Publication must preserve the approved meaning.

If a Builder publishes the specification, the Builder should read the file back and confirm that it matches the approved text.

A file's existence does not prove Producer approval. A specification is authoritative because it was approved and published through the recognized process.

## 6. Assigned

The Producer or Architect invokes a Builder and directs it to execute the published specification.

A normal Builder invocation may be as small as:

> You are the Builder.
> Read your role governance at `[path]`.
> Execute the approved specification at `[path]`.

The assignment may add immediate operational details such as:

* repository;
* branch instructions;
* relevant environment;
* required reporting destination;
* whether publication, implementation, or both are authorized.

The assignment prompt must not silently change the approved specification.

If the prompt and specification conflict, the conflict must be resolved before implementation.

## 7. Implemented

The Builder performs the authorized scope and records evidence.

Implementation should remain bounded by:

* the approved specification;
* Builder role governance;
* governing project artifacts;
* the demonstrated capabilities of the execution environment.

Implementation does not automatically mean the work is correct, congruent, or accepted.

## 8. Reviewed

The Architect reviews the implementation against the approved specification.

Review should distinguish at least three questions:

### Correctness

Was the work performed accurately?

### Completeness

Was all authorized scope completed and validated?

### Congruence

Does the result still serve the Producer's actual intent?

The Architect should review evidence rather than rely only on the Builder's summary.

Findings may result in:

* acceptance recommendation;
* a corrective assignment;
* specification revision;
* additional validation;
* architectural escalation.

## 9. Accepted

The Producer accepts the completed work.

Acceptance confirms that the result is satisfactory for the intended outcome.

Acceptance may occur even when known limitations remain, provided those limitations are understood and explicitly accepted.

Builder completion and Architect approval do not replace Producer acceptance.

## 10. Superseded or Archived

A specification may later be replaced or made obsolete.

A superseded specification should remain available when historical traceability matters, but it must not appear to be the current governing instruction.

The replacement artifact should identify what it supersedes.

Archived specifications must not be used for new implementation unless deliberately reauthorized.

## Publication modes

### Manual publication

The Producer copies the approved specification into the repository.

This mode provides the clearest human control point and is well suited to users learning the process.

### Assisted publication

The Builder publishes approved text but does not execute it during the same assignment.

The Producer or Architect reviews the publication before issuing a separate execution assignment.

### Combined publication and execution

The Builder publishes and executes the specification in one assignment.

This mode is valid only when the Producer explicitly authorizes both actions.

It is best reserved for mature workflows, low-risk changes, or specifications whose publication can be verified deterministically before execution proceeds.

## Change control after approval

A substantive change to an approved specification requires renewed Producer approval.

Substantive changes include changes to:

* objective;
* scope;
* exclusions;
* architecture;
* required outputs;
* acceptance criteria;
* destructive authority;
* migration behavior;
* security or confidentiality boundaries.

Minor corrections that do not change meaning may be published without repeating the full approval cycle, but they should remain visible in repository history.

The Builder must not rewrite an approved specification to match the implementation it prefers.

## Emergency or exploratory work

Some assignments may need to occur before a complete specification exists.

Such work must be explicitly classified, for example as:

* investigation;
* experiment;
* read-only assessment;
* proof of concept;
* recovery action.

The assignment must state what authority is granted and what remains prohibited.

Exploratory output does not become production architecture merely because it works.

## Failure modes this protocol prevents

This lifecycle is designed to prevent:

* an AI-generated draft being treated as approved;
* a Builder expanding scope while implementing;
* conversational instructions disappearing between sessions;
* publication being mistaken for execution authority;
* implementation being mistaken for acceptance;
* a polished but incongruent result being accepted without review;
* obsolete specifications remaining silently authoritative.

## Normal operating cycle

The standard cycle is:

```text
Producer directive
        ↓
Architect drafts specification
        ↓
Producer reviews
        ↓
Producer approves
        ↓
Specification is published
        ↓
Builder is assigned
        ↓
Builder implements and validates
        ↓
Architect reviews
        ↓
Producer accepts
```

## Operating principle

> Authority should be visible in artifacts and decisions, not inferred from fluency, file existence, or tool access.
