# Troubleshooting

## Group message skipped with `reason: not-allowed`

Cause: the group is not present under `channels.telegram.groups` or is disabled.

Fix:

1. Add `chatId` under `channels.telegram.groups`
2. Set `enabled: true`
3. Restart or reload gateway
4. Re-test from the Telegram group

## Message reaches the wrong agent

Cause: wrong or conflicting binding.

Fix:

1. Inspect `openclaw agents list --bindings`
2. Remove the old binding for that `chatId`
3. Add the correct binding
4. Restart gateway
5. Re-test

## Two groups share memory

Cause: both groups point to one agent or one workspace was reused.

Fix:

1. Create a fresh agent
2. Assign a unique workspace
3. Move the target `chatId` binding to the new agent
4. Verify that no other group still points to that agent

## Gateway installed but not running

On macOS, check LaunchAgent status.
On Linux, check the systemd user service.

Typical commands:

```bash
openclaw gateway install
openclaw gateway status
systemctl --user start openclaw-gateway.service
```

## Telegram network timeouts

Typical symptoms in logs:

- `sendMessage failed`
- `sendChatAction failed`
- `UND_ERR_CONNECT_TIMEOUT`

Interpretation: OpenClaw is up, but network access to Telegram is unstable.

Check:

- server outbound network
- DNS resolution
- firewall rules
- VPN or proxy path
- whether `api.telegram.org` is reachable from the host

Do not confuse network failure with routing failure.
