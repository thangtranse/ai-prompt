---
name: docs-orchestration
description: '**WORKFLOW SKILL** — Coordinate feature, workflow, service, and architecture documentation. Classify the request, gather verified read-only findings through specialized subagents, build a normalized brief, then use Mintlify Docs to write MDX and Docs QA to validate the result. USE FOR: feature docs; service/module docs; workflow docs; architecture notes; hybrid feature-plus-API docs. DO NOT USE FOR: endpoint-only API docs when the API workflow is already sufficient; generic copywriting; runtime debugging.'
argument-hint: feature name, service/module, workflow, architecture note, or hybrid documentation target
---

# General Documentation Orchestration Skill

## Workflow Overview

This skill is the workflow contract for non-API and mixed documentation requests in Mintlify.

Use it with the custom-agent pipeline in this repository:

- `Docs Orchestrator` classifies and coordinates the work
- `Feature Context Reader` extracts what exists in code and nearby artifacts
- `Flow Mapper` explains how the system behaves end to end
- `Docs Clarifier` identifies ambiguity, assumptions, and missing evidence
- `API Code Reader` and `API Contract Reader` are optional for hybrid requests with a real API slice
- `Mintlify Docs` writes the final MDX and updates `docs/docs.json`
- `Docs QA` validates structure, completeness, and brief-to-doc consistency

Separate analysis from writing. Do not ask the writer to infer behavior from a pile of raw files when a normalized brief can be built first.

## Step-by-step process

### 1. Classify the request

- Decide whether the request is `feature`, `workflow`, `architecture`, or `hybrid`
- If the request is endpoint-first or contract-first, route it to the API workflow instead of forcing it through the feature workflow
- For hybrid requests, keep the feature/workflow narrative as the top-level frame

### 2. Gather implementation context

- Use `Feature Context Reader` to identify entry points, modules, dependencies, side effects, and scope boundaries
- Use `Flow Mapper` to capture the real trigger-to-output flow, branch points, and safeguards
- Use `Docs Clarifier` to call out unstable terminology, missing evidence, and assumptions that must stay visible
- Use `API Code Reader` and `API Contract Reader` only when the feature documentation genuinely depends on API behavior

### 3. Build a normalized `feature-doc-brief`

Prepare a concise structured brief with at least:

- feature summary
- user/problem context
- source files consulted
- entry points and triggers
- components/services involved
- end-to-end flow
- inputs and outputs
- state changes and side effects
- failure modes and safeguards
- config, flags, and dependencies
- examples / scenarios
- open questions and assumptions
- proposed docs path and sidebar title
- recommended related pages
- recommended diagram type

For hybrid requests, merge in the relevant API findings without duplicating behavior that is already explained at the feature or workflow level.

### 4. Write Mintlify docs from the brief

- Use `Mintlify Docs` to convert the normalized brief into production-ready MDX
- Prefer the brief over raw implementation context
- If the brief is missing required sections, stop and surface the gap instead of writing from guesses
- Update `docs/docs.json` when a new page or navigation entry is required

### 5. Validate before closing

- Use `Docs QA` to check frontmatter, heading levels, required closing sections, navigation updates, and contradictions against the brief
- Confirm assumptions and unresolved gaps stay visible in the output
- Treat unsupported claims and invented examples as failures

## Quality criteria

- Output always includes an intermediate normalized brief
- The main orchestrator does not become the primary code archaeologist
- The writer works from verified findings, not broad inference
- Conflicts between subagent findings are preserved explicitly
- Final docs explain triggers, flow, dependencies, side effects, and safeguards when those concepts matter to the request

## Decision points

- If the request becomes API-first, route to `API Doc Orchestrator`
- If the system behavior is multi-stage, include a Mermaid diagram recommendation in the brief
- If examples are weak or missing, document the limitation and keep examples conservative
- If the request is ambiguous, prefer `Docs Clarifier` output over guessing user intent

## Completion check

- `Docs Orchestrator` selected the correct route
- A `feature-doc-brief` or merged brief was prepared before writing
- `Mintlify Docs` wrote or updated the page under `docs/`
- `docs/docs.json` was updated when required
- `Docs QA` returned findings plus a pass/fail conclusion
