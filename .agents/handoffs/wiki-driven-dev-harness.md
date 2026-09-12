# Handoff: Wiki-Driven Development Harness, grill in progress

Written 2026-09-12 from a session in the `JoziGila/skills` repo (a fork of `mattpocock/skills`), branch `claude/wiki-driven-dev-harness-wwzk0n`. Nothing has been committed; the branch is clean at `3cca18b`. The next session cannot clone, so this document is self-contained: it carries the original design handoff, a description of how the repo's skills work today, the grill so far, and the open frontier.

**What the next session is for:** continue the grill. Do not draft `SKILL.md` files or the linter until the frontier below is empty and the user confirms shared understanding.

## Suggested skills

If the next harness has them, call the Skill tool for:

- `grilling`: the interview discipline. Rounds, the frontier, numbered questions each with a recommended answer, an HR between questions. Format reproduced under "Grilling format" below in case the skill is not available.
- `writing-for-agents`: when drafting finally starts, for the style of `SKILL.md` files.

## Part 1: the original design handoff (verbatim, from the conversation before this one)

Compacted from a design conversation (Sept 11 to 12, 2026).

### Problem

Small team, everyone works with their own AI coding agents. Things move too fast for conventional process. Two specific pains:

1. Multiple people's agents change the same codebase in parallel with nothing coordinating them.
2. Things ship before anyone has decided whether they should.

Constraint from the user: review should happen at the spec level. Code is an implementation detail that must align with the spec.

### Path taken (and rejected)

- Started with classic docs (PRD, design doc/RFC, ADR) and a five-stage process. Rejected as compensating for code being expensive, which it no longer is.
- Considered a "global spec as compressed representation of code" with spec deltas and code convergence. Kept the idea, dropped the heavyweight form.
- Considered `main` = aligned state, PR = transaction, auto-generated DAG of mutations. Rejected as too rigid.
- Brainstormed looser shapes (spec-as-tests, swarm scratchpad, continuous reconciliation, inverted flow, two-speed lanes, etc.). Kept: grill-based shaping, ticket-based DAG, rebuild-from-spec as a smoke alarm.
- Considered folder-based spec. Rejected in favor of flat, atomic, wikilinked notes (Obsidian-style, Zettelkasten).
- Considered a literal cellular-automaton ruleset with node states. Rejected as over-engineered; the intent was only "simple writing rules produce the organization."

### Converged design

**Primitives**

- A **note** is one claim (claim-titled, e.g. "refund sum never exceeds captured amount").
- A **link** means "depends on."
- Code files link to the claims they implement (comment or decorator, e.g. `// [[refund-sum-bounded-by-capture]]`).
- Flat `wiki/` directory. Obsidian for browsing (vault = `wiki/`), git for truth. Frontmatter carries `kind` (decision | behavior | term | constraint) for filtering only.

**Invariant**

Every commit leaves the wiki well-shaped. Hard, statically checkable, sub-second:

- every note has a parent (except root)
- every link resolves
- fan-out within a band (roughly 2 to 9 children per parent)
- notes under a length threshold
- top layer at most a handful of notes
- no duplicate titles

Enforced by a pre-commit hook, a PreToolUse hook on `git commit` for agents, and CI as backstop. `main` and every commit are green by construction.

Soft metrics (dashboard/warnings, not gates): percent of code files with an inbound claim, unconfirmed links older than N days, open contradictions, near-duplicate claims.

**The one user-invoked skill: `/grill`**

Fork of Matt Pocock's `grill-with-docs` with the "update CONTEXT.md and ADRs" step replaced by graph maintenance operators.

1. **Orient**: search wiki around the topic, load claims two hops up, read soft-metric report for the region.
2. **Interview**: until each answer is one claim wide; check every answer against existing claims (confirm / correct / contradict).
3. **Emit a graph delta**: new, changed, merged, split, pruned, summarized claims plus links, placed so shape rules hold. Open questions become notes. Commit.
4. **Run `to-tickets`** over the unconfirmed region: one ticket per link needing confirmation, blocking edges from link direction, each ticket body carrying the claim and its neighborhood.

Modes: pointed at an idea (shape a feature), at a file (extract claims from code), at a contested note (mediate).

Compression operators the skill applies on every touch: extract, merge, split, summarize, prune, confirm. Hierarchy is the emergent result of repeated summarization, not a designed taxonomy.

**Implementation (Pocock skills, unchanged)**

`/implement` ticket → worktree → `/tdd` at the seam → `/code-review` (Spec axis reads the claim) → PR closes ticket → link confirmed.

**Sweep**

A scheduled tick runs `/grill` unattended on the worst-scoring region, restricted to judgment-light operators (merge obvious duplicates, prune dead claims, propose summaries). Lands as a small PR.

