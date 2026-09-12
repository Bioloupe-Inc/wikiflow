---
status: accepted
---

# Write concise, linked wiki pages

Write the wiki as concise, coherent pieces of information in Markdown, with topics such as `sandbox-file-sync`. Keep the related explanation, behavior, constraints, and decisions together so a reader can understand the subject without reconstructing it from isolated claims. A page is not restricted to one claim or required to mirror a single code module; no numeric length limit has been agreed.

Use Mermaid diagrams where they improve the explanation, with relevant nodes linking to wiki pages that provide more detail through the reader's supported internal-link mechanism. Prose and diagrams navigate the same information rather than maintaining separate specifications. [Viewer support findings](../research/wiki-workflow.md#diagram-navigation) distinguish documented navigation from unverified indexing or cross-viewer behavior.

Provide a simple browser viewer reached from the PR. Use a graph as the primary way into an Obsidian-like experience of connected pages, with the UX focused on understanding proposed changes deeply. The viewer is read-only; people discuss the proposal verbally in a call for now. Review comments, approvals, and workflow controls do not belong in this tool.

The experience should feel light and pleasant to navigate. Use subtle motion to support orientation, selection, and movement between explanations. The exact layout, renderer, hosting, access, folder layout, link syntax, and page metadata remain undecided; [review precedents](../research/wiki-workflow.md#reviewing-wiki-changes) and [existing-tool research](../research/wiki-review-tools.md) inform the design without selecting its implementation.
