---
slug: pt-br/real-world-development/app
title: "Aplicativo GitHub Copilot"
description: "Crie, verifique e entregue mudanças na Tailspin Toys com o aplicativo GitHub Copilot, aprendendo sobre modos, personalizações, ferramentas MCP e canvases."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

O **[aplicativo GitHub Copilot](https://docs.github.com/copilot/concepts/agents/github-copilot-app)** é um aplicativo para desktop baseado no Copilot CLI que reúne o desenvolvimento orientado por agentes em um espaço de trabalho único e focado. Ele oferece sessões paralelas de agentes, modos de sessão alternáveis, canvases compartilhados e gerenciamento nativo de issues e pull requests do GitHub — incluindo o **Agent Merge**, que conduz um pull request durante rebases, feedback de revisão, correções de integração contínua (CI) e merge.

O workshop acompanha um fluxo de trabalho contínuo na Tailspin Toys:

1. Prepare o projeto, instale o aplicativo, conecte o repositório e explore o espaço de trabalho e o backlog predefinido.
2. Faça uma mudança pequena na avaliação em estrelas, revise-a no navegador e faça manualmente o merge do primeiro pull request (PR).
3. Comece pela issue de filtragem, defina a abordagem no modo **Plan**, implemente-a no modo **Autopilot** e revise-a no modo **Interactive**.
4. Atualize as instruções do repositório e aplique-as ao trabalho de filtragem.
5. Personalize a skill existente `quality-checks` e use-a para executar as verificações do projeto.
6. Adicione o servidor Model Context Protocol (MCP) do Playwright e use-o para explorar a filtragem em um navegador.
7. Crie um agente personalizado de garantia de qualidade (QA) e use-o para revisar requisitos, cobertura e evidências de verificação.
8. Revise a mudança completa da filtragem e use o Agent Merge no segundo PR.
9. Verifique a disponibilidade de canvases e use o Database Explorer para criar e testar um canvas de triagem vinculado ao repositório. Se os recursos necessários não estiverem disponíveis, registre o impedimento e use a alternativa somente leitura ou continue para o resumo.

Para manter o foco do workshop, você criará dois PRs: um para a avaliação em estrelas e outro para a filtragem, com as atualizações de instruções e da skill, o perfil de QA e os testes. Comece cada um a partir do `main` atualizado. O fluxo de filtragem e qualidade compartilha uma sessão, uma worktree e um branch para que você aproveite o trabalho ao explorar cada ferramenta. O exercício final de canvas permanece na própria sessão para que você se concentre em criar e testar esse canvas compartilhado sem repetir o fluxo de PR.

## Lições

| Lição | Tópico | Descrição |
|--------|-------|-------------|
| [0. Pré-requisitos][ex0] | Configuração | Instale o Node.js e crie sua cópia do projeto Tailspin Toys |
| [1. Instale o aplicativo Copilot][ex1] | Configuração | Instale o aplicativo, conecte o projeto e conheça o espaço de trabalho |
| [2. Adicione avaliações em estrelas: uma melhoria rápida][ex2] | Primeira mudança | Exiba as avaliações existentes e o estado sem avaliação, depois faça merge do PR 1 |
| [3. Modos de agente: Plan e Autopilot][ex3] | Modos de agente | Planeje a funcionalidade a partir da issue, implemente-a com Autopilot e revise-a no modo Interactive |
| [4. Oriente o Copilot com instruções personalizadas][ex4] | Contexto | Explore e atualize as instruções e aplique-as à filtragem |
| [5. Personalize e use uma skill quality-checks][ex5] | Verificações repetíveis | Explore a skill existente, altere o formato do relatório e execute-a |
| [6. Valide a funcionalidade com MCP do Playwright][ex6] | Observação no navegador | Configure o MCP por meio de Customize e examine o comportamento da filtragem |
| [7. Crie e use um agente de QA][ex7] | Requisitos e cobertura | Crie e selecione um perfil especializado e reúna as evidências finais de verificação |
| [8. Crie e faça merge do PR da funcionalidade][ex8] | Revisão e merge | Revise a filtragem, as instruções, a skill, o perfil de QA e os testes e use o Agent Merge no segundo PR |
| [9. Explore e crie canvases][ex9] | Colaboração | Use o Database Explorer e, em seguida, crie e teste um canvas de triagem vinculado ao repositório |
| [10. Revisão e próximos passos][ex10] | Resumo | Revise o fluxo, os artefatos e outros recursos |

## Pré-requisitos

Antes de participar deste workshop, confira se você tem:

- [ ] Uma conta do GitHub com um plano **Copilot Student, Pro, Pro+, Business ou Enterprise** ativo
- [ ] Um computador com **macOS, Linux ou Windows**
- [ ] O [Git instalado][install-git] no computador

> [!TIP]
> Não tem um plano pago? Estudantes com status verificado podem usar o GitHub Copilot gratuitamente pelo [GitHub Education][callout-student-plan-education]. O plano **Copilot Student** inclui o agente, MCP, revisão de código e os recursos do Copilot CLI usados neste workshop — então você pode concluir todos os roteiros com esse plano.

> [!NOTE]
> Como o aplicativo Copilot é executado no seu próprio computador, e não em um codespace, a [lição de pré-requisitos][ex0] orienta você na instalação do Node.js e na criação da sua cópia do projeto antes de instalar o aplicativo.

> [!NOTE]
> Se você usa o Copilot Business ou o Copilot Enterprise, o administrador precisa manter habilitada a política **GitHub Copilot app**. Essa política é diferente da política do Copilot CLI.

## Comece

**[Comece pelos pré-requisitos →][ex0]**

[ex0]: 0-prerequisites/
[ex1]: 1-install-copilot-app/
[ex2]: 2-add-star-rating/
[ex3]: 3-agent-modes/
[ex4]: 4-custom-instructions/
[ex5]: 5-agent-skills/
[ex6]: 6-mcp-playwright/
[ex7]: 7-qa-agent/
[ex8]: 8-create-pull-request/
[ex9]: 9-canvases/
[ex10]: 10-review/
[install-git]: https://github.com/git-guides/install-git
[callout-student-plan-education]: https://github.com/education/students
