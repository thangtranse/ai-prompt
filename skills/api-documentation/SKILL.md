---
name: api-documentation
description: '**WORKFLOW SKILL** — Create and maintain API documentation in Mintlify MDX format. Analyze handler code, create MDX pages, update docs.json navigation. USE FOR: writing docs for new API endpoints, updating docs for API changes, converting old docs to Mintlify. DO NOT USE FOR: general coding questions; non-API documentation; runtime debugging. INVOKES: Mintlify Docs agent, file system tools, grep/search tools.'
---

# API Documentation Skill

## Workflow Overview

This skill guides the creation of complete API documentation following Mintlify structure, from code analysis to publishing docs.

## Step-by-Step Process

### 1. Analyze API Code
- Read handler function to understand logic, auth, params, response
- Grep routes.js to find endpoint path and method
- Identify auth requirements (sessionAuth, etc.)
- Analyze error handling and response formats
- **Understand code logic of router (routes.js), controller (handlers), service (helpers) processing**
- Trace flow from route → middleware → handler → helper calls
- Understand data flow, validations, business logic in all layers
- **If API has middleware, describe middleware chain and processing logic in detail**

### 2. Draft MDX Content
- Use Mintlify Docs agent to generate MDX page
- Structure according to API Reference format:
  - Endpoint info (method, path, handler)
  - Authentication requirements
  - Request/Response schemas
  - Error codes
  - Examples
- Write in Vietnamese for Vietnamese users

### 3. Add Logic Description
- Describe API processing logic in detail from all layers
- Router: middleware chain, routing logic
- **Middleware: if present, describe each middleware in chain (auth, validation, logging, etc.)**
- Controller: main handler logic, error handling
- Service: helper functions, business logic, data processing
- Include processing flow, conditions, data transformations
- Explain business rules and edge cases

### 4. Document Relations
- List external services: Redis, RabbitMQ, PostgreSQL, etc.
- Describe how API interacts with them (cache keys, message queues, DB queries)
- Dependencies and integrations

### 5. Add Operational Notes
- Points to note when deploying/maintaining
- Performance considerations
- Monitoring points
- Common failure scenarios

### 6. Suggest Refactors (if needed)
- Identify code smells or technical debt
- Propose improvements for maintainability, performance
- Suggest safer rollout strategies if there are risks

### 7. Update Navigation
- Add new page to docs.json navigation
- Ensure "API Reference" dropdown has new page
- Create introduction page if not exists

### 8. Validate and Publish
- Check links and references
- Verify MDX syntax
- Test navigation flow

## Quality Criteria

- Docs must cover fully: auth, params, responses, errors
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
- Include sections: Logic Description, Relations, Operational Notes, Refactor Suggestions (if applicable)
- **Must understand and document logic from all layers: router (routes.js), controller (handlers), service (helpers)**
- **If API has middleware, must describe middleware chain and processing logic**

## Decision Points

- If API is complex (multi-step logic): Create flow diagram
- If there are related APIs: Link in "Related APIs" section
- If auth is complex: Detail each required credential

## Completion Check

- MDX file created in docs/api-reference/
- docs.json updated with new page
- Content accurate and complete
- No broken links

## Bundled Assets

- MDX template for API docs
- Example docs.json updates
- Validation checklist script