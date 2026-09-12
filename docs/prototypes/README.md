# Wiki viewer prototype

Question: which graph-based layout makes it easiest to understand a proposed wiki change together on a call?

This is a throwaway, read-only UI study with illustrative content. It does not connect to a repository, PR, account, or review system. Discussion happens verbally. No layout has been selected for implementation.

Deferred on 2026-09-12. User feedback: the prototype is partly in the right direction, but needs better UI and UX. None of the three variants is approved. Keep this as a reference for a later design exploration; no further implementation is planned now.

Run from this checkout:

```sh
python3 -m http.server 8768 --bind 127.0.0.1 --directory docs/prototypes
```

Open [the prototype](http://127.0.0.1:8768/wiki-viewer-prototype.html?variant=A).

- **A, Explore:** a stable graph alongside a reading pane.
- **B, Compare:** aligned before and proposed graphs, with corresponding pages below.
- **C, Follow:** the selected page surrounded by incoming and outgoing connections.

Use the floating arrows or the keyboard's left and right arrows to change variants. `?variant=A`, `B`, or `C` selects a layout. Page and reading-version selection are also kept in the URL.

Click graph nodes, prose links, connected-page cards, or the Resume node in the proposed transfer diagram. Search pages by name with the search field or Command/Ctrl+K. Drag the graph to pan; use its zoom controls or pinch to zoom. Graph coordinates remain stable across before and proposed views, and graph zoom survives page selection.

Motion follows navigation: nearby connections ease into focus on hover, a newly selected topic gets one quiet settling cue, pages arrive softly, and zoom glides into place. The viewer respects the operating system's reduced-motion preference.

The example Markdown is the source for page content, change classification, and prose-link connections. The prototype uses version-pinned D3, Marked, jsdiff, and Mermaid from jsDelivr, so opening it requires network access. It has no persistence beyond navigation URLs.

Proof limits: the sample text comparison pairs simple document blocks and does not establish a general Markdown diff algorithm. The graph follows links in Markdown prose; automatic indexing of links inside Mermaid is not implemented. Diagram navigation uses known example destinations. Real repository loading, exact Git revision selection, large-wiki layout, hosting, and access remain design work.

Browser checks covered all three layouts, topic and search navigation, before/proposed selection, diagram links, browser Back, zoom and fit, and the absence of browser warnings or errors. This is desktop prototype verification, not a production acceptance suite.

## Directions to explore later

These are brainstorms, not selected features or architecture. Preserve the core intent: a light, read-only browser viewer reached from a PR, connected wiki explanations, useful diagram navigation, and discussion on a call.

| Direction | Experience to explore | Question it should answer |
| --- | --- | --- |
| A small neighborhood that unfolds | Begin with the changed topic and a few useful connections. Expand neighboring topics deliberately, keeping visited places stable and easy to return to. | Can discovery feel natural without presenting a wall of nodes? |
| A landscape with semantic zoom | Start with recognizable areas of the system. Reveal pages as you zoom closer, then explanations at reading distance. | Can one continuous space support both orientation and detail? |
| The page opens inside the map | Expand the selected node into a comfortable reading surface. Keep surrounding connections visible, with brief link previews for nearby context. | Can reading and exploring feel like one interaction? |
| A meaningful system diagram as the entrance | Enter through a workflow or architecture diagram already explained in the wiki. Open its steps, states, or components to read the connected pages. | Does a diagram of how the system works explain more than a graph of page links? |
| One map with a temporary before view | Keep positions stable while switching between accepted and proposed behavior. Try holding a key to peek at the previous version and showing changes only where attention is focused. | Can the difference become clear without making the reader compare two whole canvases? |
| A trail through the proposal | Begin with the proposal's purpose, then follow a visible path through the changed behavior and related constraints. Allow detours and an easy return to the discussion's thread. | Does a guided path help a call while preserving free exploration? |

When revisiting, try these against realistic wiki content and a concrete conversation: find what changed, understand its consequences, inspect an unchanged constraint, follow a diagram link, and return without losing your place. Pay particular attention to typography, hierarchy, density, useful previews, and keyboard navigation. Motion should make those transitions feel continuous; the underlying interactions still need to earn their place.

Keep this source on `codex/wiki-viewer-prototype`. The current verdict is deferred, with no winning layout. Retain only validated design decisions in the main project.
