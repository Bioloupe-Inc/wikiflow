# Wiki workflow: open questions

Updated 2026-09-12. Resume with [CONTEXT.md](../../CONTEXT.md) and the [decision records](../../docs/adr/). [Template bodies](../../docs/issue-templates.md) and [dated source research](../../docs/research/wiki-workflow.md) retain the supporting material.

Continue the design conversation before implementing skills or a linter. Documentation cleanup and a throwaway UI prototype are authorized; the harness and tracker-template installation remain unimplemented.

## Next decisions

- Clarify useful parent/child relationships, ownership transfer, and Issue-to-PR cardinality where they affect coordination. Detailed tracker states and enforcement are still open.
- Define completion and evidence for different outcomes, including Issue closure versus merge, deployment, and verified delivery. Merge button operation does not need a separate policy.
- Decide what warrants enforcement or maintenance: resolving links, duplicate content, citations, confirmation, and drift. Claim-graph fan-out limits, per-commit shape gates, hooks, metrics, and scheduled sweeps are not current requirements. A citation alone cannot prove a claim.
- Replace the existing setup skill with full repository setup: build the entire initial wiki, install the Issue templates, and set up CI/CD, as recorded in [ADR-0003](../../docs/adr/0003-develop-an-independent-wiki-workflow.md). Next define source reconciliation, unanswered questions, completeness, pipeline responsibilities, and treatment of existing glossaries and ADRs. Retiring those documents is unapproved. Ongoing maintenance remains to be designed.
- Consider `wikispec/` at the adopting repository's root as the home for the wiki. The user proposed this tentatively; the directory name and internal organization are not yet settled.
- Choose skill boundaries, invocation policy, setup, tracker integration, and agent runtime support. Names such as `grill-with-wiki`, a graph-maintenance component, and `setup-wiki` are provisional.

The existing [setup skill](../../skills/engineering/setup-wikiflow/SKILL.md) scaffolds tracker instructions, domain pointers, optional triage mappings, and a root instruction block. It does not build a wiki, install Issue templates, or configure CI/CD. Its tracker and triage seeds need reconciliation with ADR-0004 and ADR-0005: they put specifications in Issues, equate readiness with full specification, and allow immediate self-claiming of unassigned work.

[Astra skill and prompt guidance](../../docs/research/wiki-workflow.md#skill-and-prompt-design) informs the replacement's instruction design.

[OpenWiki findings](../../docs/research/openwiki.md) list the mechanics worth borrowing for building and maintaining the wiki: code-derived indexes and link checks, evidence hashes as a change lens, the materiality test, a user-authored brief, and a static graph export. The clone lives beside this repository at `../openwiki`. [Spec Kit and OpenSpec findings](../../docs/research/spec-driven-tools.md) add the review order, delta vocabulary, right-sizing rule, and the question of growing the wiki from changes rather than building it all at setup; those clones live at `../spec-kit` and `../openspec`.

## Candidate decisions from the reference study

Proposed on 2026-09-12 after reading OpenWiki, Spec Kit, and OpenSpec together with the ADRs. None is accepted; each needs its own discussion and, if agreed, an ADR.

- The wiki outranks the code. Because the contract describes intended behavior even when the implementation is wrong, drift is a symmetric signal a person adjudicates. No automated pass may rewrite pages from source.
- Ground contract sections in tests, not code. A cited test that changes means the proof changed; code changing under green tests is not a contract change. Test citations also give a page a coverage measure with no model involved.
- The page is the only authored unit. Indexes, backlinks, and hierarchy are derived from links; folders are avoided or derived; one routing page is written last. Moving a page must break nothing.
- Headings are the addressable unit. Issues, tests, and pages reference a section by wikilink and anchor; git diffs at that granularity; the link checker catches renames. No ids or sidecars.
- An Issue links the pages it expects to affect. That set is the agent's reading list (those pages plus one hop) and the reviewer's expected-change set: pages changed but not linked are a scope-change signal to record.
- The viewer produces the call's agenda from derived facts only: the assignment, pages added, changed, or removed with neighborhoods, unedited pages whose cited tests changed, and links broken or introduced. It shows no model summaries.
- Setup builds a complete wiki with every page marked draft; a page becomes stable the first time a PR touches it under review. This keeps the full initial wiki while staying honest about what has been verified.
- Removing a page is a contract removal: the same PR must fix every inbound link, and CI enforces it.
- A PR that changes tests but no wiki page gets a non-blocking prompt asking whether the contract changed.
- Anything shown to reviewers by tooling must be a derived fact, never model output, so that the tool stays trustworthy.

## Deferred: wiki viewer

Parked at the user's request on 2026-09-12. The prototype is partly in the right direction but needs better UI and UX; no variant is selected. Keep the intent in [ADR-0006](../../docs/adr/0006-write-concise-linked-wiki-pages.md), and resume viewer work only when the user returns to it.

The [prototype, feedback, and six directions to explore later](../../docs/prototypes/README.md) are preserved in this repository. The original UI snapshot is `0d44062`. The user requested publishing all work on `main`; the brainstorms remain proposals, not accepted requirements.

## Repository identity

WikiFlow is the independent `JoziGila/wikiflow` repository. GitHub fork detachment, repository rename, package/plugin identity, installation wording, and the `ask-wikiflow` / `setup-wikiflow` skill renames are complete. Matt Pocock's original license, attribution, and history are preserved. These identity changes do not implement the replacement setup workflow.
