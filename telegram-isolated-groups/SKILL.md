---
name: telegram-isolated-groups
description: Set up OpenClaw Telegram groups with strict one-group-one-agent isolation, including unique workspaces, isolated memory files, model separation, group allowlisting, routing bindings, and verification/troubleshooting. Use when creating a new Telegram group bot route, migrating a group off a shared agent, fixing cross-group memory pollution, or auditing whether a Telegram group is bound to the correct OpenClaw agent.
---

# Telegram Isolated Groups

Configure Telegram groups so each group uses its own OpenClaw agent, workspace, memory, and model.

## Core rules

- Create one agent per group.
- Give each agent its own workspace.
- Keep memory files isolated inside that workspace.
- Bind each Telegram `chatId` to exactly one agent.
- Verify with logs and active sessions after every change.

## Workflow

### 1. Collect inputs

Gather:

- target Telegram `chatId`
- new `agentId`
- workspace path
- model name or alias
- whether the group should require `@mention`

If the `chatId` is unknown, detect it from OpenClaw logs before binding.

### 2. Create the isolated agent

Run:

```bash
openclaw agents add <agentId> \
  --workspace <workspacePath> \
  --model <modelAliasOrFullModel> \
  --non-interactive
```

Prefer short predictable ids such as `qun3` or `grp_<chatid_suffix>`.

### 3. Allow the Telegram group

Edit `~/.openclaw/openclaw.json` and add the group under:

- `channels.telegram.groups[chatId].enabled = true`
- `channels.telegram.groups[chatId].requireMention = false` unless the user explicitly wants mention-gating

If the logs show `reason: not-allowed`, fix this section first.

### 4. Bind the group to the new agent

Add or replace a binding:

```json
{
  "agentId": "<agentId>",
  "match": {
    "channel": "telegram",
    "peer": { "kind": "group", "id": "<chatId>" }
  }
}
```

Remove any conflicting binding for the same `chatId`.

### 5. Restart or reload gateway

Use:

```bash
openclaw gateway restart
openclaw gateway status
openclaw agents list --bindings
```

If the host uses systemd user services, ensure the gateway service is installed and running.

### 6. Verify isolation

Confirm all of the following:

- `openclaw agents list --bindings` shows the correct `chatId -> agentId`
- the workspace path is unique
- recent logs show the target group hitting the intended agent
- active sessions land in the expected agent session
- no other group shares that agent unless the user explicitly wants shared state

## Detecting unknown chat IDs

When the user only knows the group title, inspect logs.

Useful patterns:

```bash
grep -Ei "telegram-auto-reply|not-allowed|chatId|conversationId|peer=group" /tmp/openclaw/openclaw-$(date +%F).log
```

The cleanest case is a skipped-group entry like:

- title
- `chatId`
- `reason: not-allowed`

Use that `chatId` for the final binding.

## Troubleshooting

Read `references/troubleshooting.md` when:

- a group is skipped as `not-allowed`
- messages land in the wrong agent
- two groups share memory accidentally
- the gateway is installed but not running
- Telegram network requests are timing out

## Verification checklist

Read `references/checklist.md` before declaring the setup finished.
