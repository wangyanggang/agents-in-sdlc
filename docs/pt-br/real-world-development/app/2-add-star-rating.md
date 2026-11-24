---
title: "Lição 2 - Adicione avaliações em estrelas: uma melhoria rápida"
description: "Inicie sua primeira sessão de agente no aplicativo GitHub Copilot, faça uma pequena mudança nos cartões dos jogos e faça merge dela como seu primeiro pull request."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

Agora que você conheceu o espaço de trabalho e usou um chat rápido, é hora de iniciar uma **sessão de agente** e fazer sua primeira mudança no projeto. Ela será pequena: os dados dos jogos já incluem uma avaliação em estrelas, mas os cartões da página inicial ainda não a exibem. Você pedirá ao agente que mostre essa informação, revisará a mudança e fará o merge do seu primeiro pull request.

Nesta lição, você vai:

- iniciar uma sessão de agente e aprender como ela é estruturada;
- pedir ao agente que faça uma mudança pequena e focada no projeto;
- revisar a mudança na visualização de diff do espaço de trabalho;
- executar a aplicação localmente e confirmar a mudança no navegador;
- abrir e fazer merge do seu primeiro pull request.

## Cenário

Cada jogo da Tailspin Toys pode ter uma avaliação em estrelas, que já aparece na página de detalhes do jogo. No entanto, os cartões da página inicial mostram somente o título, a categoria, o publisher e a descrição. Como aquecimento, você pedirá ao agente que mostre a avaliação existente em cada cartão — uma mudança pequena e independente, perfeita para sua primeira sessão.

## Estrutura de uma sessão

Uma **sessão** é uma conversa com um agente executada em seu próprio espaço de trabalho isolado. Cada sessão recebe um **git worktree e um branch dedicados**, o que permite executar várias sessões ao mesmo tempo — uma adicionando uma funcionalidade, outra corrigindo um bug — sem que as mudanças entrem em conflito. Suas sessões aparecem agrupadas por repositório na barra lateral; selecione qualquer uma para acessá-la.

Em uma sessão, você verá três elementos: a **conversa** com o agente, a **atividade das ferramentas** enquanto ele explora e edita arquivos e a lista de **arquivos alterados** com seus diffs.

## Inicie uma sessão e solicite a mudança

Vamos iniciar uma nova sessão para explorar o projeto e implementar a funcionalidade. Durante a [configuração do aplicativo][prior-lesson], você adicionou o projeto pelo repositório do GitHub. Criaremos uma nova sessão para esse repositório e solicitaremos a mudança.

1. Volte ao aplicativo GitHub Copilot ou abra-o.
2. Selecione **+** na parte superior da barra lateral para iniciar uma sessão.
3. Selecione `tailspin-toys` como repositório.
4. Abaixo da caixa de prompt, escolha uma **new working tree** e o modo **Interactive**. Use este prompt para solicitar a mudança:

    ```plaintext
    Show each game's starRating out of 5 in the game cards on the list page. If the rating is null, show "No rating yet". Keep the card layout as it is, add tests, and run the relevant checks.
    ```

5. Pressione <kbd>Enter</kbd> para enviar o prompt ao Copilot.

O aplicativo Copilot começará criando um novo worktree, uma cópia isolada do projeto. Depois, explorará o projeto, localizará os arquivos que precisam ser atualizados para adicionar a funcionalidade e criará o código necessário. Você acabou de adicionar uma funcionalidade com o aplicativo Copilot!

## Revise o diff

Todas as mudanças geradas por IA devem ser revisadas antes do merge, mesmo as pequenas. Vamos examinar as mudanças diretamente no aplicativo Copilot.

1. No canto superior direito do aplicativo, selecione **Toggle review panel**. No painel que abrir, selecione **Changes** para ver os arquivos alterados e seus diffs.

    ![Barra de ferramentas superior do aplicativo GitHub Copilot com uma seta apontando para o botão Toggle review panel à direita de Create PR](../../../_images/app-2-review-panel.png)

