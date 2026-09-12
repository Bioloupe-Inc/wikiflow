# Issue templates

Agreed content design, 2026-09-12. These templates have not been installed in a tracker. Their role is defined in [ADR-0004](adr/0004-separate-issues-system-contracts-and-proposals.md); pickup readiness is defined in [ADR-0005](adr/0005-clarify-the-assignment-before-developing-the-solution.md).

Give an Issue a clear title and enough context to recover the thought. A sentence can be enough for quick capture. Use the prompts when useful, remove empty sections, and distinguish observations from assumptions. A blank issue is available when classification is unclear. Human and agent authors follow the same content guidance.

For a discovery during other work, find an existing Issue or capture a short new one, then continue the current work. Capture does not require immediate grilling or branch creation.

## Bug

Use for observed or suspected incorrect behavior. An unknown root cause or missing reproduction does not make it an Investigation.

```markdown
## Problem
<!-- What happened, and what did you expect? Include the basis for that expectation if known. -->

## Context
<!-- Where did you notice it? Add known steps, environment, evidence, impact, or links. Mark anything unverified. -->

## Done when
<!-- When clarified: what observable behavior or evidence would show the problem is resolved? -->
```

Quick capture: "Saved filters appeared to reset after reloading while I was checking the dashboard. Not reproduced yet. Investigate the saved-filter flow before assuming the cause."

## Change

Use for desired capabilities, improvements, maintenance, refactoring, or documentation. An engineering outcome is sufficient; it need not be recast as an end-user story.

```markdown
## Outcome
<!-- What should change, or what problem should be addressed, and why does it matter? -->

## Context
<!-- Relevant wiki contracts, constraints, scope boundaries, and open questions. Include only what is known. -->

## Done when
<!-- When clarified: what observable result would satisfy this issue? -->
```

Quick capture: "Consider remembering dashboard filters between visits so people do not have to rebuild their view. Came up while reviewing the dashboard. Storage scope and privacy implications are still open."

## Investigation

Use when the immediate deliverable is an evidence-backed answer or decision. Research needed within a Bug or Change stays there unless separate coordination is useful. Record the findings and supporting evidence; create follow-up work only for a distinct unresolved outcome.

```markdown
## Question
<!-- What do we need to learn or decide, and why does the answer matter? -->

## Context
<!-- Starting evidence, options, constraints, and related work. Add an effort or scope bound when useful. -->

## Done when
<!-- When clarified: what answer, evidence, or recorded decision would resolve this inquiry? -->
```

Quick capture: "Should saved filters be device-local or shared across a user's devices? We need this decision to choose persistence behavior. Check user expectations and shared-device risks before selecting an approach."

## Installation considerations

Use short Markdown templates with blank issues enabled. When installation is authorized, supply the platform's required metadata and validate its current requirements. Template categories do not presume custom native issue types or labels, and browser validation does not enforce every agent creation path; see the [platform research](research/wiki-workflow.md).

The inherited triage and ticket-generation skills still follow their existing contracts. Reconcile them when implementing this workflow.
