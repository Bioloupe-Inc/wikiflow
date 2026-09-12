# Existing wiki review tools

Primary documentation checked on 2026-09-12. Scope: Read the Docs, GitBook, Mintlify, Fern, and two smaller review clients. No accounts connected, software installed, previews deployed, or authenticated review flows tested.

## Recommendation

Read the Docs is a strong option for a conventional documentation preview with rendered differences. The chosen design direction places a graph at the center of a read-only viewer, with discussion happening verbally in a call. That calls for exploring the navigation experience before choosing a platform, while reusing maintained graph, Markdown, and diagram components. Mintlify and GitBook offer document review inside larger products; their review workflows are outside the viewer's scope. These are documentation-based judgments, not a product trial or an accepted implementation choice.

## Read the Docs

Read the Docs builds PR revisions and can post a preview link and changed-page list through its GitHub App. Visual Diff adds a changed-page menu and highlights changed sections in rendered HTML, with controls to move between changes or return to ordinary reading. [PR previews](https://docs.readthedocs.com/platform/stable/pull-requests.html), [Visual Diff](https://docs.readthedocs.com/platform/stable/visual-diff.html).

Internal links can show hover previews, preserving reading context. The renderer supplies Markdown layout, navigation, and diagrams; Read the Docs documents integration with Material for MkDocs, whose Mermaid support is configured through its existing extension mechanism. This establishes the pieces, not proof that diagram comparison and node navigation work together during a review. [Link previews](https://docs.readthedocs.com/platform/stable/link-previews.html), [MkDocs integration](https://docs.readthedocs.com/platform/stable/intro/mkdocs.html), [Mermaid support](https://squidfunk.github.io/mkdocs-material/reference/diagrams/).

Private previews are supported by Read the Docs Business. Its Basic plan starts at $50/month; Community hosting is free for open-source projects. Visual Diff currently pins its baseline on the first successful PR build and does not automatically refresh that snapshot after an update against a newer base. HTML and table comparison can also produce misleading highlights. [Preview access](https://docs.readthedocs.com/platform/stable/pull-requests.html#security), [Pricing](https://about.readthedocs.com/pricing/), [Comparison limitations](https://docs.readthedocs.com/platform/stable/visual-diff.html#limitations-and-known-issues).

## Mintlify

Mintlify accepts `.md` and `.mdx` pages, supports connecting an existing repository and subdirectory, and renders Mermaid fences. Its normal page layout includes navigation and a table of contents. [Pages](https://www.mintlify.com/docs/organize/pages), [GitHub integration](https://www.mintlify.com/docs/deploy/github), [Mermaid](https://www.mintlify.com/docs/components/mermaid-diagrams).

PRs targeting the deployment branch receive a preview link that updates with pushes. A preview widget lists added, modified, and removed files, opens the relevant page, and offers a route into the editor. Previews require Pro or Enterprise; restricting preview access requires Enterprise. Fork PRs do not receive previews. [Preview deployments](https://www.mintlify.com/docs/deploy/preview-deployments).

The editor has a visual content diff and a source diff against the published version, plus native GitHub PR approval and merge controls. Comparison lives in the editor, rather than being documented as an overlay on the public preview. Deleted files and images cannot open in its diff view. Editor links require access to the Mintlify organization. [Review changes](https://www.mintlify.com/docs/editor/review).

Editor comments remain in Mintlify; unresolved threads are summarized and linked in the PR description. They are not native GitHub review comments. Keeping discussion entirely in GitHub would therefore remain a team convention. [Editor collaboration](https://www.mintlify.com/docs/editor/collaborate).

## GitBook

Git Sync connects repository Markdown bidirectionally with GitBook content. Its collaboration guide describes corresponding branches when work starts through GitBook or a GitHub PR. A GitHub PR status provides a preview URL. This is a synchronized documentation product, not a passive renderer over Git. [Git Sync](https://gitbook.com/docs/docs-as-code/git-sync), [Collaboration guide](https://gitbook.com/docs/guides/docs-best-practices/make-your-documentation-process-more-collaborative-with-change-requests), [PR previews](https://gitbook.com/docs/docs-as-code/git-sync/github-pull-request-preview).

GitBook change requests provide previous and updated content side by side, changed-block navigation, and a choice between all pages or only changed pages. This explicitly preserves unchanged context during review. Standard Mermaid fences render as native blocks. [Change-request diff view](https://gitbook.com/docs/collaborate/change-requests/change-requests-in-a-space#diff-mode), [Mermaid blocks](https://gitbook.com/docs/create-content/blocks/mermaid-blocks).

PR previews require a published site and a GitBook account, and are unavailable for sites behind authenticated access. Change requests also carry GitBook reviews, comments, and merge rules. The sources do not establish that these reviews and comments become native GitHub reviews and comments. That extra collaboration authority and the private-preview restriction weaken the fit for an internal wiki reviewed through GitHub. [PR previews](https://gitbook.com/docs/docs-as-code/git-sync/github-pull-request-preview), [Change requests](https://gitbook.com/docs/collaborate/change-requests/change-requests-in-a-space).

## Fern

Fern builds hosted documentation from repository Markdown and configuration. Both direct repository editing and its visual editor use GitHub PRs. Mermaid fences render diagrams. [How Fern works](https://buildwithfern.com/learn/docs/getting-started/how-it-works), [Mermaid support](https://buildwithfern.com/learn/docs/writing-content/markdown-media#diagrams).

Its CLI and documented GitHub Actions workflow publish PR previews and link changed pages in a PR comment. The beta `fern docs diff` command compares preview and production screenshots and creates side-by-side images. It does not establish an interactive word or block diff with navigable context inside the comparison. A full preview remains available separately. [Preview changes](https://buildwithfern.com/learn/docs/preview-publish/preview-changes), [Docs diff command](https://buildwithfern.com/learn/cli-api-reference/cli-reference/docs-commands#fern-docs-diff).

## Remaining proof

None of the reviewed pages establishes clickable Mermaid nodes that reliably remain inside the selected PR revision or a graph of affected relationships. Mermaid rendering alone does not prove navigation or visual diagram comparison. Mintlify and Fern compare against the published site; Read the Docs uses a pinned build snapshot. None should be assumed equivalent to the exact current PR merge-base. A focused trial should verify the relevant comparison and navigation behavior before adoption.

## Smaller review clients

- [GitHub MD Review](https://chromewebstore.google.com/detail/github-md-review/hcoodlcadbhcgikicjkijhdnglcjjebj) adds a Review rendered button to Markdown files in GitHub PRs. Its developer documents Mermaid rendering and comments posted as native GitHub review comments. The listing does not establish a rendered change comparison or navigation across a wiki. Each reviewer needs the Chrome extension; its small, unrated listing is not adoption evidence.
- [PullMark](https://github.com/jedijashwa/pullmark) documents rendered word and block diffs, Mermaid, native GitHub reviews, and navigation to related Markdown at the PR commit. It is a macOS app, so it does not satisfy the shared browser entry point. It could be useful for individual reviewers without adding a hosted wiki platform.
