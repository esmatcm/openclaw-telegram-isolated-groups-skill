# OpenClaw Telegram Isolated Groups Skill

AgentSkill for configuring **fully isolated Telegram group routing** in OpenClaw.

This repository packages a reusable skill for the pattern:

- **one group = one agent**
- **one agent = one workspace**
- isolated memory files per workspace
- independent model selection per group
- explicit `chatId` bindings
- verification and troubleshooting workflow

## What this skill covers

- creating a fresh agent for a Telegram group
- assigning a unique workspace and model
- allowing the group in `channels.telegram.groups`
- binding a Telegram `chatId` to the target agent
- detecting unknown `chatId` values from OpenClaw logs
- verifying the final setup and fixing common mistakes

## Repository layout

```text
telegram-isolated-groups/
  SKILL.md
  references/
    checklist.md
    troubleshooting.md
```

## Use cases

Use this skill when you need to:

- onboard a new Telegram group into OpenClaw
- migrate a group off a shared agent
- stop cross-group memory pollution
- audit whether a group is bound correctly
- recover from `reason: not-allowed` routing failures

## Package the skill

```bash
python3 /opt/homebrew/lib/node_modules/openclaw/skills/skill-creator/scripts/package_skill.py telegram-isolated-groups
```

## Release artifact

The packaged `.skill` file can be attached to a GitHub Release for distribution.

## License

MIT
