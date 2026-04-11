---
name: document-service
description: Analyze a service, module, or worker, build a normalized documentation brief, and generate Mintlify docs through the Docs Orchestrator workflow.
agent: Docs Orchestrator
argument-hint: service/module name, worker/job, integration point, or change summary
---

Use [the general documentation orchestration skill](../skills/docs-orchestration/SKILL.md) as the execution contract.

Document the service or module described by `${input:target:service/module name, worker/job, integration point, or change summary}`.

Use the current editor selection when it adds signal:

${selection}

Expected outcome:

- classify the request and gather read-only findings with subagents
- build a normalized `feature-doc-brief` or merged brief
- write or update Mintlify documentation under `docs/`
- update `docs/docs.json` when navigation changes are required
- report assumptions, gaps, conflicts, and follow-up items explicitly
