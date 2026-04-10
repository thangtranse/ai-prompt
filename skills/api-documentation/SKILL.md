---
name: api-documentation
description: '**WORKFLOW SKILL** — Coordinate API documentation for new or changed endpoints. Extract runtime behavior from code, reconcile it with OpenAPI/Swagger or other contract sources, build a normalized api-doc-brief, then use Mintlify Docs to write Mintlify MDX and update docs navigation. USE FOR: new API endpoints; API behavior changes; API doc backfills. DO NOT USE FOR: generic feature docs; non-API copywriting; runtime debugging.'
argument-hint: feature name, endpoint path, route file, handler symbol, or API change summary
---

# API Documentation Skill

## Workflow Overview

This skill is the workflow contract for documenting a new or changed API in Mintlify.

Use it with the custom-agent pipeline in this repository:

- `Docs Orchestrator` is the top-level router when the request enters through a prompt such as `/document-api`
- `API Doc Orchestrator` coordinates the work
- `API Code Reader` extracts real runtime behavior from code
- `API Contract Reader` reads OpenAPI/Swagger and other contract artifacts
- `Mintlify Docs` writes the final MDX and updates `docs/docs.json`
- `Docs QA` validates structure, completeness, and navigation

Separate analysis from writing. Do not ask the writer to infer everything from raw code when a normalized brief can be prepared first.

## Step-by-Step Process

### 1. Identify the API surface

- Confirm which endpoint, route file, handler, or feature is being documented
- Identify whether the task is a brand-new API, a behavior change, or a doc backfill
- Locate related tests, schemas, fixtures, and existing docs before writing anything

### 2. Analyze runtime behavior from code

- Use `API Code Reader` or equivalent code analysis to read the route, middleware, handler, and service layers
- Capture the real method, path, auth model, params, body, responses, errors, and side effects
- Trace the full processing flow from route → middleware → handler → helper/service calls
- If middleware exists, describe the chain and the purpose of each middleware
- Record any business rules, validation branches, caching, queueing, DB writes, or external calls

### 3. Analyze the API contract

- Use `API Contract Reader` or equivalent contract analysis to inspect OpenAPI, Swagger, schema files, fixtures, and API examples
- Compare the declared contract with the actual implementation
- Mark every mismatch explicitly: missing fields, stale examples, outdated status codes, auth drift, naming drift
- If no contract artifact exists, say so clearly and treat code as the primary source of truth

### 4. Build a normalized `api-doc-brief`

Before writing MDX, prepare a concise structured brief with at least:

- endpoint summary
- source files consulted
- method and path
- authentication requirements
- request path, query, headers, and body contract
- response contract and error codes
- middleware chain
- business logic summary
- external relations and side effects
- operational notes and rollout risks
- example requests and responses
- spec drift or unresolved gaps
- proposed docs path and sidebar title

### 5. Write Mintlify docs from the brief

- Use `Mintlify Docs` to convert the normalized brief into production-ready MDX
- Keep repository-specific Mintlify rules in the agent, not duplicated here
- Default to English in this repository unless the user explicitly changes the documentation language
- Update `docs/docs.json` when a new page or navigation entry is required

### 6. Validate before closing

- Use `Docs QA` or an equivalent validation pass to check frontmatter, heading levels, required sections, and navigation
- Verify the page does not invent unsupported request or response details
- Confirm every documented behavior can be traced to code, contract artifacts, or an explicit assumption note

### 7. Capture follow-ups when docs reveal gaps

- If the implementation and contract disagree, call that out instead of silently fixing the narrative
- If examples or schemas are missing, leave an explicit follow-up item
- If the code suggests refactors or rollout risks, add them as recommendations, not hidden assumptions

## Quality Criteria

- Docs must cover fully: auth, params, responses, errors
- Code and spec mismatches must be called out explicitly
- Correct Mintlify MDX format (headings, code blocks, tables)
- Navigation updated correctly
- Links between pages work
- File must have frontmatter:
  ```
  ---
  sidebarTitle: "/endpoint/path"
  title: "Endpoint Title"
  description: "Short description"
  icon: "circle-play"
  ---
  ```
- Start with ## for all headings, do not use #
- End every generated or updated page with `## Todo - Plan` and `## References`
- Include sections: Logic Description, Relations, Operational Notes, Refactor Suggestions (if applicable)
- Must understand and document logic from all relevant layers: router, middleware, controller, service/helper
- If API has middleware, describe the middleware chain and processing logic
- Do not let the writer infer missing contract details from partial context when analysis is incomplete

## Decision Points

- If API is complex (multi-step logic): Create flow diagram
- If there are related APIs: Link in "Related APIs" section
- If auth is complex: Detail each required credential
- If Swagger/OpenAPI is stale: prioritize code as source of truth and mark the drift
- If examples are missing: synthesize only conservative examples that match the verified contract

## Completion Check

- MDX file created in docs/api-reference/
- docs.json updated with new page
- `api-doc-brief` was prepared before the writing phase
- Content accurate and complete
- No broken links

## Bundled Assets

- Workflow contract for `API Doc Orchestrator`
- Brief structure for implementation vs contract reconciliation
- Validation checklist for final Mintlify output
