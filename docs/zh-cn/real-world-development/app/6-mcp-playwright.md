---
title: "第 6 课 - 使用 Playwright MCP 验证功能"
description: "通过 Customize 配置 Playwright MCP，在现有功能工作树中通过浏览器观察筛选功能。"
authors:
  - geektrainer
lastUpdated: 2026-07-09
---

正如前面提到的，编写代码不只是写代码。我们还需要处理数据、外部服务，并允许 Copilot 使用更多自动化工具。MCP 服务器可以扩展 Copilot app 内置的能力，为它提供更多工具和服务。

本课将学习如何：

- 了解模型上下文协议 (MCP) 以及 GitHub Copilot app 如何使用它。
- 添加 Playwright MCP 服务器。
- 让智能体驱动浏览器并探索筛选功能。

## 场景

单元测试和端到端测试很重要，但验证 UI 更新需要实际与 UI 交互。你希望 Copilot 像用户一样使用正在开发的网站，进一步自动化更改的验证流程，并增强对功能符合预期的信心。

## 什么是模型上下文协议 (MCP)？

[模型上下文协议 (MCP)][mcp-blog-post] 为 AI 智能体提供与外部工具和服务通信的方式。通过 MCP，AI 智能体可以实时访问最新信息（使用资源），并代表你执行操作（使用工具）。

智能体通过 MCP 服务器访问这些工具和资源。MCP 服务器充当 AI 智能体与外部工具和服务之间的桥梁，负责管理双方之间的通信；外部工具可以是现有 API，也可以是 NPM 包等本地工具。每个 MCP 服务器都代表 AI 智能体可以访问的一组工具和资源。

常见的 MCP 服务器包括：

- **[GitHub MCP Server](https://github.com/github/github-mcp-server)**：提供一组用于管理 GitHub 存储库的 API，让 AI 智能体可以创建和更新存储库，并管理议题和拉取请求。
- **[Playwright MCP Server][playwright-mcp-server]**：通过 Playwright 提供浏览器自动化能力，让 AI 智能体可以浏览网页、填写表单和选择按钮。

还有许多其他 MCP 服务器提供不同工具和资源。GitHub 托管了 [MCP 注册表](https://github.com/mcp)，方便大家发现并为生态系统做出贡献。

> [!CAUTION]
> 对待 MCP 服务器时，应像对待项目中的其他依赖项一样考虑安全问题。使用前，请仔细审查源代码、验证发布者并评估安全影响。只使用信任的 MCP 服务器，并谨慎授予其访问敏感资源或执行敏感操作的权限。

## 添加 Playwright MCP 服务器

通过侧边栏中的 **Customize** 管理 MCP 服务器。在存储库或 Copilot CLI 中配置的服务器可能已在 app 中可用，因此添加前先检查，避免重复。[App 自定义文档][customize-app]介绍了可用选项。

1. 在侧边栏中选择 **Customize**。
2. 打开 **All types** 下拉菜单并选择 **MCP**，然后检查 **Installed** 列表中是否已有 Playwright 服务器。
3. 如果尚未安装 Playwright，请在可用服务器中找到 **Playwright**，然后选择 **Add server**。
4. 批准前审查发布者、配置和所有安装提示。按照提示添加服务器；组织策略或缺少先决条件可能会阻止设置。
5. 返回处于 **Interactive** 模式的筛选会话，确认 Playwright MCP 工具可用。

如果设置失败，请先解决配置或权限问题，再继续。

## 要求 Copilot 使用 Playwright 探索功能

议题和规划决策已包含在上下文中。要求 Copilot 启动服务器前，先停止之前启动的所有开发服务器。

1. 使用以下提示，让 Copilot 验证新功能：

    ```plaintext
    Start the app and use Playwright MCP to check filtering against the issue and our plan. Tell me what works and what doesn't, without making changes. Stop the server you started when you're done.
    ```

> [!NOTE]
> 不必明确要求 Copilot 使用特定 MCP 服务器；它通常会根据当前上下文自行判断。不过，明确指出你认为重要的信息始终是合理做法。

2. 观察 Copilot 在浏览器中执行的操作。

Copilot 会启动服务器、打开浏览器并与网站交互。完成后，它会停止服务器并提供报告。

## 总结和后续步骤

恭喜！你使用 Playwright MCP 服务器，从 GitHub Copilot app 在真实浏览器中探索了功能。回顾一下，你：

- 了解了模型上下文协议 (MCP) 以及 GitHub Copilot app 如何使用它。
- 添加了 Playwright MCP 服务器。
- 让智能体驱动浏览器并探索筛选功能。

接下来创建一个[自定义 QA 智能体][next-lesson]，将技能和浏览器工具整合到专门角色中。

## 资源

- [什么是 MCP，为什么大家都在谈论它？][mcp-blog-post]
- [Microsoft Playwright MCP Server][playwright-mcp-server]
- [在 GitHub Copilot app 中配置 MCP 服务器][customize-app]

[next-lesson]: ../7-qa-agent/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[customize-app]: https://docs.github.com/copilot/how-tos/github-copilot-app/customize-github-copilot-app
