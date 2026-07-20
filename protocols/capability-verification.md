# Capability Verification Protocol

## Purpose

This protocol defines how to determine what an execution environment can actually do.

AI products, connectors, local agents, desktop applications, web interfaces, subscriptions, permissions, and repository settings may expose different capabilities. A capability must not be assumed merely because an interface appears agentic or because a tool is listed.

Capabilities should be demonstrated through minimal, bounded tests.

## Core principle

> Do not infer a capability when it can be tested safely.

A verified capability is one that has succeeded under known conditions and produced observable evidence.

A failed operation is also useful evidence. It identifies a real boundary and allows the workflow to route around it deliberately.

## Role and environment are separate

A logical role is not the same thing as the product or environment hosting it.

Examples of logical roles include:

* Producer;
* Architect, including its review function;
* Builder.

A domain overlay or project specification may define a separate Reviewer role and its relationship to the Architect. Aurora Core does not define that separate role.

Examples of environments include:

* conversational AI;
* project or work-oriented AI;
* local coding agent;
* repository connector;
* command-line environment;
* web interface.

One environment may support several roles. One role may be performed in several environments.

The Aurora Operating System should define role requirements independently from vendor or product names.

## Capability categories

An environment may need to be evaluated for capabilities such as:

### Repository observation

* locate a repository;
* read the default branch;
* read a named branch;
* inspect files;
* inspect commit history;
* inspect diffs;
* inspect pull requests;
* inspect review comments and check results.

### Repository mutation

* create a branch;
* create or edit files;
* create commits;
* push commits;
* open pull requests;
* respond to reviews;
* merge pull requests;
* delete merged branches.

### Local execution

* access a working tree;
* run commands;
* install dependencies;
* run tests;
* inspect generated files;
* build artifacts.

### External systems

* read connected documents;
* write connected documents;
* access calendars or mail;
* create or update records;
* transfer files;
* invoke APIs.

### Reasoning and coordination

* retain project context;
* compare governing artifacts;
* draft specifications;
* review implementation evidence;
* identify conflicts;
* preserve domain boundaries.

## Minimal-test rule

A capability test should be:

* narrow;
* reversible when possible;
* isolated from production work;
* explicit about prohibited side effects;
* easy to verify independently;
* small enough that failure causes no meaningful harm.

Do not combine several unverified capabilities into one test.

For example, testing branch creation should not also edit files, commit changes, push implementation work, and open a pull request.

## Suggested repository capability sequence

Repository capabilities should be tested in increasing order of consequence.

### 1. Repository read

Ask the environment to:

* identify the default branch;
* read a known file;
* report a known commit.

Evidence:

* correct branch;
* correct content summary;
* matching commit SHA.

### 2. Non-default branch read

Ask the environment to read a known branch and report its latest commit.

Evidence:

* correct branch;
* correct SHA;
* correct ahead/behind relation when available.

### 3. Branch creation

Ask the environment to create a dedicated test branch with no file changes.

Evidence:

* successful operation report;
* branch visible through an independent read;
* correct starting commit.

### 4. File creation

Ask the environment to create one harmless test file on the test branch.

Evidence:

* exact file path;
* exact content;
* resulting commit;
* file visible on the remote branch.

### 5. Commit and push

Ask the environment to commit and push the bounded test change.

Evidence:

* commit SHA;
* remote branch state;
* matching repository history.

### 6. Pull-request creation

Ask the environment to open a draft pull request.

Evidence:

* pull-request number;
* correct base and head branches;
* expected changed files;
* draft status.

### 7. Pull-request mutation

Separately test, when needed:

* adding a comment;
* responding to review;
* updating metadata;
* merging;
* deleting the branch.

Each action should be authorized and verified independently.

## Recording a successful test

A capability verification record should include:

* environment tested;
* date;
* connected account or repository scope, without exposing secrets;
* requested operation;
* exact test instruction;
* expected outcome;
* observed outcome;
* supporting evidence;
* limitations;
* whether the capability should be considered approved for future use.

