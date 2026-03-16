# OpenClaw Telegram 多群完全独立配置 Skill

中文主说明已整合进仓库根目录 `README.md`，并且默认中文在前、英文在后。

这个文件只保留给需要纯中文入口的人快速查看。

## 核心原则

- 一群一代理
- 一代理一工作区
- 独立记忆边界
- 独立模型
- 精确 chatId 绑定
- 每次改完都要验证

## 主要能力

- 建立新的 Telegram 群独立 agent
- 侦测真正 chatId
- 修复 `not-allowed`
- 校验 bindings
- 验证最终隔离是否成功
