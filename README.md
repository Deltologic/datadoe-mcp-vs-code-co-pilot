# DataDoe MCP + VS Code Copilot Template

This repository is a starter template for integrating DataDoe MCP with **VS Code + GitHub Copilot** in a secure, team-friendly way.

## Table of Contents

- [What you can do with this repo](#what-you-can-do-with-this-repo)
- [What This Repo Includes](#what-this-repo-includes)
- [Prerequisites](#prerequisites)
- [How to get a DataDoe subscription and get MCP Key](#how-to-get-a-datadoe-subscription-and-get-mcp-key)
- [Configure DataDoe MCP in VS Code + Copilot](#configure-datadoe-mcp-in-vs-code--copilot)
- [Example prompt library starter pack](#example-prompt-library-starter-pack)
- [VS Code Copilot Settings](#vs-code-copilot-settings)
- [DataDoe MCP Configuration Options](#datadoe-mcp-configuration-options)
- [How to Get Help](#how-to-get-help)

## What you can do with this repo

- Connect GitHub Copilot chat to DataDoe MCP in a secure way.
- Ask Amazon seller questions using DataDoe-backed data.
- Reuse this setup as a template for new Amazon-focused assistant projects.

## What This Repo Includes

- VS Code + Copilot MCP setup via `.vscode/mcp.json`
- Secure secret handling with `.env` and `.env.example`
- Agent instructions in `AGENTS.md` for GitHub Copilot
- `.gitignore` configured to protect secrets

## Prerequisites

- [Visual Studio Code](https://code.visualstudio.com/) (latest stable)
- [GitHub Copilot extension](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot) installed and active
- A valid DataDoe subscription
- A generated DataDoe MCP key

## How to get a DataDoe subscription and get MCP Key

1. Go to [app.datadoe.com](https://app.datadoe.com)
2. Create account
3. Purchase subscription
4. Accept Terms and Conditions and Privacy Policy
5. Go to `Integrations`
6. Click `MCP` tile (`/integrations/mcp`)
7. Click `MCP Key`, add name + expiration, click `Create`
8. Copy key and store in a secure secret manager

## Configure DataDoe MCP in VS Code + Copilot

### Option A: Use the included `.vscode/mcp.json` (recommended)

This repository already includes `.vscode/mcp.json` configured with a secure input prompt for your API key. When Copilot first connects to the DataDoe MCP server, VS Code will prompt you to enter your API key.

The config uses VS Code's built-in `input` variables so your key is never stored in the file:

```json
{
  "inputs": [
    {
      "type": "promptString",
      "id": "datadoe-key",
      "description": "DataDoe MCP API Key",
      "password": true
    }
  ],
  "servers": {
    "datadoe": {
      "type": "http",
      "url": "https://api.datadoe.com/mcp/v1",
      "headers": {
        "datadoe-mcp-key": "${input:datadoe-key}"
      }
    }
  }
}
```

### Option B: Hardcode the key directly (quick setup, not recommended for teams)

Replace the config with your key inline:

```json
{
  "servers": {
    "datadoe": {
      "type": "http",
      "url": "https://api.datadoe.com/mcp/v1",
      "headers": {
        "datadoe-mcp-key": "YOUR_API_KEY"
      }
    }
  }
}
```

### Verify in VS Code

1. Open the Command Palette (`Cmd+Shift+P` / `Ctrl+Shift+P`)
2. Run **MCP: List Servers**
3. Confirm `datadoe` appears and shows as connected

Reference: [VS Code MCP server docs](https://code.visualstudio.com/docs/copilot/customization/mcp-servers)

## Example prompt library starter pack

To help you start faster with an AI Agent + DataDoe MCP workflow, this repo includes a small prompt library at:

- `.vscode/prompts/EXAMPLES.md`

Use it as a starter pack:

1. Open `.vscode/prompts/EXAMPLES.md`.
2. Copy a prompt block and adjust placeholders (for example `{{seller_name}}`) to your account context.
3. Run the prompt in GitHub Copilot chat with DataDoe MCP enabled.
4. Save your own high-performing prompts in the same file to build a reusable internal playbook.

## VS Code Copilot Settings

VS Code + GitHub Copilot uses these configuration files:

- **Workspace MCP config**: `.vscode/mcp.json` (shared with this repository team)
- **Agent instructions**: `AGENTS.md` (team-shared assistant guidance for Copilot)
- **VS Code settings**: `.vscode/settings.json` (workspace-level editor settings)

To customize Copilot behavior for this project, edit `AGENTS.md` at the repository root.

Reference: [VS Code MCP configuration reference](https://code.visualstudio.com/docs/copilot/reference/mcp-configuration)

## DataDoe MCP Configuration Options

The MCP server is configured in `.vscode/mcp.json` using `servers` key with `type: "http"`:

```json
{
  "servers": {
    "datadoe": {
      "type": "http",
      "url": "https://api.datadoe.com/mcp/v1",
      "headers": {
        "datadoe-mcp-key": "${input:datadoe-key}"
      }
    }
  }
}
```

> [!CAUTION]
> Treat `DATADOE_MCP_KEY` like a password. Do not publish repositories, screenshots, or logs that contain this key.
> Never commit real keys to git.
> If a key is exposed, rotate it immediately.

## How to Get Help

- Email: [contact@datadoe.com](mailto:contact@datadoe.com)
- GitHub Copilot Documentation: [https://docs.github.com/en/copilot](https://docs.github.com/en/copilot)
- VS Code Documentation: [https://code.visualstudio.com/docs](https://code.visualstudio.com/docs)
- VS Code MCP servers: [https://code.visualstudio.com/docs/copilot/customization/mcp-servers](https://code.visualstudio.com/docs/copilot/customization/mcp-servers)
