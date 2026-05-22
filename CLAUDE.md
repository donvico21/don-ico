# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

This workspace configures Claude Code to run against GoDaddy's internal Anthropic API proxy (GoCode), rather than the public Anthropic API. It is not a traditional application codebase.

## Launching Claude Code

Run the startup script from PowerShell to set the required environment variables and start Claude Code:

```powershell
.\start-gocode.ps1
```

This sets:
- `ANTHROPIC_BASE_URL` — GoDaddy's internal GoCode endpoint (`caas-gocode-prod.caas-prod.prod.onkatana.net`)
- `ANTHROPIC_MODEL` — `claude-sonnet-4-6`
- `GOCODE_API_TOKEN` / `ANTHROPIC_AUTH_TOKEN` — API credentials for the GoCode proxy
- `CLAUDE_CODE_DISABLE_EXPERIMENTAL_BETAS=1` — disables experimental beta features

Do not launch `claude` directly without running this script first, or it will attempt to use the public Anthropic API with incorrect credentials.

## Settings

`.claude/settings.local.json` contains the project-level permission allowlist. Permissions added via `/allowed-tools` or the Claude Code UI are written here.
