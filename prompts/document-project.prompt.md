---
name: document-project
description: Initialize project-level Mintlify documentation by analyzing modules, architecture, and project style, asking the user for the target layout, and bootstrapping `docs/docs.json` plus the initial docs structure.
agent: Project Docs Orchestrator
argument-hint: project name, repo scope, docs bootstrap target, or initialization summary
---

Use [the project docs bootstrap skill](../skills/project-doc-bootstrap/SKILL.md) as the execution contract.

Initialize project documentation for `${input:target:project name, repo scope, docs bootstrap target, or initialization summary}`.

Use the current editor selection when it adds signal:

${selection}

Expected outcome:

- inspect the repository module-by-module with subagents
- review architecture and project style through specialized agents
- ask the user which Mintlify layout should be used before writing
- build a normalized `project-doc-brief`
- create or update `docs/docs.json` and the initial Mintlify docs structure
- report assumptions, gaps, conflicts, and follow-up items explicitly
