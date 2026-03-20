# AI Prompting Guide

## Onboarding & Installation

### Sub repo

1. Clone the repository:

```bash
git submodule add https://github.com/thangtranse/ai-prompt.git .github/ai-prompt
```

2. Pull the latest changes from the submodule:

```bash
git subtree pull --prefix=.github/ai-prompt origin main --squash
```

3. Push the changes to your repository:

```bash
git subtree push --prefix=.github/ai-prompt origin main
```

### VSCode configuration

1. Update `.vscode/settings.json` with the following configuration:

```json
{
  "chat.agent.enabled": true
  "chat.agent.maxRequests": 50
}
```
