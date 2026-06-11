# Day 02: Slack Integration

Connecting OpenClaw to Slack for team communication and AI-assisted workflows.

---

## What Was Done

- Installed OpenClaw Slack plugin (`openclaw-slack`)
- Created Slack App with Bot Token + App Token
- Configured Socket Mode for real-time messaging
- Connected Slack workspace to OpenClaw gateway

---

## Prerequisites

- Slack workspace (free tier works)
- Slack App created at https://api.slack.com/apps
- Bot Token (`xoxb-...`)
- App Token (`xapp-...`)

---

## Configuration Steps

### 1. Create Slack App

1. Go to https://api.slack.com/apps
2. Click "Create New App" > "From scratch"
3. Enter app name and select workspace
4. Go to **OAuth & Permissions** > add scopes:
   - `chat:write`
   - `channels:history`
   - `channels:read`
   - `groups:history`
   - `groups:read`
   - `im:history`
   - `im:read`
   - `mpim:history`
5. Go to **Socket Mode** > enable > generate App Token with `connections:write` scope
6. Go to **Event Subscriptions** > enable > subscribe to:
   - `message.channels`
   - `message.groups`
   - `message.im`
   - `app_mention`
7. Install app to workspace

### 2. Configure OpenClaw

```bash
# Set bot token
openclaw config set channels.slack.botToken --secret-input-mode ref --ref-source env --ref-id SLACK_BOT_TOKEN

# Set app token
openclaw config set channels.slack.appToken --secret-input-mode ref --ref-source env --ref-id SLACK_APP_TOKEN
```

### 3. Enable and Restart

```bash
openclaw config set channels.slack.enabled true
openclaw gateway restart
```

### 4. Verify

```bash
openclaw channels status --probe
```

---

## Key Learnings

- Socket Mode is preferred over webhooks for development (no public URL needed)
- Bot Token handles API calls; App Token maintains WebSocket connection
- DM policy `pairing` is safest default (human auto-authorized, strangers get one-time code)
- Groups need `groupPolicy: open` + `@mention` to respond

---

## Troubleshooting

| Issue | Fix |
|-------|-----|
| Bot not responding | Check `openclaw channels status --probe` |
| Socket disconnects | Verify App Token has `connections:write` scope |
| No DM access | Bot needs `im:read` + `im:history` scopes |
| Group mentions not working | Set `groupPolicy: open` in config |

---

## Files Created

- `~/.openclaw/openclaw.json` - Slack config section
- `~/.openclaw/workspace/openclaw-projects/day-02-slack-integration/README.md` - This file
