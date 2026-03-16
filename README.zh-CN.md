# OpenClaw Telegram 多群完全独立 Skill

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

## License

MIT
