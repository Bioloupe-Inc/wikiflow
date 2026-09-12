---
status: accepted
---

# Separate work, system contracts, and proposed changes

An Issue owns the assignment, the wiki owns lasting system rules, and the PR description explains a particular proposal and its acceptance evidence. This keeps a stable reference for what needs resolving while allowing the proposed solution to develop, without maintaining competing specifications. Summaries may repeat useful context; link to the authoritative detail.

Keep the wiki on `main` as the accepted contract for the merged version, including intended behavior that a bug may violate. Develop proposed wiki changes and implementation in the same PR, normally merging them together; fixing a bug against a correct existing contract may require no wiki edit. This keeps the system contract aligned with the version it governs, rather than storing future work as unimplemented claims on `main` or requiring a separate wiki-only merge.

Capture unresolved work with the [Bug, Change, and Investigation templates](../issue-templates.md), using short entries or a blank issue when appropriate. These distinguish the evidence and outcomes needed without multiplying overlapping categories such as Feature, Chore, Idea, PRD, and Epic. A mandatory pitch or a separate Issue for every PR would make capture and small changes unnecessarily expensive.

An Issue can outlive an abandoned PR or resolve through a decision without code. Capture does not commit the team to implementation, and Issue closure is not evidence of shipment. Wiki references establish traceability; verification must establish whether behavior satisfies the contract.

Split larger work when its parts have independently meaningful outcomes or need separate ownership and coordination. Changes across the database, API, and UI can stay in one Issue when they serve one outcome. Use a checklist for ordinary implementation steps; an agent needing another session is not itself a reason to create another Issue.

The [dated research](../research/wiki-workflow.md) records supporting platform capabilities and precedents, with their limits. It does not establish that this workflow is optimal or that wiki links should generate Issues or blocking dependencies.
