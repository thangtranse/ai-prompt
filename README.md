# AI Prompting Guide

## Onboarding & Installation

### Sub repo

1. Clone the repository:

```bash
git submodule add https://github.com/thangtranse/ai-prompt.git .github/ai-prompt
```

### VSCode configuration

1. Update `.vscode/settings.json` with the following configuration:

```json
{
  "chat.agent.maxRequests": 50,
  "chat.customAgentInSubagent.enabled": true,
  "chat.agentSkillsLocations": {
    ".github/ai-prompt/skills": true,
    ".github/skills": true,
    ".claude/skills": true,
    "~/.copilot/skills": true,
    "~/.claude/skills": true
  },
  "chat.promptFilesLocations": {
    ".github/ai-prompt/prompts": true,
    ".github/prompts": true
  },
  "chat.agentFilesLocations": {
    ".github/ai-prompt/agents": true,
    ".github/agents": true
  },
  "chat.instructionsFilesLocations": {
    ".github/ai-prompt/instructions": true,
    ".github/instructions": true,
    ".claude/rules": true,
    "~/.copilot/instructions": false,
    "~/.claude/rules": false
  },
  "github.copilot.chat.commitMessageGeneration.instructions": [
    {
      "file": ".github/ai-prompt/instructions/copilot-commit-message-generation.md"
    }
  ]
}
```

### API documentation workflow

- Use `/document-api` as the entrypoint for documenting a new or changed API.
- Use `/document-feature` as the entrypoint for documenting a feature, workflow, or integration.
- Use `/document-service` as the entrypoint for documenting a service, module, or worker.
- Use `/document-project` as the entrypoint for initializing project-level Mintlify documentation and `docs/docs.json`.
- The existing `document-api`, `document-feature`, and `document-service` prompts run the `Docs Orchestrator` custom agent.
- `/document-project` runs the `Project Docs Orchestrator` custom agent.
- `Docs Orchestrator` routes API-only work to `API Doc Orchestrator`.
- `Docs Orchestrator` routes feature/service/workflow work through `Feature Context Reader`, `Flow Mapper`, `Docs Clarifier`, `Mintlify Docs`, and `Docs QA`.
- `API Doc Orchestrator` still delegates to `API Code Reader`, `API Contract Reader`, `Mintlify Docs`, and `Docs QA` for endpoint-level API documentation.
- `Project Docs Orchestrator` delegates to `Module Context Reader`, `Architecture Checker`, `Project Style Checker`, `Docs Clarifier`, `Mintlify Docs`, and `Docs QA` for project bootstrap.
- `chat.customAgentInSubagent.enabled` must be enabled for custom-agent subagent orchestration.

### Core code review rules

Use the following reusable rules when reviewing or refactoring code for readability and maintainability:

- `rules/arch-avoid-magic-numbers.md`
- `rules/arch-use-meaningful-names.md`
- `rules/db-use-snake-case-model-fields.md`
- `rules/arch-single-purpose-functions.md`
- `rules/arch-use-early-return.md`

Rule interaction:

- Prefer early return for guard clauses to reduce nesting.
- Keep a single main happy-path return when possible.
- Allow one additional return for guard clauses when it makes the function clearer.

# References

1. [VSCode copilot configuration](https://code.visualstudio.com/docs/copilot/reference/copilot-settings#_general-settings)
2. [VSCode config 'code review', 'Commit messages', custom instructions](https://code.visualstudio.com/docs/copilot/customization/custom-instructions#_specify-custom-instructions-in-settings)
3. [Skill NestJS](https://github.com/Kadajett/agent-nestjs-skills)
