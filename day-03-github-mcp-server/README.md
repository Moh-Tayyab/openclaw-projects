# Day 03: GitHub MCP Server

Connecting OpenClaw to GitHub for repository management, commits, and PR creation.

---

## What Was Done

- Configured GitHub MCP server in OpenClaw
- Fixed SSH key configuration for git operations
- Verified SSH connection to GitHub
- Tested MCP server connectivity

---

## Components

| Component | Details |
|-----------|---------|
| MCP Server | `github` (stdio transport) |
| Command | `npx -y @modelcontextprotocol/server-github` |
| Token | GitHub Personal Access Token (from `gh` CLI) |
| SSH Key | `~/.ssh/id_ed25519_github` (ED25519) |
| SSH Config | `~/.ssh/config` (fixed newline issue) |

---

## Setup Steps

### 1. GitHub MCP Server

```bash
openclaw mcp set github '{
  "command": "npx",
  "args": ["-y", "@modelcontextprotocol/server-github"],
  "env": {
    "GITHUB_PERSONAL_ACCESS_TOKEN": "gho_your_token_here"
  }
}'

openclaw gateway restart
```

### 2. SSH Key Fix

The SSH config file had literal `\n` characters instead of proper newlines. Fixed by rewriting:

```bash
# ~/.ssh/config
Host github.com
  IdentityFile ~/.ssh/id_ed25519_github
  StrictHostKeyChecking no
```

### 3. Verify SSH

```bash
ssh -T git@github.com
# Expected: Hi Moh-Tayyab! You've successfully authenticated...
```

---

## Key Learnings

- SSH config file must have proper newlines (not literal `\n`)
- `gh` CLI token can be reused for MCP server
- MCP server needs gateway restart to pick up changes
- Probe timeout may need increase for first-time npx downloads

---

## Troubleshooting

| Issue | Fix |
|-------|-----|
| SSH Permission denied | Check `~/.ssh/config` has proper newlines |
| MCP probe timeout | First download takes time; increase timeout |
| Key not found | Ensure `IdentityFile` path matches actual key name |
| GitHub rejects key | Verify fingerprint matches: `ssh-keygen -lf key.pub` |

---

## Available MCP Tools

Once connected, OpenClaw agent can:
- Create/clone repositories
- Commit and push changes
- Create/merge pull requests
- Manage issues
- Search code
- Read file contents

---

## Files Modified

- `~/.openclaw/openclaw.json` - MCP server config
- `~/.ssh/config` - Fixed SSH configuration
- `~/.openclaw/workspace/openclaw-projects/day-03-github-mcp-server/README.md` - This file