**Human touchpoints**

Exactly three: answering grill questions; approving a graph delta on a region they own (CODEOWNERS on wiki notes); reading a verifier report that didn't come back clean.

**Bootstrap**

One-time weekend pass: agent extracts claims for every file, summarizes into a pyramid, humans skim the top two levels, flip the gate on. Escape hatch if too big: a real `_undescribed` parent that no new file may link to.

### Rules for agents (AGENTS.md sketch)

1. Everything links up. No orphans.
2. Write where it belongs, not where you are.
3. Say it once. Merge or link duplicates.
4. Too long means two notes.
5. Code cites what it implements.
6. If you learn a claim is false, change or delete it in the same change that taught you.

### Open questions (from the original handoff)

- Exact fan-out band and note length threshold (tune empirically).
- How much of the near-duplicate detection needs a model vs. title similarity.
- Whether code-coverage-by-claims ever becomes a hard gate (currently soft).
- Which agent runtime to standardize on (affects hook/skill formats). Pocock's skills ship for Claude Code natively and Codex via `npx skills`.
- Tracker choice (GitHub Issues / Linear / local files). `to-tickets` supports all; the tracker is a disposable view of the graph.

### References checked

- mattpocock/skills: grill-me, grill-with-docs, to-spec, to-tickets (tracer-bullet tickets with blocking edges), implement, tdd, code-review (Standards + Spec axes as parallel sub-agents), wayfinder, improve-codebase-architecture. Philosophy: small composable skills, explicitly against process-owning frameworks (GSD, BMAD, Spec-Kit).
- LangChain OpenWiki: agent-maintained descriptive wiki of a codebase, Grounded Claims tied to source evidence, OKF format. Useful as bootstrap seed and as an as-built mirror; not a substitute for the prescriptive wiki.
- Böckeler (Thoughtworks) on SDD levels: spec-first / spec-anchored / spec-as-source; MDD-failure warning. Design here is spec-anchored.
- OpenSpec (delta-based change proposals), Spec Kit, Kiro, Tessl: surveyed, not adopted.
- arXiv 2609.00252 on team-scale agentic engineering and the review-capacity productivity paradox.

## Part 2: how the repo works today

Read from the repo this session. This is what the wiki harness replaces or builds on.

### Repo structure and rules

- Skills live under `skills/<bucket>/<name>/SKILL.md` with an `agents/openai.yaml` beside each (Codex metadata). Buckets: `engineering/` and `productivity/` (promoted: in the plugin, in the top-level README, each with a docs page), `in-progress/` (beta, public, flat list in its README, no docs page, not in the plugin), `misc/`, `deprecated/`.
- **User-invoked** skills set `disable-model-invocation: true` and `policy.allow_implicit_invocation: false`; only a human can fire them, and no other skill can call them. **Model-invoked** skills have a trigger-rich description and can be called by other skills via "Call the Skill tool with `<name>`".
- `ask-matt` is the router documenting every user-reachable skill. Any new user-reachable skill must be added to it.
- Repo rules that bite: no em-dashes in any prose; a changeset per change; `scripts/link-skills.sh` symlinks every non-deprecated, non-misc skill into `~/.claude/skills` and `~/.agents/skills`.
- Nothing is enforced by hooks or CI. Every rule is prose the agent may or may not follow. The linter would be the first hard gate in the system.

### Layer 1: per-repo config (`/setup-matt-pocock-skills`, user-invoked)

Run once in a target repo. Explores, asks three questions, writes `docs/agents/*.md` and an `## Agent skills` block in `CLAUDE.md`:

