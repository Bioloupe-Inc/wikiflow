# Issue template research

Date: 2026-09-12

Question: What minimal issue templates fit optional issues, deferred discoveries, evolving product requirements, and implementation through wiki-and-code PRs?

Status: Research and proposed adaptations. No templates, issue types, or external issues have been installed or changed.

## Primary-source findings

### 1. Native issue types classify work

GitHub provides Task, Bug, and Feature types by default for organizations. Organization owners can customize, disable, or delete these types, with a maximum of 25. Types support filtering and project views. This is a classification facility, not a prescribed template taxonomy or a required progression through readiness states.

Source: [GitHub: Managing issue types in an organization](https://docs.github.com/en/issues/tracking-your-work-with-issues/using-issues/managing-issue-types-in-an-organization).

### 2. Templates guide capture through the web interface

GitHub supports Markdown templates and YAML forms, with defaults including labels and issue type. Forms support required and optional fields. Templates become available from the default branch. The chooser can allow blank issues; even when blank issues are disabled, maintainers with write access or above retain a blank-issue option. These mechanisms standardize initial reports without establishing the completeness of later work.

Source: [GitHub: Configuring issue templates](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/configuring-issue-templates-for-your-repository).

### 3. The REST creation contract accepts a body, not form answers

The create-issue endpoint requires a title and accepts an optional body string, labels, assignees, type, and other metadata. Its documented parameters include no template identifier or issue-form answers. Inference: web-form requirements should not be treated as general enforcement over agent-created issues; an agent must deliberately follow the repository's authoring contract.

Source: [GitHub: REST API endpoints for issues, Create an issue](https://docs.github.com/en/rest/issues/issues#create-an-issue).

### 4. CLI creation can supply the issue body directly

The official CLI accepts a title and body, including a body file. Its template option is documented as starting body text, and its web option opens browser creation. Inference: use one content contract for human and agent authors instead of assuming a browser form is automatically applied to every CLI path. The current manual does not establish that all YAML field validations are enforced in direct CLI creation.

Source: [GitHub CLI: gh issue create](https://cli.github.com/manual/gh_issue_create).

### 5. Intake can precede commitment and enrichment

Linear's Triage is an inbox where issues can be reviewed, updated, and prioritized before entering the team's workflow. It supports acceptance, duplicate handling, declining, snoozing, and requesting more information. It therefore provides precedent for capturing incomplete work first and deciding its disposition later, without treating every captured report as an accepted delivery commitment.

Source: [Linear: Triage](https://linear.app/docs/triage).

## Recommended minimal design to evaluate

These are workflow recommendations, not requirements prescribed by the sources.

| Template | Kind of unresolved work | Enough to capture | Enrich when needed |
| --- | --- | --- | --- |
| Bug | Observed or suspected violation of expected behavior | Observation, where it occurred, known evidence or source context | Expected behavior and its basis, reproduction, affected environment, impact, regression check |
| Change | A desired improvement, capability, maintenance task, or refactor | Desired change or motivating problem, why it might matter, source context | Outcome, boundaries, constraints, success conditions, open decisions |
| Investigation | A question or decision requiring inquiry | Question, why the answer matters, starting context | Evidence needed, bounded inquiry, decision criteria, findings and disposition |

- Quick capture should be a sparse use of the appropriate template, not a fourth permanent work type. A short note can be enough. Where even classification is uncertain, allow a generic title and description, then classify during triage without recreating the issue.
- Distinguish template, type, and state. A template prompts useful information; a type classifies work; a state describes its position in a workflow. Backlog, deferred, and ready belong to the latter dimension. An idea is usually an immature Change or Investigation, not necessarily another type.
- Do not require root cause, a working reproduction, scope, priority, ownership, implementation plan, or acceptance criteria merely to preserve a discovery. Add what is known and explicitly preserve uncertainty. Useful information requirements can become stricter when someone takes the work on.
- Change can grow into a lightweight PRD without changing issue identity. Technical work can use the same template with an engineering outcome, such as reduced maintenance cost or removal of an unsupported dependency. Do not force every issue into an end-user story.
- Separate product outcome from decomposition: implementation tasks can become child issues when separate coordination justifies them. They link to shared intent rather than duplicating the parent PRD. A checklist or a standalone PR remains sufficient when no separate issue is useful.
- Investigation should have an answer or decision as its immediate deliverable. Its findings may justify a linked Change or Bug. Do not turn every unanswered implementation detail into a separate investigation issue.
- Prefer short Markdown prompts if agents are the main authors; choose YAML forms if browser intake quality warrants them. In both cases, publish the same minimal authoring rules for agents. Neither choice by itself makes the contents correct or complete.

## Tradeoffs and limits

Three templates preserve useful differences in evidence and resolution while keeping the chooser small. A single universal template is simpler to implement but makes bug and inquiry prompts less useful. Separate Feature, Task, Chore, Refactor, Idea, PRD, and Epic templates introduce overlapping distinctions in this workflow unless observed intake problems justify them.

The three recommended templates need not map one-to-one onto GitHub's default native types. Custom types require organization-level configuration; portable templates should not silently assume that configuration exists. Template names and authoring behavior can be settled before choosing metadata.

These five sources establish platform capabilities and workflow precedent. They do not prove that this exact three-template set is optimal. No external writes or API mutation tests were performed.
