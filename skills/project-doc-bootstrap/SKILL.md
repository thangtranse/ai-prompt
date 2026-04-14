---
name: project-doc-bootstrap
description: '**WORKFLOW SKILL** — Initialize Mintlify documentation for a project. Gather a verified module inventory, architecture findings, and project style conventions through specialized subagents, ask the user to choose a Mintlify layout, then create `docs/docs.json` and the initial documentation structure. USE FOR: first-time docs setup; project-wide docs bootstrap; repo-wide information architecture planning. DO NOT USE FOR: single endpoint docs; incremental page edits; generic copywriting.'
argument-hint: project name, repo scope, docs bootstrap target, or initialization summary
---

# Project Docs Bootstrap Skill

## Workflow Overview

This skill is the execution contract for bootstrapping project-level Mintlify documentation from an existing codebase.

Use it with this custom-agent pipeline:

- `Project Docs Orchestrator` coordinates the workflow
- `Module Context Reader` inventories modules and documentation surfaces
- `Architecture Checker` reviews architecture and system boundaries
- `Project Style Checker` extracts project conventions and style expectations
- `Docs Clarifier` identifies ambiguity, missing evidence, and unresolved assumptions
- `Mintlify Docs` creates `docs/docs.json` and the initial Mintlify page structure
- `Docs QA` validates the generated structure and navigation

Separate repository analysis from documentation generation. Do not ask the writer to infer project structure from raw files when a normalized brief can be prepared first.

## Step-by-step process

### 1. Inspect the repository and setup state

- Check whether `docs/` exists
- Check whether `docs/docs.json` already exists
- Identify likely application roots such as `src/`, `apps/`, `packages/`, `libs/`, `modules/`, or framework-specific entrypoints
- Detect whether API contract artifacts already exist, such as OpenAPI or Swagger files

### 2. Ask the user for the target layout before writing

If the repository does not already have an approved Mintlify navigation structure, ask the user a concise setup question covering:

- preferred Mintlify layout shape: `groups`, `tabs`, `dropdowns`, `anchors`, or custom
- documentation language
- OpenAPI/Swagger path, if one exists
- project title and short description, if those are not obvious from the repository

Do not create `docs/docs.json` until the layout choice is explicit.

### 3. Gather repository findings with subagents

- Use `Module Context Reader` to sweep the repository by module or domain area
- Use `Architecture Checker` to identify architectural layers, shared infrastructure, boundaries, and risks
- Use `Project Style Checker` to extract naming conventions, directory conventions, testing patterns, and style rules worth preserving in docs
- Use `Docs Clarifier` to preserve uncertainty, terminology conflicts, or missing evidence

### 4. Build a normalized `project-doc-brief`

Prepare a concise structured brief with at least:

- project summary
- source files consulted
- repository roots inspected
- module inventory
- architecture findings
- project style conventions
- docs audience and language
- chosen Mintlify layout
- OpenAPI/Swagger input, if any
- proposed `docs/docs.json` shape
- proposed initial page tree
- assumptions and unresolved gaps
- rollout or maintenance notes

### 5. Create the Mintlify bootstrap

- Use `Mintlify Docs` to create or update `docs/docs.json`
- Create the initial page structure under `docs/`
- Keep navigation and folder names aligned with the chosen layout and the analyzed module boundaries
- Prefer a minimal but scalable initial structure over generating dozens of low-signal pages

### 6. Validate before closing

- Use `Docs QA` to verify `docs/docs.json`, navigation integrity, and page structure
- Confirm the generated structure reflects the chosen layout instead of an assumed default
- Keep unresolved assumptions visible in the output

## Quality criteria

- The workflow asks for layout before initializing Mintlify structure
- The project bootstrap uses verified repository findings, not guesses
- The initial docs tree reflects real module boundaries and architecture
- The generated `docs/docs.json` is coherent and maintainable
- Assumptions, layout choices, and missing inputs remain explicit

## Completion check

- A `project-doc-brief` was prepared
- The user's layout choice was captured explicitly
- `docs/docs.json` was created or updated through `Mintlify Docs`
- The initial documentation structure under `docs/` was created
- `Docs QA` returned validation findings and a pass/fail conclusion
