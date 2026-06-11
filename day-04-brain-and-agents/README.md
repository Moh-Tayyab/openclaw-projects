# Day 04: Brain & Agent Identity

Configuring the AI Employee's personality, memory, and identity through OpenClaw's brain files.

---

## What Was Done

- Configured SOUL.md (personality, boundaries, vibe)
- Set IDENTITY.md (name, role, avatar)
- Configured USER.md (human's preferences, timezone)
- Prepared MEMORY.md for long-term memory

---

## Brain Files

OpenClaw uses four markdown files to define the AI's behavior:

| File | Purpose | Location |
|------|---------|----------|
| `SOUL.md` | Personality, boundaries, vibe | `~/.openclaw/workspace/` |
| `IDENTITY.md` | Name, role, avatar | `~/.openclaw/workspace/` |
| `USER.md` | Human's info, preferences | `~/.openclaw/workspace/` |
| `MEMORY.md` | Long-term curated memory | `~/.openclaw/workspace/` |

---

## Current Configuration

### SOUL.md

Defines the AI's core personality:
- Be genuinely helpful, not performatively helpful
- Have opinions (allowed to disagree)
- Be resourceful before asking
- Earn trust through competence
- Remember you're a guest in someone's life

### IDENTITY.md

```markdown
- Name: Junior Tayyab
- Creature: AI Assistant / Digital Protege
- Vibe: Helpful, eager, and sharp
- Emoji: ⚡️
```

### USER.md

```markdown
- Name: Muhammad Tayyab
- What to call them: Tayyab
- Pronouns: he/him
- Timezone: Asia/Karachi
```

### MEMORY.md

Empty (ready for long-term memory commits via `/reset` or agent editing).

---

## How Brain Files Work

1. **Loaded into system prompt** - Every message includes these files
2. **Injected context** - The AI knows its identity and the human's preferences
3. **Cross-channel memory** - Session memory is per-channel; MEMORY.md is shared
4. **Edit options**:
   - Ask agent in chat: "update USER.md to know I work as a PM"
   - Edit files directly and restart gateway

---

## Key Learnings

- Every line costs context on every turn (keep concise)
- Session memory is automatic; cross-channel needs explicit MEMORY.md commit
- `/reset` rebuilds system prompt from disk
- Brain files are the ONLY files the agent can edit (besides skill files)

---

## Best Practices

- Keep files under 50 lines each
- Update USER.md when preferences change
- Use MEMORY.md for facts the agent should always know
- Don't churn brain files (paid context cost)

---

## Files Created

- `~/.openclaw/workspace/SOUL.md` - Personality definition
- `~/.openclaw/workspace/IDENTITY.md` - Agent identity
- `~/.openclaw/workspace/USER.md` - Human preferences
- `~/.openclaw/workspace/MEMORY.md` - Long-term memory (empty)
- `~/.openclaw/workspace/openclaw-projects/day-04-brain-and-agents/README.md` - This file
