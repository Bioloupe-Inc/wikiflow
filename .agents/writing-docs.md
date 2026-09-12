# Writing skill docs

Every promoted skill has a human-facing page at `docs/<bucket>/<skill-name>.md`, mirroring `skills/engineering/` and `skills/productivity/`. Add or update the page when a skill is added, renamed, or changes behavior. Rename or move the page with the skill. Non-promoted buckets get no docs page.

These pages belong to WikiFlow and are read in this repository. Use relative links within the repo, or canonical `https://github.com/Bioloupe-Inc/wikiflow/blob/main/...` links when an absolute URL is needed. Links to upstream issues and other external sources retain their original destinations.

A page helps a person choose a skill and understand its result. It explains the available behavior, while proposed wiki-workflow changes belong in the design records. Link to the root README's [installation section](../README.md#installation) instead of copying commands; [.agents/install-block.md](./install-block.md) owns their wording.

## Page structure

Use these sections in order. The four required sections are **What it does**, **When to reach for it**, **Common questions**, and **It's working if**. Add **Where it fits** to connect the page to the router. Other sections earn their place only when the skill needs them.

### What it does

One or two paragraphs stating the skill's job and its defining constraint. Explain what makes it useful, without reproducing its instructions or templates.

### When to reach for it

State how it is invoked: only by the user, or also by the agent when the task fits. Explain the trigger boundary, including the choice between neighboring skills where readers might confuse them. Put several alternative situations in a short list or table.

### Prerequisites (optional)

State required configuration, tools, and the workspace it writes into. For tracker-dependent skills, link to `setup-wikiflow`. Omit this section when there is no prerequisite.

### Substance (optional)

Use one to three short sections in the skill's vocabulary to explain its central idea, output, or consequential choice. Keep procedural detail in `SKILL.md`.

### Common questions

Use bold questions followed by concise answers. Prefer questions from the current conversation, relevant repository issues, and `CHANGELOG.md`. Use `gh issue list --repo Bioloupe-Inc/wikiflow --search "<skill-name>" --state all` when current issues would help. Historical upstream reports remain useful evidence, but their status is not WikiFlow's status.

When evidence is thin, answer only questions a reader needs to use this skill. Do not pad the section. State limitations directly and distinguish current behavior from proposed changes.

### It's working if

Name observable results a person can check without reading the skill's source: a decision becomes clearer, a bug is reproduced, or the resulting document is useful. Avoid internal formatting and source-shape checks.

### Where it fits

Name its role and the one or two neighboring skills that matter, explaining why. Link to [ask-wikiflow](../docs/engineering/ask-wikiflow.md) for the full map instead of repeating it.

## Done when

- The page matches the current skill's name, invocation policy, behavior, and prerequisites.
- All four required sections are present, in order, and the page connects to the router.
- Local links resolve and external citations retain their source identity.
- No stale page survives a rename or bucket move.
- The page explains the skill to a person without duplicating its runbook or installation commands.
