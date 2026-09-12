---
status: accepted
---

# Clarify the assignment before developing the solution

Issues start unassigned, and the team reviews them together in meetings to establish the need, intended outcome, scope, and resolution conditions before pickup. For behavior-changing work, the developer then develops detailed system behavior in a draft wiki PR and adds implementation to that same PR. Requiring the complete wiki proposal before pickup would put substantial design work before assignment, so readiness concerns the assignment rather than a finished system design.

Preserve the agreed Issue as the assignment develops into a solution, recording material scope changes explicitly. Developers and agents can investigate facts and choose routine technical details within agreed intent. Consequential product choices need agreement before implementation that depends on them.

Daily standups provide open communication about progress, questions, and proposed decisions; ad hoc meetings allow further discussion. Use that cadence as needed rather than requiring everyone to author the detailed specification together or creating separate mandatory clarification stages for each artifact.

Allow concurrent work in the same area. While preparing changes, agents check relevant open Issues and draft PRs, surface conflicting proposals through the existing communication channels, and record real blocking dependencies. Ordinary file overlap can be handled during integration; a disagreement about system behavior needs resolution before implementing the affected part.

A completed PR needs another developer's approval and passing required checks before merge. Review focuses on delivered behavior and verification evidence against the agreed wiki, supported by agent code review and automated checks. Standup is the usual review venue, not an exclusive approval window; who performs the merge is an ordinary execution detail.
