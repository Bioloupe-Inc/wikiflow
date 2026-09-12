# Wiki viewer prototype

Question: which graph-based layout makes it easiest to understand a proposed wiki change together on a call?

This is a throwaway, read-only UI study with illustrative content. It does not connect to a repository, PR, account, or review system. Discussion happens verbally. No layout has been selected for implementation.

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

Keep this source on `codex/wiki-viewer-prototype`. Capture the chosen layout and the question it settles after user feedback; retain only the validated design in the main project.
