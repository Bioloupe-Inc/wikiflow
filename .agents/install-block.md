# The canonical install block

Keep install commands consistent with these blocks. WikiFlow is distributed from this repository's own Claude Code marketplace and through skills.sh. It has no official-marketplace listing.

## Claude Code

<canonical-block name="claude-code">

```bash
claude plugin marketplace add JoziGila/wikiflow
claude plugin install wikiflow@wikiflow
```

Or, from inside a session:

```text
/plugin marketplace add JoziGila/wikiflow
/plugin install wikiflow@wikiflow
```

</canonical-block>

The plugin ships exactly the promoted engineering and productivity skills. Manage its updates through Claude Code's plugin settings.

## Codex and other agents

<canonical-block name="skills-sh-whole-set">

```bash
npx skills@latest add JoziGila/wikiflow
```

Pick the skills and agents you want. Include `setup-wikiflow` for the current tracker-based engineering flow.

</canonical-block>

For a single skill:

<canonical-block name="skills-sh-one-skill">

```bash
npx skills@latest add JoziGila/wikiflow --skill=<name>
```

```bash
npx skills@latest update <name>
```

</canonical-block>

Choose one install route per agent to avoid duplicate skills. Human-facing skill pages link to the root README's installation section instead of copying commands.
