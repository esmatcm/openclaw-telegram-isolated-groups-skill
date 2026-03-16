# OpenClaw Telegram 多群完全独立配置 Skill / OpenClaw Telegram Isolated Groups Skill

把 **OpenClaw 的 Telegram 多群独立配置** 整理成一份可复用、可发布、可审计的 AgentSkill。

这份 Skill 的目标很明确：

- **一群一代理**
- **一代理一工作区**
- **一工作区一套记忆**
- **每个群可独立模型**
- **按 chatId 精确绑定**
- **配置后必须验证，不靠猜**

## 这个仓库解决什么问题

当 Telegram 多个群共用同一个 agent 时，最常见的问题就是：

- 群与群之间记忆污染
- 回复跑错群 / 走错 agent
- `not-allowed` 但不知道真正 chatId
- 改了配置却没有完整验收

这个仓库把这些坑整理成一套标准 Skill，方便直接复用。

## 核心能力

- 为新 Telegram 群建立独立 agent
- 分配唯一 workspace 与 model
- 在 `channels.telegram.groups` 中放行目标群
- 将指定 `chatId` 绑定到目标 agent
- 从 OpenClaw 日志中侦测未知群 ID
- 验证最终配置是否真的隔离成功
- 排查 `reason: not-allowed`、绑错群、共享记忆等常见问题

## 适用场景

适合以下需求：

- 新增 Telegram 群并接入 OpenClaw
- 把群从共用 agent 拆成独立 agent
- 避免不同群之间记忆污染
- 检查群是否绑到正确的 agent
- 排查 Telegram 群被 `not-allowed` 跳过的问题

## 仓库结构

```text
telegram-isolated-groups/
  SKILL.md
  references/
    checklist.md
    troubleshooting.md
```

## 快速打包

```bash
python3 /opt/homebrew/lib/node_modules/openclaw/skills/skill-creator/scripts/package_skill.py \
  telegram-isolated-groups
```

## 发布方式

打包得到的 `.skill` 文件可直接附加到 GitHub Release。

---

This repository packages an AgentSkill for **fully isolated Telegram group routing** in OpenClaw.

Its purpose is simple:

- **one group = one agent**
- **one agent = one workspace**
- **one workspace = one memory boundary**
- **independent model per group**
- **exact chatId binding**
- **verification after every change**

## What problem this repository solves

When multiple Telegram groups share one agent, common failures include:

- cross-group memory pollution
- wrong replies landing in the wrong group or agent
- `not-allowed` groups with unknown chat IDs
- incomplete verification after config changes

This repository turns that messy operational knowledge into a reusable OpenClaw skill.

## Core capabilities

- create a dedicated agent for each Telegram group
- assign a unique workspace and model
- allow the group under `channels.telegram.groups`
- bind a specific `chatId` to the target agent
- detect unknown `chatId` values from OpenClaw logs
- verify that isolation is actually working
- troubleshoot `reason: not-allowed`, wrong bindings, and shared-memory mistakes

## Use cases

Use this skill when you need to:

- onboard a new Telegram group into OpenClaw
- migrate a group off a shared agent
- stop cross-group memory pollution
- audit whether a group is bound correctly
- recover from `reason: not-allowed` routing failures

## Repository layout

```text
telegram-isolated-groups/
  SKILL.md
  references/
    checklist.md
    troubleshooting.md
```

## Quick packaging

```bash
python3 /opt/homebrew/lib/node_modules/openclaw/skills/skill-creator/scripts/package_skill.py \
  telegram-isolated-groups
```

## Release artifact

The packaged `.skill` file can be attached directly to a GitHub Release.

## License

MIT
