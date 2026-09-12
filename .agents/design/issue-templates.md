# Issue templates: locked v1

Date: 2026-09-12

Status: agreed by the user with "Lock it" on 2026-09-12.

The agreed content template set for the wiki-driven workflow is **Bug, Change, Investigation**, with the shared authoring rules and bodies below. GitHub installation and tracker configuration remain pending.

## Shared authoring rules

- Capture needs a clear title and enough context to recover the thought. A sentence can be enough. Include known evidence and where the discovery came from; distinguish observations from assumptions.
- Optional prompts help develop the issue. Remove empty sections instead of filling them with guesses or boilerplate. Missing reproduction steps, success criteria, ownership, or a solution must not prevent capture.
- Update the same issue as grilling clarifies the work. Keep the current understanding in the description and material reasoning in the discussion. There is one continuous clarification process, which can also refine the proposed PR.
- Once work is taken on, clarify the intended resolution and any constraints needed for that work. This document does not prescribe a new approval gate or readiness status.
- Link relevant wiki contracts and PRs. Avoid copying a full specification into multiple places. Use tracker properties and relationships for ownership, scheduling, and dependencies where available.
- An issue is optional when a direct PR is sufficient. Capturing an issue does not authorize implementation or commit the team to doing it.

## 1. Bug

Use when observed or suspected behavior violates the expected behavior. An unknown root cause or incomplete reproduction does not turn a bug into a separate Investigation.

Suggested title: `Saved filter resets after reloading`

```markdown
## Problem
<!-- What happened, and what did you expect? Include the basis for that expectation if known. -->

## Context
<!-- Where did you notice it? Add known steps, environment, evidence, impact, or links. Mark anything unverified. -->

## Done when
<!-- When clarified: what observable behavior or evidence would show the problem is resolved? -->
```

Quick capture example:

```markdown
Saved filters appeared to reset after reloading while I was checking the dashboard. Not reproduced yet. Investigate the saved-filter flow before assuming the cause.
```

## 2. Change

Use for desired capabilities, improvements, maintenance, refactoring, documentation, and deferred ideas. A substantial Change can develop into a lightweight PRD in the same issue. Technical work can state an engineering outcome without inventing an end-user story.

Suggested title: `Keep dashboard filters between visits`

```markdown
## Outcome
<!-- What should change, or what problem should be addressed, and why does it matter? -->

## Context
<!-- Relevant observations, wiki contracts, constraints, scope boundaries, and open questions. Include only what is known. -->

## Done when
<!-- When clarified: what observable result would satisfy this issue? -->
```

Quick capture example:

```markdown
Consider remembering dashboard filters between visits so people do not have to rebuild their view. Came up while reviewing the dashboard. Storage scope and privacy implications are still open.
```

## 3. Investigation

Use when the immediate deliverable is an evidence-backed answer or decision. Ordinary research needed to complete a Bug or Change stays with that issue unless separately tracking it has a coordination benefit.

Suggested title: `Decide whether saved filters should follow the user across devices`

```markdown
## Question
<!-- What do we need to learn or decide, and why does the answer matter? -->

## Context
<!-- Starting evidence, options, constraints, and related work. Add an effort or scope bound when useful. -->

## Done when
<!-- When clarified: what answer, evidence, or recorded decision would resolve this inquiry? -->
```

Quick capture example:

```markdown
Should saved filters be device-local or shared across a user's devices? We need this decision to choose persistence behavior. Check user expectations and shared-device risks before selecting an approach.
```

Findings can resolve the issue without code. Record the answer and supporting evidence. Link follow-up work only when there is a distinct unresolved outcome worth tracking.

## Boundaries

| Concept | How it fits |
| --- | --- |
| Quick capture | A short use of a template. Allow a blank title/body route when classification is unclear. |
| Idea | Usually an early Change or Investigation; detail can grow without a new issue. |
| Backlog or deferred | Scheduling or disposition, independent of the template. |
| PRD | The depth a Change issue can reach, not a fourth template. |
| Feature, chore, refactor, docs | Uses of Change. Add separate templates only if practical intake needs justify them. |
| Parent issue | Shared intent for independently coordinated work. Children need meaningful outcomes, not one issue per wiki link. |

## GitHub delivery choice

Prefer short Markdown templates for this agent-led workflow. Keep blank issues available. These headings guide content; they are not mandatory fields for every capture.

If installed in a target repository, place the templates in `.github/ISSUE_TEMPLATE/` with the required GitHub frontmatter. Use a chooser name such as `Bug report`, because GitHub currently requires template names longer than three characters. Do not assume custom native issue types or labels already exist. The category names above are content choices, not organization-level configuration.

Agents using a direct issue API must follow the same authoring rules. Browser form validation is not a general enforcement mechanism for all creation paths. See the [primary-source research](../research/issue-templates.md) for documented platform behavior and the limits of this inference.

The inherited `triage` skill currently assumes bug/enhancement categories and the inherited `to-tickets` skill targets implementation-ready slices. Those skills will need reconciliation with this design when workflow implementation is authorized. Recording this decision does not change their behavior.