- `issue-tracker.md`: GitHub (`gh` CLI), GitLab (`glab`), local markdown under `.scratch/<feature>/`, or freeform. Every skill that says "publish to the tracker" or "fetch the ticket" reads this file.
- `triage-labels.md`: five canonical roles (`needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, `wontfix`) mapped to real label strings.
- `domain.md`: tells every engineering skill to read `CONTEXT.md` (glossary) and `docs/adr/` (decisions) before exploring code, use the glossary's words, and flag ADR conflicts. If the files are absent, proceed silently.

The tracker is the only shared state between sessions.

### Layer 2: the main flow, idea to ship

1. **`/grill-with-docs`** (user-invoked). A two-line skill that calls two model-invoked skills: `grilling` (the interview) and `domain-modeling` (writes `CONTEXT.md` glossary terms inline as they resolve, and an ADR when a decision is hard to reverse, surprising without context, and a real trade-off; challenges terms against the glossary, sharpens fuzzy language, stress-tests with scenarios, cross-references with code).
2. **`/prototype` via `/handoff`** (optional): a runnable answer to a design question, on a `prototype/<name>` branch.
3. **`/to-spec`** (user-invoked). No interview. Synthesizes the conversation into a fixed template (problem, solution, long user-story list, implementation decisions, testing decisions, out of scope). Makes the user agree the test **seams** (ideally one). Publishes with `ready-for-agent`.
4. **`/to-tickets`** (user-invoked). Splits the spec into tracer-bullet vertical slices, each declaring which tickets block it. User approves the breakdown, then it publishes blockers-first. Native blocking links on GitHub, a `Blocked by:` line locally.
5. **`/implement`** (user-invoked). Per ticket, in a fresh context: drive `tdd` at the pre-agreed seams, run `code-review`, commit. `implement-spec` (in-progress) is the concurrent version: tickets as a task graph, implementer subagents in worktrees across the ready frontier, one PR.
6. **`code-review`** (model-invoked). Two parallel subagents. Standards: documented repo standards plus a fixed Fowler smell baseline. Spec: finds the originating spec (commit-message issue refs, an argument, or a file under `docs/`, `specs/`, `.scratch/`) and reports missing requirements, scope creep, wrong implementations. Reports are never merged.

Context rule: steps 1 to 4 in one unbroken window; each `/implement` starts fresh from its ticket.

### Layer 3: on-ramps and standalone

`/triage` (issue state machine, can call `grilling` and `domain-modeling`), `/diagnosing-bugs`, `/wayfinder` (map issue plus decision tickets for foggy efforts, merges onto the flow at `/to-spec`), `/improve-codebase-architecture` and `codebase-design` (module-shape vocabulary), `/research`, `/to-questionnaire`, `/wizard`, `/wait-what`, `/teach`, `/handoff`.

### What a ticket is today

- **Derived from a spec, one-way.** Closing a ticket never edits the spec; the spec is never re-read after the breakdown.
- **Vertical, not horizontal.** A complete path through every layer, demoable on its own. Wide refactors are the exception: expand, migrate in batches, contract.
- **Sized to one context window**, so the body is self-sufficient: what to build from the user's perspective, acceptance criteria, blockers. No file paths or code snippets.
- **A node in a task graph.** Blocking edges; the **frontier** is every ticket whose blockers are closed.
- **Agent-grabbable by construction**: published with `ready-for-agent`, skipping triage.
- Not a spec, not a record of state. Once closed, the codebase is the only trace.
- Repo vocabulary (`CONTEXT.md`): canonical term is **Issue**; "ticket" only when quoting external systems or for a `wayfinder` **Decision ticket**.

### `to-tickets` templates (so the next session can reason about ticket bodies)

Local file per ticket at `.scratch/<feature-slug>/issues/<NN>-<slug>.md`:

```
# <NN>: <Ticket title>
**What to build:** end-to-end behaviour, user's perspective.
**Blocked by:** numbers/titles, or "None (can start immediately)".
**Status:** ready-for-agent
- [ ] Acceptance criterion
```

Real tracker: sections `## Parent`, `## What to build`, `## Acceptance criteria`, `## Blocked by`.

### Grilling format (from the `grilling` skill)

Interview relentlessly until shared understanding. Map a design tree. Each round asks the whole **frontier** (every question whose prerequisites are settled), numbered, each with a recommended answer, separated by `---`:

```
❓ **Q1** - **<title>**: <body>

➡️ <recommended answer>
```

Facts are the agent's job (look them up); decisions are the user's. Done when the frontier is empty. Do not act until the user confirms shared understanding.

## Part 3: the grill so far

### Settled

| # | Decision | Answer |
|---|---|---|
| 1 | Replacement or parallel flow | **Replacement.** In a wiki-enabled repo, `/grill-with-wiki` replaces `grill-with-docs` → `to-spec` → `to-tickets`. The unmodified main flow stays for repos without a wiki. |
| 2 | Fork-only or upstream-shaped | **Fork-only.** Ship in `in-progress/` so bucket rules apply, but don't constrain the design to what upstream would take. |
| 3 | What a ticket is | **Reframed by the user:** a ticket is how we get from the wiki's current state to an approved new state of the wiki-spec. The code work is whatever closes that gap. This makes the tracker derivable from the wiki, not just a disposable view. |

Agent observations accepted without objection (treat as provisional, not settled):

- "Fork `grill-with-docs`" really means "write a new wrapper over `grilling` that swaps `domain-modeling` for graph maintenance". The interview primitive stays untouched.
- `to-tickets` is user-invoked, so no skill can call it. Step 4 of `/grill` either becomes a hand-off line to the human ("now run `/to-tickets`") or the ticket emission is written into the new skill itself.
- Naming: `grill-with-wiki` (matches `grill-with-docs`, keeps `ask-matt` readable). Not yet confirmed by the user.
- Three components likely: `grill-with-wiki` (user-invoked), a model-invoked graph-maintenance reference (operators and shape rules, the thing that replaces `domain-modeling`, so the sweep and `code-review` can share it), and `setup-wiki` (user-invoked, installs `wiki/`, linter, hooks, `AGENTS.md` rules, CODEOWNERS, rewritten `domain.md`; follows the `setup-ts-deep-modules` pattern of shipping the config file inside the skill folder).

### Open frontier (last round asked, not yet answered)

❓ **Q1** - **Is the wiki on `main` allowed to be ahead of the code?**: (a) `main`'s wiki carries approved claims with a status marker (`proposed` until code satisfies them, then `confirmed`), so the set of `proposed` notes *is* the backlog; or (b) `main`'s wiki only describes what the code does, and the approved delta lives on a branch until implementation lands with it.

➡️ (a). Spec-anchored means the wiki leads. The backlog becomes a query, and "proposed for more than N days" is the staleness metric.

---

❓ **Q2** - **What is the approval act?**: Does `/grill-with-wiki` commit its delta to a branch and open a wiki-only PR, so CODEOWNERS on `wiki/` forces the right reviewer and merge is the approval? Or commit to `main` directly with tickets carrying the approval?

➡️ Wiki-only PR, merge is approval. Reuses review machinery, one-claim notes make the diff readable, and it gives a clean "tickets are emitted on merge" trigger. Cost: one PR per grill session.

---

❓ **Q3** - **Ticket granularity**: one ticket per approved delta (whole feature, no concurrency); one per claim (a claim with three children isn't independently demoable); or one per connected sub-delta confirmable on its own, blocking edges following link direction.

➡️ Connected sub-delta. Keeps the vertical-slice rule and gives `implement-spec` a real frontier. Body: the sub-delta's notes copied in plus the two-hop neighborhood.

---

❓ **Q4** - **What flips `proposed` to `confirmed`?**: The implementing PR edits the note's status in the same PR as the code. Should the linter make it a hard gate that a note may only become `confirmed` in a commit where some code file cites it by wikilink?

➡️ Yes. Statically checkable, sub-second, and it turns the citation from a convention into the only way to close a ticket, so nobody has to be told to cite.

---

❓ **Q5** - **Retire `CONTEXT.md` and ADRs in wiki repos?**: `kind: term` and `kind: decision` notes cover both; keeping them means two sources of vocabulary truth.

➡️ Retire. `setup-wiki` rewrites `docs/agents/domain.md` to point the other skills at `wiki/` filtered by kind, so `tdd`, `triage`, `to-tickets` follow the pointer unedited.

---

❓ **Q6** - **Separate `setup-wiki` skill?**: or extend `setup-matt-pocock-skills` with a Section D.

➡️ Separate, user-invoked, run after `setup-matt-pocock-skills`.

### Questions queued for later rounds (blocked on the frontier above)

- Where confirmation status lives: per note (frontmatter `status`) or per link. Depends on Q1 and Q4.
- Drift: what happens when code later contradicts a `confirmed` claim. Who detects it (the sweep, `code-review`, a test), and what state does the note enter.
- Whether `code-review`'s Spec axis should learn to resolve `wiki/` links directly (option b from an earlier round) once the loop has run on one module. For the first spike, ticket bodies carry the claims copied in so promoted skills stay unchanged.
- Whether the `to-tickets` emission becomes part of `grill-with-wiki` or stays a hand-off to the human, given `to-tickets` is user-invoked and cannot be called. If it moves into the skill, whether the tracker choice still comes from `docs/agents/issue-tracker.md`.
- Sweep runtime: a scheduled Claude Code Remote routine, a GitHub Action, or a cron on someone's machine. Affects which hook format the linter ships.
- Linter language: dependency-free is what makes the pre-commit hook sub-second. Node matches the repo; a single-file script with no install step matches the target repos better.
- Fan-out band and note length threshold, the near-duplicate detection method, and the coverage soft-metric: all carried over from the original open questions, all "tune empirically".
- Bootstrap mode ("pointed at a file, extract claims from code") and mediate mode ("pointed at a contested note") have not been discussed at all beyond the handoff's one line each.

### Suggested next step for the new session

Present the six open frontier questions again, take the answers, recompute the frontier from the queued list, and keep going until it is empty. Then, and only then, draft `SKILL.md` for `grill-with-wiki`, the graph-maintenance reference, `setup-wiki`, and the shape-linter spec, and run the loop on one feature in one module.
