---
name: document-api
description: Analyze a new or changed API, route it through the top-level docs workflow, reconcile implementation with Swagger/OpenAPI, and generate Mintlify docs.
agent: Docs Orchestrator
argument-hint: feature name, endpoint path, route file, handler symbol, or API change summary
---

Use [the API documentation workflow skill](../skills/api-documentation/SKILL.md) as the execution contract.

Document the API change described by `${input:target:feature name, endpoint path, route file, handler symbol, or API change summary}`.

Use the current editor selection when it adds signal:

${selection}

Expected outcome:

- classify the request and route it through the top-level docs orchestration workflow
- inspect implementation behavior from code
- reconcile it with Swagger, OpenAPI, schemas, tests, or examples when available
- build a normalized `api-doc-brief`
- write or update Mintlify documentation under `docs/`
- update `docs/docs.json` when navigation changes are required
- report contract drift, assumptions, and follow-up items explicitly