A successful result in one repository does not always prove the same permission exists in another repository or organization.

## Recording a failed test

A failed capability record should include:

* requested operation;
* exact error or failure message;
* whether any partial action occurred;
* how the final state was verified;
* likely boundary;
* available workaround;
* unresolved uncertainty.

Do not convert a specific observation into a universal claim without evidence.

For example:

> The tested ChatGPT GitHub connector could read the repository but returned `403 — Resource not accessible by integration` when asked to create a branch.

This is more accurate than:

> ChatGPT can never write to GitHub.

Different products, plans, connectors, repository settings, or future versions may behave differently.

## Allow, block, and workaround structure

Instructional documentation for a capability should distinguish three things.

### Allowed

Operations demonstrated to work in the tested environment.

Example:

* read repository files;
* inspect branches;
* inspect pull-request metadata;
* review commits.

### Blocked

Operations demonstrated to fail or known to be unavailable.

Example:

* create a branch through a read-only connector;
* commit repository changes;
* push files.

### Workaround

A safe alternate path that preserves the operating model.

Example:

* the Producer publishes the approved specification manually;
* a write-capable Builder publishes it on a dedicated branch;
* a local coding environment performs implementation;
* the Architect reviews the resulting pull request through read access.

A workaround should preserve authority boundaries rather than bypass them.

## Current observed GitHub connector example

During establishment of the Aurora Operating System repository, the tested ChatGPT GitHub connector demonstrated the ability to:

* read the repository;
* read the default branch;
* inspect a non-default branch;
* report commit SHAs;
* inspect pull-request state.

The same branch-creation test was performed through multiple ChatGPT interfaces.

The requested operation was:

> Create a new branch named `architect/capability-test`, make no file changes, commit nothing, and report whether the branch was successfully created.

The operation failed with:

> `403 — Resource not accessible by integration`

A subsequent read confirmed that the branch did not exist.

No files were changed and no commits were created.

The supported workaround was:

* Aurora drafts the specification;
* the Producer reviews and approves it;
* the Producer publishes it manually, or a write-capable Builder publishes it;
* implementation proceeds through the normal specification lifecycle;
* Aurora reviews repository evidence using read access.

This observation should be treated as specific to the tested connector and conditions, not as a permanent universal statement about all ChatGPT or GitHub integrations.

## Subscription and product uncertainty

A capability may vary by:

* subscription;
* product;
* interface;
* connector type;
* organization policy;
* repository installation scope;
* requested app permissions;
* local credentials;
* product version.

When the cause of a limitation is unknown, record the limitation without inventing an explanation.

An unverified theory such as subscription gating should remain explicitly labeled as a possibility rather than a fact.

## Capability profiles

A role may define a minimum capability profile.

### Architect profile

A fully repository-grounded Architect should be able to:

* read governing artifacts;
* inspect repository state;
* compare implementation with specifications;
* draft durable instructions;
* identify conflicts and uncertainty.

Repository write access may be useful but is not required when an approved publication path exists.

### Builder profile

A repository Builder normally needs to:

* access the target files;
* create or use an authorized branch;
* make changes;
* run validation;
* commit;
* push;
* report evidence.

If an environment lacks one of these capabilities, the assignment must be narrowed or routed to another environment.

### Producer profile

The Producer must be able to:

* express intent;
* review specifications;
* approve or reject work;
* control publication or delegate it;
* accept final results.

Technical repository access is useful but is not universally required if a trusted publication process exists.

## Reverification

Capabilities should be retested when:

* a connector is reinstalled;
* credentials change;
* repository ownership changes;
* organization policy changes;
* a subscription or product tier changes;
* the interface or product changes materially;
* an operation that previously worked begins failing;
* a previously blocked capability is announced or appears available.

Past capability evidence should guide the test, not replace it.

## Operating principle

> Capability boundaries are part of the architecture. Record them, respect them, and route work through verified paths.
