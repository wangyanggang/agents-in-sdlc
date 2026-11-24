---
title: "Lição 3 - Modos de agente: Plan e Autopilot"
description: "Explore os modos de agente: use Plan para definir uma abordagem, Autopilot para criar a filtragem a partir de uma issue e Interactive para revisar e verificar o resultado."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

Começamos adicionando uma pequena funcionalidade ao projeto. Mudanças maiores exigem um processo mais robusto. Felizmente, o aplicativo GitHub Copilot foi criado para trabalhar com o fluxo existente de uma organização e ajudar a desenvolver as funcionalidades certas da maneira certa. Esta é a primeira de várias lições em que você seguirá um processo típico de desenvolvimento orientado por agentes: começará com uma issue para gerar uma nova funcionalidade, garantirá que o código seja válido e que a funcionalidade se comporte como esperado e, por fim, fará o merge no projeto.

> [!NOTE]
> Você usará a mesma sessão durante todo o fluxo de trabalho da funcionalidade. Normalmente, você usaria sessões ou PRs diferentes para cada tipo de arquivo, mas vamos simplificar para nos concentrarmos nos conceitos principais.

Nesta lição, você vai:

- iniciar uma nova sessão de agente a partir de uma issue do GitHub;
- definir requisitos no modo **Plan**;
- implementar a funcionalidade no modo **Autopilot**;
- revisar o código;
- validar a funcionalidade manualmente em um canvas de navegador.

Ao continuar o trabalho nesta funcionalidade, você atualizará as instruções do repositório, personalizará a skill `quality-checks` existente, adicionará validação MCP, criará um agente de QA e abrirá o PR da funcionalidade.

## Cenário

O catálogo da Tailspin Toys está crescendo, e os visitantes precisam filtrar os jogos por categoria e publisher. A issue do backlog descreve a funcionalidade, mas é preciso chegar a um acordo sobre detalhes, como combinar categorias, antes de começar a programar. Você usará o modo Plan para decidir esses pontos e, depois, autorizará uma implementação com escopo definido no modo Autopilot.

## Contexto

Adicionar agentes de programação com IA ao fluxo de desenvolvimento não muda os fundamentos — na verdade, eles ficam ainda mais importantes. A maioria das pessoas desenvolvedoras segue um processo parecido com este:

1. Abrir uma issue registrada com os detalhes do trabalho.
2. Criar um plano do que precisa ser implementado.
3. Desenvolver e revisar o código.
4. Executar os testes para validar o código.
5. Validar manualmente a nova funcionalidade.
6. Criar um pull request (PR).
7. Depois que o código for revisado e o processo de integração contínua for concluído com sucesso, fazer o merge.

> [!NOTE]
> Os detalhes exatos variam de acordo com sua equipe e organização. No entanto, a maioria dos processos segue alguma variação do fluxo acima.

Seguir essa abordagem padrão ajuda a garantir que o código gerado por IA atenda aos requisitos e passe pelo mesmo processo de revisão aplicado ao código escrito manualmente.

## Modos de sessão

O **modo de sessão** controla o nível de autonomia do agente. Você pode defini-lo no menu suspenso abaixo do campo de prompt e alterá-lo a qualquer momento:

- **Interactive**: você e o agente trabalham em conjunto. O agente sugere mudanças e aguarda sua resposta antes de continuar.
- **Plan**: o agente cria um plano primeiro. Você revisa e aprova o plano antes que o agente o execute.
- **Autopilot**: o agente trabalha de forma totalmente autônoma, escrevendo código, executando testes e iterando sem aguardar sua resposta.

Comece no modo Plan, revise o plano e depois use o Autopilot para implementá-lo.

## Inicie uma sessão a partir da issue

Antes de começar, confirme que o PR da avaliação em estrelas foi mesclado e que seu `main` local está atualizado.

1. Em **Sessions**, na barra lateral, selecione a pasta do repositório Tailspin Toys e, em seguida, selecione **Issues** na navegação superior do repositório. Abra **Allow users to filter games by category and publisher**. Essa issue já foi criada para você; não é necessário criar outra.
2. Selecione **New session** e escolha uma **new working tree** baseada no `main` atualizado.

    ![Visualização da issue no aplicativo GitHub Copilot com uma seta apontando para o botão New session](../../../_images/app-new-session-from-issue.png)

3. Confirme se a issue foi anexada à sessão e selecione **Plan** no seletor de modo.

> [!NOTE]
> Se o Node.js ou o npm não forem encontrados, peça ao agente para executar `node --version` e `npm --version`. Se os comandos funcionarem no terminal, mas não na sessão, verifique o PATH do aplicativo ou a configuração do gerenciador de versões e feche o aplicativo completamente antes de abri-lo novamente. Tente de novo a operação e as verificações que falharam; não reinstale o npm apenas porque o agente não consegue encontrá-lo.

