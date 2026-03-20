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

# References

1. [VSCode copilot configuration](https://code.visualstudio.com/docs/copilot/reference/copilot-settings#_general-settings)
2. [VSCode config 'code review', 'Commit messages', custom instructions](https://code.visualstudio.com/docs/copilot/customization/custom-instructions#_specify-custom-instructions-in-settings)
