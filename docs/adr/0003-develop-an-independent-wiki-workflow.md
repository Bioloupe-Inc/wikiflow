---
status: accepted
---

# Develop an independent wiki workflow

WikiFlow starts from [Matt Pocock's skills](https://github.com/mattpocock/skills) and evolves independently to coordinate a small team of coding agents and keep human review focused on the system specification. In repositories that adopt the wiki, the new workflow replaces the inherited specification-and-ticket pipeline; repositories without a wiki keep the inherited flow. We accept divergence from upstream rather than constrain this design to upstream compatibility, while retaining the original license and attribution.

The new skills will begin in `in-progress/`. Skill names, composition, wiki mechanics, and migration remain design work; the [open questions](../../.agents/handoffs/wiki-driven-dev-harness.md) track that work. The repository was detached from its GitHub fork on 2026-09-12 and transferred to the Bioloupe-Inc organization the same day as `Bioloupe-Inc/wikiflow`. The package and plugin are named `wikiflow`, and the current router and setup skills are `ask-wikiflow` and `setup-wikiflow`. Rebranding does not implement the proposed workflow.

A replacement for the existing [setup skill](../../skills/engineering/setup-wikiflow/SKILL.md) prepares a repository for the wiki workflow. It builds the full initial wiki across the existing system and sets up the Issue templates and CI/CD. Source handling, treatment of conflicting evidence, pipeline responsibilities, and completion criteria remain design work.