## Planeje a funcionalidade de filtragem

O planejamento permite revisar a abordagem antes de o Copilot escrever o código. Como você começou pela issue, o Copilot já tem a solicitação da funcionalidade como contexto. Envie:

```plaintext
Build this feature.
```

Responda às perguntas do Copilot e compare o plano com os critérios de aceitação da issue. Confirme se o plano inclui filtragem por categoria e publisher, controles acessíveis, mudanças de acesso a dados e testes. Converse sobre qualquer comportamento que não esteja claro, como a forma de combinar várias categorias ou o que acontece quando nenhum jogo corresponde.

O plano deve incluir lint, testes unitários, testes E2E e verificação de tipos usando as ferramentas existentes do projeto. Mantenha o escopo na implementação e nos testes da filtragem; você criará o PR depois de concluir o fluxo de qualidade. Peça mudanças no plano antes de aprová-lo e mantenha à mão a URL da issue e quaisquer esclarecimentos acordados para a validação posterior.

## Aprove o Autopilot explicitamente

Quando estiver satisfeito com o plano, selecione **Approve and implement this plan** ou a opção equivalente na sua versão. Confira o modo ativo em vez de presumir que a aprovação o alterou. Confirme que o indicador de modo mostra **Autopilot**.

O Copilot começará a trabalhar na implementação. Você verá que ele seguirá o plano de forma iterativa, gerando código e executando testes.

> [!NOTE]
> A aprovação pode iniciar a implementação imediatamente, portanto revise o plano primeiro. Se o Copilot informar que faltam dependências ou que há conflito de porta, resolva o problema de configuração antes de considerar as verificações concluídas. Interrompa somente os servidores que você iniciou.

## Revise e valide a implementação

Depois que o código for gerado, revise-o antes de fazer merge, como faria com qualquer outro código. Vamos revisar o código e executar o site para confirmar que tudo funciona.

1. Abra **Changes** e examine a implementação da filtragem e os testes.
2. Compare o resultado com a issue e com os esclarecimentos aprovados, incluindo combinações de várias categorias e publishers. Confirme se as mudanças seguem as instruções existentes do repositório.
3. Examine os resultados de lint, testes unitários, testes E2E e verificação de tipos. Uma verificação ignorada não conta como aprovação.
4. Resolva as falhas e execute novamente as verificações afetadas antes de aceitar a implementação. A configuração E2E do Playwright cria e disponibiliza uma pré-visualização e pode reutilizar um servidor local. Confirme que o servidor testado pertence a esta worktree, não a uma lição anterior.

## Explore a nova funcionalidade

O código parece correto, mas será que funciona? Vamos iniciar a aplicação como antes e abrir o site em um canvas de navegador.

1. Use o prompt a seguir para pedir ao Copilot que inicie a aplicação e abra a página no canvas de navegador:

    ```plaintext
    Start the app and open it in the browser canvas.
    ```

2. Em alguns instantes, a aplicação será iniciada e uma janela do navegador será aberta dentro do aplicativo Copilot.
3. Selecione uma categoria e confirme se os resultados correspondem a ela. Limpe o filtro e, depois, selecione um publisher e confirme se os resultados correspondem a ele.
4. Combine filtros de categoria e publisher e compare os resultados com a issue e o plano aprovado. Se várias categorias forem aceitas, verifique o comportamento combinado acordado.
5. Teste uma combinação sem jogos correspondentes e confira o estado vazio. Limpe ou redefina os filtros e confirme se a lista completa volta a aparecer.
6. Quando terminar, peça ao Copilot para parar o servidor de desenvolvimento iniciado para esta sessão:

    ```plaintext
    Stop the dev server and close the browser canvas.
    ```

## Mantenha esta sessão para as próximas lições

Ainda não crie nem faça merge do PR da filtragem. Mantenha esta sessão, worktree e branch para as Lições 4 a 8. Em seguida, você aplicará instruções personalizadas ao código de filtragem e adicionará melhorias à skill e ao perfil de QA antes de criar e fazer merge do PR combinado na Lição 8. Depois de parar o servidor de desenvolvimento, você pode deixar a sessão inativa e voltar a ela na próxima lição.

## Resumo e próximos passos

Você usou diferentes modos de agente para criar e revisar uma funcionalidade. Nesta lição, você:

- iniciou uma nova sessão de agente a partir de uma issue do GitHub;
- definiu requisitos no modo **Plan**;
- implementou a funcionalidade no modo **Autopilot**;
- revisou o código;
- validou a funcionalidade manualmente em um canvas de navegador.

Em seguida, vamos aprofundar como o código é gerado e garantir que ele siga as práticas documentadas [usando instruções personalizadas][next-lesson].

## Recursos

- [Trabalhar com sessões de agente no aplicativo GitHub Copilot][agent-sessions]

[next-lesson]: ../4-custom-instructions/
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
