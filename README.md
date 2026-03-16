# OpenClaw Telegram 多群完全独立 Skill / OpenClaw Telegram Isolated Groups Skill

这是一个用于 **OpenClaw Telegram 群组完全独立配置** 的 AgentSkill。

它把这套规范整理成可复用流程：

- **一群一代理**
- **一代理一工作区**
- 每个工作区拥有独立记忆文件
- 每个群可独立指定模型
- 使用明确的 `chatId` 绑定
- 附带验证与故障排查步骤

## 这个 Skill 能做什么

- 为新 Telegram 群建立独立 agent
- 分配唯一 workspace 与 model
- 在 `channels.telegram.groups` 中放行目标群
- 将指定 `chatId` 绑定到目标 agent
- 从 OpenClaw 日志中侦测未知群 ID
- 验证最终配置是否真的隔离成功
- 处理 `reason: not-allowed`、绑错群、共享记忆等常见问题

## 仓库结构

```text
telegram-isolated-groups/
  SKILL.md
  references/
    checklist.md
    troubleshooting.md
```

## 适用场景

适合以下需求：

- 新增 Telegram 群并接入 OpenClaw
- 把群从共用 agent 拆成独立 agent
- 避免不同群之间记忆污染
- 检查群是否绑到正确的 agent
- 排查 Telegram 群被 `not-allowed` 跳过的问题

## 打包命令

```bash
python3 /opt/homebrew/lib/node_modules/openclaw/skills/skill-creator/scripts/package_skill.py telegram-isolated-groups
```

## 发布方式

打包得到的 `.skill` 文件可直接附加到 GitHub Release。

---

This repository packages an AgentSkill for **fully isolated Telegram group routing** in OpenClaw.

It turns the following rules into a reusable workflow:

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
