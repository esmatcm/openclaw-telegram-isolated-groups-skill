# Verification Checklist

Use this checklist after every Telegram group isolation change.

- Agent exists and has the expected model.
- Workspace path is unique and not reused by another group.
- `channels.telegram.groups[chatId]` exists and is enabled.
- `requireMention` matches the requested behavior.
- Exactly one binding exists for the target `chatId`.
- No unrelated group points at the new agent.
- Gateway restart or reload completed successfully.
- `openclaw agents list --bindings` shows the intended mapping.
- Recent logs show the target group entering through the expected path.
- A test message in the target group reaches the intended agent.
- Memory and daily notes will be written in the agent's own workspace.

If any item fails, do not mark the setup complete.