2. Você verá código adicionado a `GameCard.astro`, o arquivo principal usado para exibir os detalhes do jogo. Deve ser semelhante ao exemplo a seguir: um pequeno bloco que mostra a avaliação quando ela existe e usa "No rating yet" quando `starRating` é `null`:

   ```astro
   {game.starRating !== null ? (
       <span class="text-xs font-medium px-2.5 py-0.5 rounded bg-amber-900/60 text-amber-300" data-testid="game-rating">
           ★ {game.starRating} / 5
       </span>
   ) : (
       <span class="text-xs font-medium text-slate-500" data-testid="game-rating-empty">
           No rating yet
       </span>
   )}
   ```

> [!NOTE]
> Como todas as ferramentas de IA generativa, o Copilot é probabilístico, não determinístico. O código exato pode variar em relação ao exemplo, mas deve ser relativamente semelhante.

## Confira as mudanças

Revise os resultados das verificações automatizadas do agente antes de abrir o navegador. Confirme se os testes cobrem um valor numérico de `starRating` e a alternativa para `null`. Um pré-requisito ausente ou uma verificação ignorada não conta como aprovação; revise qualquer solicitação de instalação antes de aprová-la.

Não basta ler o código e presumir que funciona. Vamos pedir ao Copilot para abrir o site e examinar a interface atualizada. Para isso, podemos pedir que ele inicie o site e o abra em um canvas de navegador.

> [!TIP]
> Um canvas é um widget interativo disponível dentro do próprio aplicativo Copilot. Você explorará canvases personalizados e até criará o seu mais adiante, mas, por enquanto, usaremos o canvas de navegador integrado.

1. Use o prompt a seguir para pedir ao Copilot que inicie a aplicação e abra a página no canvas de navegador:

    ```plaintext
    Start the app and open it in the browser canvas.
    ```

2. Em alguns instantes, a aplicação será iniciada e uma janela do navegador será aberta dentro do aplicativo Copilot.
3. Confirme se os cartões dos jogos avaliados mostram a nota de um total de cinco.
4. Quando terminar, peça ao Copilot que pare o servidor de desenvolvimento iniciado para esta sessão:

    ```plaintext
    Stop the dev server and close the browser canvas.
    ```

## Abra e faça merge do seu primeiro pull request

Você criou a funcionalidade. Agora, crie um pull request (PR) para fazer merge do novo código na base de código existente.

1. Selecione **Create PR** no canto superior direito.
2. Se solicitado, selecione **Sign in with your browser** e siga as instruções para se autenticar.
3. Se o Copilot explicar que a política do repositório exige uma issue correspondente antes de criar o PR, confirme que ele deve seguir esse processo.
4. O Copilot começará a criar o PR.
5. Selecione o indicador **PR** logo acima do chat para abrir o pull request no painel de revisão. Revise-o conforme necessário.
6. Quando estiver tudo pronto, selecione **Ready to merge**.
7. Na nova janela de diálogo, selecione **Merge pull request** para fazer merge do pull request.

## Resumo e próximos passos

Parabéns! Você publicou sua primeira mudança usando o aplicativo GitHub Copilot. Nesta lição, você:

- iniciou uma sessão de agente e aprendeu como as sessões são estruturadas;
- orientou o agente a fazer uma mudança pequena e focada nos cartões dos jogos;
- revisou a mudança na visualização de diff do espaço de trabalho;
- executou a aplicação localmente e confirmou a avaliação em estrelas no navegador;
- abriu o PR 1, revisou as verificações e fez o merge explicitamente.

Em seguida, você [começará pela issue de filtragem e usará os modos Plan e Autopilot][next-lesson] para criar uma funcionalidade maior.

## Recursos

- [Trabalhar com sessões de agente no aplicativo GitHub Copilot][agent-sessions]
- [Sobre o aplicativo GitHub Copilot][about-copilot-app]
- [Gerenciar issues e pull requests com o aplicativo GitHub Copilot][managing-issues-prs]

[prior-lesson]: ../1-install-copilot-app/#instale-e-configure-o-aplicativo-github-copilot
[next-lesson]: ../3-agent-modes/
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
[managing-issues-prs]: https://docs.github.com/copilot/how-tos/github-copilot-app/managing-issues-and-pull-requests
