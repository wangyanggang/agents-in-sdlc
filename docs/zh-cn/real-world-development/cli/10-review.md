---
title: "第 10 课 - 总结和后续步骤"
description: "回顾 Copilot CLI 工作流、两个拉取请求、可复用的自定义项和更多资源。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

你通过一套连续的 Tailspin Toys 工作流使用了 GitHub Copilot CLI。你：

- 准备了 Codespace、安装了 Copilot CLI、探索项目并找到预先创建的筛选议题。
- 添加了星级评分，在转发的浏览器中审查结果，并手动合并了第一个拉取请求 (PR)。
- 从筛选议题开始，在 Plan 模式中确定方案、在 Autopilot 模式中构建功能，并在 Interactive 模式中审查。
- 使用自定义说明引导智能体，随后自定义现有的 `quality-checks` 技能，并用它运行单元测试、lint 和类型检查。
- 添加 Playwright 模型上下文协议 (MCP) 服务器，并用它在真实浏览器中探索筛选功能。
- 创建并选择质量保证 (QA) 自定义智能体，评估需求、覆盖率、技能结果和浏览器证据。
- 审查完整的筛选功能更改，并授权 Agent Merge 合并筛选 PR。
- 探索了用于管理上下文、模型、共享和可选云委派的斜杠命令。

## 交付成果

本工作坊包含两个 PR 阶段，每个阶段都从更新后的 `main` 分支创建独立分支：

1. **星级评分**：在游戏卡片上显示现有的 `starRating` 和明确的未评分状态。
2. **筛选功能与质量工作流**：实现筛选功能，更新说明并应用到功能中，自定义 `quality-checks` 报告，创建 QA 配置文件并添加相关测试。

从规划筛选功能到创建 PR，你一直使用同一个对话和分支。为了简化工作坊，这些更改被合并到一个 PR 中。

## 不同类型的验证

你通过多种方式检查了代码：自动测试、亲自在浏览器中检查，以及使用 MCP 让 Copilot 在浏览器中探索。`quality-checks` 技能运行了单元测试、lint 和类型检查，并按新格式报告结果。QA 智能体在 PR 创建之前，综合审查这些结果、需求和测试覆盖率。

新增测试应解决实际缺口；如果 QA 检查后发现不需要新测试，也可能是合理结果。授权合并前，审查代码和证据；更改后应重新生成受影响的验证证据。

## 最佳实践

提供给 Copilot 的上下文和工具会影响它的工作。在本工作坊中，你更新了说明、自定义技能、创建 QA 配置文件并配置 MCP 服务器。可以在不同对话中复用这些自定义项，并随着团队需求变化进行调整。说明用于设定标准，技能用于描述可重复任务，自定义智能体用于定义专业角色，MCP 服务器用于连接外部工具。审查实际更改和工具结果，而不只是智能体的总结。

根据任务选择**模式和模型**。使用 **Plan** 在构建前思考方案，使用 **Interactive** 参与专注的更改，使用 **Autopilot** 处理范围明确的任务。常规编辑可以选择响应更快的模型，复杂工作则选择能力更强的模型。

上下文和基础设施同样重要。明确描述希望构建的*内容*、*原因*和*方式*，会显著影响输出。

## 继续探索

你已经完成核心工作流。还可以进一步了解以下 CLI 功能：

- 使用 `/review` 让代码审查智能体分析更改。
- 使用 `/rubber-duck` 讨论问题并获取另一种观点。
- 使用 `/fleet` 并行协调独立子任务。
- 使用 `/worktree` 隔离单独的任务。
- 使用 `/delegate` 将任务发送给 Copilot 云智能体。

## 下一步

持续使用任何工具，都是提高能力的最佳方式！可以用它编写生产代码、兴趣项目，或者多年来一直想构建却没时间动手的小应用。与团队分享经验，也向团队成员学习。别忘了继续探索文档。

如果想继续在终端中扩展 Tailspin Toys，可以接着学习可选的 [Foundry Backer Concierge 系列][foundry]。若想比较其他工作环境，还可以探索 [VS Code 工作坊][vscode]、[GitHub Copilot app 工作坊][app]或 [Copilot 云智能体工作坊][cloud]。

## 资源

- [关于 GitHub Copilot CLI][about-cli]
- [Copilot CLI 命令参考][cli-reference]
- [自定义 Copilot CLI][customize-cli]
- [使用 Copilot CLI 管理拉取请求][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
