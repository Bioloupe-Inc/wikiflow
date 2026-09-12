# Wiki workflow research

Research collected on 2026-09-12, consolidated from the issue-template and issue/wiki/PR investigations. These findings preserve the earlier source review; this cleanup did not recheck live platform behavior. Accepted decisions live in [ADR-0004](../adr/0004-separate-issues-system-contracts-and-proposals.md) and [ADR-0005](../adr/0005-clarify-the-assignment-before-developing-the-solution.md).

## Issue intake

| Source | Finding and limit |
| --- | --- |
| [GitHub: issue types](https://docs.github.com/en/issues/tracking-your-work-with-issues/using-issues/managing-issue-types-in-an-organization) | Organizations can configure native classifications independently of templates and workflow states. Portable templates must not assume custom types exist. |
| [GitHub: issue templates](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/configuring-issue-templates-for-your-repository) | Markdown templates and YAML forms guide browser intake. Forms support required fields, templates are exposed from the default branch, and the chooser can allow blank issues; users with write access retain a blank route. This governs capture, not readiness. |
| [GitHub REST: create an issue](https://docs.github.com/en/rest/issues/issues#create-an-issue) | The documented creation contract accepts a title and optional body and metadata, without a template-answer contract. Inference: browser-form requirements are not a general authoring gate for agents. |
| [GitHub CLI: `gh issue create`](https://cli.github.com/manual/gh_issue_create) | The CLI accepts direct body text or a body file and describes templates as starting body text. Its manual does not establish enforcement of all YAML form validation on direct creation paths. |
| [Linear: Triage](https://linear.app/docs/triage) | Intake can be reviewed, enriched, prioritized, declined, deferred, or resolved as duplicate before entering the team's workflow. This supports capture before commitment, without prescribing this project's states. |

## Work, specification, and verification

| Source | Finding and limit |
| --- | --- |
| [Linear: Projects](https://linear.app/docs/projects) | Projects organize outcome-oriented work across issues and documents. This supports shared intent above independently coordinated work, not equating every Issue with a full PRD. |
| [Linear: Documents](https://linear.app/docs/documents) | Documents can attach to issues and projects, allowing substantial context near tracked work. This does not require a separate document for each Issue. |
| [Shape Up: Write the Pitch](https://basecamp.com/shapeup/1.5-chapter-06) | A pitch makes the case for investing in bounded work using the problem, an outline, risks, and exclusions. It is a commitment proposal, not a universal definition of an Issue. |
| [Shape Up: Hand Over Responsibility](https://basecamp.com/shapeup/3.1-chapter-10) | Teams receive shaped work and discover implementation tasks. Its deployment expectation means it cannot justify treating a merged PR as delivered value. |
| [Shape Up: Map the Scopes](https://basecamp.com/shapeup/3.3-chapter-12) | Work can be split into integrated, independently finishable parts as dependencies become clear. This supports meaningful outcomes over one Issue per layer or wiki paragraph. |
| [OpenSpec: Concepts](https://github.com/Fission-AI/OpenSpec/blob/main/docs/concepts.md) | Persistent specifications and proposed deltas have separate roles. Using branches and PRs for those deltas is our adaptation, not OpenSpec's prescribed storage mechanism. |
| [OpenSpec: Editing and Iterating](https://github.com/Fission-AI/OpenSpec/blob/main/docs/editing-changes.md) | Clarification and review can continue during implementation; a stale specification and code violating a correct specification need different responses. This does not establish our approval policy or justify silently changing agreed scope. |
| [OpenAI: Harness engineering](https://openai.com/index/harness-engineering/) | A firsthand agent-driven project combines repository knowledge with executable feedback and review. The account is not controlled evidence for this wiki design, its graph shape, or its proposed gates. |
| [SpecMine, arXiv:2608.25202v3](https://arxiv.org/abs/2608.25202v3) | A corpus enables observation of specifications and related changes in public repositories. Its abstract does not establish an optimal workflow or a causal improvement from this design. |

## Evidence limits

The sources establish platform capabilities, precedents, and research directions. They do not prove that the chosen template set, wiki topology, or review cadence is optimal. No external writes, API mutation tests, harness implementation, or live workflow validation were performed in these investigations.

Earlier discussion also mentioned Birgitta Boeckeler's specification-driven development analysis, Spec Kit, Kiro, Tessl, and arXiv:2609.00252. Those were research leads; no detailed source extracts were retained for them. Revisit the primary material before relying on their claims. LangChain OpenWiki was subsequently reviewed for the navigation precedents below.

## Diagram navigation

Additional primary documentation reviewed on 2026-09-12; no live renderer tests were performed.

- [Obsidian's diagram-link documentation](https://github.com/obsidianmd/obsidian-help/blob/master/en/Editing%20and%20formatting/Advanced%20formatting%20syntax.md#linking-files-in-a-diagram) supports node-to-note navigation using the `internal-link` class and the node's displayed text. These links do not appear in Graph view; the documentation does not establish equivalent rename handling or other indexing behavior.
- [Mermaid flowchart syntax](https://mermaid.js.org/syntax/flowchart.html) uses doubled brackets for a subroutine-shaped node, not a wiki reference. Its hyperlink directives depend on the host's [security configuration](https://mermaid.js.org/config/schema-docs/config#securitylevel); literal wikilink text is not a portable linking mechanism inside a diagram.
- [GitHub's diagram documentation](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/creating-diagrams) establishes Mermaid rendering, not Obsidian-style note navigation or a promise that all clickable nodes work. Choose the reader before relying on a particular link mechanism.

## Reviewing wiki changes

Primary documentation reviewed on 2026-09-12. These are documented capabilities and design precedents, without a running integration or renderer test.

| Source | Finding and limit |
| --- | --- |
| [GitHub: rendering prose differences](https://docs.github.com/en/repositories/working-with-files/using-files/working-with-non-code-files#rendering-differences-in-prose-documents) | Rendered Markdown diffs highlight changed prose and links, with source view as a fallback. This does not establish a connected wiki review experience or visual Mermaid comparison. |
| [GitHub: deploying to an environment](https://docs.github.com/en/actions/how-tos/write-workflows/choose-what-workflows-do/deploy-to-environment) | An Actions job's environment URL produces a native View deployment link in the PR timeline for a PR-triggered workflow. This supplies the entry point, not hosting or the reader. |
| [GitHub: workflow artifacts](https://docs.github.com/en/actions/how-tos/manage-workflow-runs/download-workflow-artifacts) | Artifacts are downloadable outputs with access requirements and retention limits. A downloaded archive alone does not provide the requested browser review view. |
| [OpenWiki: explore your wiki](https://github.com/langchain-ai/openwiki/blob/main/README.md#explore-your-wiki) | An interactive graph accompanies a Markdown reader, with linked pages, Mermaid explanations, source evidence, and static-site export. Navigation is a useful precedent; PR comparison and clickable Mermaid nodes were not established. OpenWiki describes implementation, while this project's wiki records the agreed contract. |
| [OpenSpec: delta specs](https://github.com/Fission-AI/OpenSpec/blob/main/docs/concepts.md#delta-specs) | Distinguishes current behavior from added, modified, or removed requirements in a proposal. Using Git base and head revisions to present this distinction is our adaptation, without adopting a second delta store. |
| [GitHub: PR reviews](https://docs.github.com/en/pull-requests/reference/pull-request-reviews) | GitHub records review comments, approvals, and change requests. A separate reader can link back to this existing review authority. |

The subsequent design direction is a read-only graph viewer for understanding changes together on a call, recorded in [ADR 0006](../adr/0006-write-concise-linked-wiki-pages.md). It has no discussion or approval controls. Opening on changed topics, comparing revisions, and navigating related context are candidate UI choices under exploration in the prototype. Hosting, access, preview lifetime, and the exact comparison presentation remain open.

The subsequent [existing-tool comparison](wiki-review-tools.md) found direct coverage in Read the Docs Visual Diff and overlapping capabilities in other products. Evaluate existing tools before choosing custom implementation.

## Skill and prompt design

Reviewed 2026-09-12: [OpenAI, Rethinking skills and prompts for GPT-6 Astra](https://developers.openai.com/blog/rethinking-skills-and-prompts-for-gpt-6-astra).

The article recommends concise, precise skill descriptions, progressive disclosure, and guidance suited to the task. Rigid recipes, unconditional document reading, excessive testing instructions, and broad approval language can constrain newer models unnecessarily. Explicit completion criteria encourage follow-through. Instructions shared across models need consideration of their different behavior.

Implications for this project, proposed rather than validated:

- Define setup's completed outcomes across the full wiki, Issue templates, and CI/CD, including appropriate verification and real blockers.
- Keep the entry skill concise and load supporting wiki, tracker, or pipeline guidance as needed.
- Keep design interviews distinct from execution so authorized setup can proceed with routine decisions.
- Audit inherited instructions for redundant reading, premature handoffs, and unnecessary approval pauses.
- Verify behavior proportionately using existing tools.

This is design input. No skill implementation or comparative model evaluation was performed.
