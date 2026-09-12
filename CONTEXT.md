# Agent Skills

Vocabulary for conversational project work with coding agents, including the inherited skill flows and the wiki workflow being designed here.

## Language

**Issue tracker**:
The place where Issues retain their identity, discussion, and coordination information.
_Avoid_: backlog manager, backlog backend, issue host

**Issue**:
Something unresolved with a persistent identity: a problem, desired change, question, or decision. Its assignment consists of the need, intended outcome, scope, and resolution conditions.
_Avoid_: ticket (except when quoting an external system or referring to a Decision ticket), spec, pitch

**Bug**:
An Issue about observed or suspected behavior that violates the expected system contract.

**Change**:
An Issue requesting a desired improvement, including a capability, maintenance, refactoring, or documentation.

**Investigation**:
An Issue whose immediate deliverable is an evidence-backed answer or decision.

**Quick capture**:
A short record sufficient to recover a need or discovery, with whatever context is already known.

**Backlog**:
Captured Issues awaiting a decision or attention. Inclusion does not imply a commitment to deliver them.

**Ready**:
The condition in which an Issue's assignment is clear enough for pickup, although its detailed system proposal may still need development. Readiness is distinct from priority, assignment, or an instruction to start.
_Avoid_: fully specified, approved for merge

**Pickup**:
A developer taking responsibility for pursuing a clear Issue.
_Avoid_: capture

**Work overlap**:
Concurrent Issues affecting the same system behavior or implementation area. Overlap does not by itself establish a blocking dependency.

**Blocking dependency**:
A relationship where an Issue needs another Issue's outcome before it can progress.
_Avoid_: shared file, wiki reference

**Wiki**:
The maintained system contract: precise behavior, constraints, domain concepts, and durable decisions. It describes intended behavior even when an implementation has bugs.
_Avoid_: backlog, activity log, as-built inventory

**Wiki page**:
A concise, coherent piece of system information, such as an explanation of sandbox file synchronization. Related behavior, rules, constraints, and design decisions can belong in the same page.
_Avoid_: one claim per note

**Setup**:
Preparing a repository for the wiki workflow, including its full initial wiki, Issue templates, and CI/CD.

**Wikilink**:
A reference to another wiki page, usable in prose or as a diagram node's navigation target.

**Wiki viewer**:
A read-only browser experience reached from a PR, with a graph for exploring connected wiki pages and understanding proposed changes. People discuss the proposal verbally in a call; the viewer does not own review comments or approvals.

**Pull request (PR)**:
A concrete proposed resolution expressed through changes to the system contract and implementation as applicable.
_Avoid_: Issue, specification

**PR description**:
The explanation accompanying a particular proposed change, including its approach and acceptance evidence.
_Avoid_: system contract

### Inherited skill flows

**Decision ticket**:
A decision-seeking child Issue in the inherited wayfinding flow.

**Triage role**:
A classification indicating the attention an Issue needs in the inherited triage flow.
