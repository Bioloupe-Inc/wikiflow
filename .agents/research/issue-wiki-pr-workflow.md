# Issue, wiki, and PR workflow research

Date: 2026-09-12

Question: Is the proposed workflow coherent: evolving GitHub issues as lightweight product definitions, a versioned normative wiki, PRs changing the wiki and implementation together, and one continuing clarification loop?

Status: Research and recommendations only. This note does not change the agreed handoff or authorize implementation.

## Findings from Linear and Shape Up

### 1. Product definition can live with tracked work, but its scale matters

Linear describes projects as outcome-oriented work comprising issues and optional documents. Its own practice places responsibility for the specification with the project lead; teammates collaborate on the brief and write their own issues. This supports keeping definition and execution connected, while qualifying any universal equation of one issue with one product requirements document. A feature spanning several independently owned efforts may need a shared definition above its execution issues.

Source: [Linear: Projects](https://linear.app/docs/projects).

### 2. An issue need not be restricted to a short task description

Linear supports documents attached to issues as well as projects, explicitly suggesting them for complex implementation needs. This establishes that substantial context can remain attached to tracked work. It does not prescribe a separate document for every issue or prove that keeping an entire specification in an issue description is superior.

Source: [Linear: Documents](https://linear.app/docs/documents).

### 3. A pitch is a specific commitment proposal, not a synonym for an issue

Shape Up pitches combine a motivating problem, effort budget, solution outline, risks, and exclusions so decision makers can choose work. The outline is intentionally less detailed than a finished design. This supports dropping mandatory pitch terminology while retaining useful questions about value and boundaries. It also challenges an absolute rule that issues may contain no solution discussion: evaluating a meaningful commitment can require an outline of the proposed approach.

Source: [Shape Up: Write the Pitch](https://basecamp.com/shapeup/1.5-chapter-06).

### 4. Whole-outcome ownership and discovered tasks are established practices

Shape Up gives teams a shaped project and lets them discover their tasks through implementation. Its rationale is that assigning isolated tasks prematurely fragments understanding and responsibility. This supports continuing clarification during real work instead of treating an initial checklist as exhaustive. Shape Up also expects deployment within the cycle, so its completion rule cannot be cited as support for automatically equating a merged PR with a delivered outcome.

Source: [Shape Up: Hand Over Responsibility](https://basecamp.com/shapeup/3.1-chapter-10).

### 5. Useful divisions emerge from real dependencies

Shape Up groups work into integrated parts that can finish independently, including both interface and backend work when necessary. Those divisions are discovered and revised as implementation exposes dependencies. This supports dividing a large effort when meaningful boundaries become clear, instead of mechanically generating an issue for every wiki paragraph or assigning permanent frontend/backend buckets.

Source: [Shape Up: Map the Scopes](https://basecamp.com/shapeup/3.3-chapter-12).

## Complementary specification and agent workflow research

### 6. Persistent specifications and proposed changes have a close precedent

OpenSpec separates current specifications from change proposals and specification deltas. Completing a change can incorporate its deltas into the persistent specification while retaining the proposal's history. It distinguishes behavior contracts from implementation plans and scales specification detail with risk. This is a close conceptual precedent for our wiki and proposed wiki changes. Our use of Git branches and PRs instead of OpenSpec's change folders is an adaptation, not its prescribed mechanism.

Source: [OpenSpec: Concepts](https://github.com/Fission-AI/OpenSpec/blob/main/docs/concepts.md).

### 7. Clarification and implementation can form one continuing loop

OpenSpec explicitly allows proposals, designs, specifications, and tasks to change during implementation. It describes reviewing as an activity available throughout the work. It also distinguishes correcting stale specifications from fixing code that violates a correct specification. This supports one continuing clarification loop with revisable artifacts, rather than separate mandatory Issue and PR interviews. It does not establish our team's approval policy.

Source: [OpenSpec: Editing and Iterating on a Change](https://github.com/Fission-AI/OpenSpec/blob/main/docs/editing-changes.md).

### 8. An agent team reports using repository knowledge and executable feedback

OpenAI's account of an internal Codex-driven project describes a short repository entry point linking to versioned knowledge, including product specifications and execution plans. It combines that knowledge with app inspection, tests, review, and mechanical architectural checks. The authors explicitly limit generalization without comparable tooling investment and leave long-term architectural coherence unresolved. This is firsthand experience, not a controlled productivity evaluation. It supports making the wiki accessible and verifiable; it does not validate our particular note graph or every proposed gate.

Source: [OpenAI: Harness engineering](https://openai.com/index/harness-engineering/), published 2026-02-11.

### 9. Empirical research is emerging, but does not establish an optimal workflow

SpecMine is a corpus paper collecting specifications and spec-touching PRs from public repositories, enabling study of relationships between specifications and implementation. Its abstract does not present a controlled comparison establishing that our workflow, issue-based PRDs, or any specific documentation topology improves outcomes. Use it as evidence of research activity and available observational data, not proof of effectiveness.

Source: [SpecMine, arXiv:2608.25202v3](https://arxiv.org/abs/2608.25202v3), revised 2026-09-01.

## Recommendations and inferences

These are proposed adaptations, not rules prescribed or experimentally validated by the sources above.

- Keep the issue as the durable record of the work's purpose, boundaries, unresolved questions, and success conditions. A product issue can grow into a lightweight PRD; a bug need not carry that ceremony.
- Treat the issue/PR distinction as responsibility, not a prohibition on content: the issue explains and coordinates the effort; the PR presents a concrete proposed change. Both may discuss behavior and approach without becoming duplicate detailed specifications.
- For a bounded effort, start with one issue. Add child work only when distinct ownership, real dependencies, or independently finishable parts justify it. A larger parent issue can hold the shared intent and link to its pieces; Linear's separate project object is precedent for scale separation, not a requirement to introduce another tool.
- Keep clarification continuous. Implementation can expose a missing requirement or a better division of work. Preserve decisions already made while reopening only what new evidence affects.
- Distinguish merge completion from delivery completion explicitly. Select the meaning appropriate to the issue instead of treating either convention as universally correct.
- Keep durable system rules and decision rationale in the versioned wiki, and link them from Issues. Avoid maintaining the same detailed contract independently in both places.
- Grill until the goal, important constraints, and consequential choices are clear enough for the next useful step. Do not demand an exhaustive task map before any implementation can reveal new information.
- Test the proposed workflow before adding strict graph-shape gates or deriving task dependencies from wiki links. The sources establish no guarantee that short notes, citations, or graph shape imply correct implementation or conflict-free parallel work.
- A small pilot should include a new behavior, a bug against an existing rule, and two related changes under different owners. Observe repeated questions, stale or duplicated decisions, review effort, and missed conflicts. These are suggested evaluation cases, not work already authorized or performed.

## Strength and limits of the evidence

These are official product capabilities, first-party workflow descriptions, practitioner recommendations, and a corpus paper. They provide credible precedent and reveal conceptual failure modes. They do not provide a controlled comparison showing that this exact issue/wiki/PR workflow improves team or agent performance. The proposed combination still needs a small real-work trial before stronger claims are justified.
