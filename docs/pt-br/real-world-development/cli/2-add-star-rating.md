---
title: "Lição 2 - Adicione avaliações em estrelas: uma melhoria rápida"
description: "Use o Copilot CLI para fazer uma pequena mudança nos cartões de jogos, revise-a em um navegador encaminhado e faça merge do seu primeiro pull request."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Agora que você instalou o Copilot CLI e experimentou uma conversa, é hora de fazer sua primeira mudança no projeto. Ela será pequena: os dados dos jogos já incluem uma avaliação em estrelas, mas os cartões da página inicial ainda não a exibem. Você pedirá ao agente que mostre essa informação, revisará a mudança e fará o merge do seu primeiro pull request.

Nesta lição, você vai:

- iniciar uma conversa focada com o Copilot em um branch de funcionalidade;
- pedir ao agente que faça uma pequena mudança no projeto;
- revisar a mudança com `/diff`;
- executar a aplicação e confirmar a mudança em um navegador encaminhado;
- abrir e fazer merge do seu primeiro pull request.

## Cenário

Cada jogo da Tailspin Toys pode ter uma avaliação em estrelas, que já aparece na página de detalhes do jogo. No entanto, os cartões da página inicial exibem somente o título, a categoria, o publisher e a descrição. Como aquecimento, você pedirá ao agente que mostre a avaliação existente em cada cartão: uma mudança pequena, independente e perfeita para sua primeira sessão.

## Estrutura de uma conversa

Uma **conversa** é onde você trabalha com o Copilot CLI em uma tarefa. Diferentemente do aplicativo Copilot, uma conversa normal da CLI usa o repositório e o branch atualmente selecionados no terminal, em vez de criar uma worktree dedicada. As conversas salvas permitem retomar a mesma discussão mais tarde, enquanto os arquivos e o branch continuam como estado normal do Git no disco.

Em uma conversa, você verá três coisas: seus prompts e as respostas do agente, a atividade das ferramentas enquanto o agente explora e edita arquivos e as mudanças que podem ser examinadas com `/diff`.

## Inicie uma conversa e solicite a mudança

Vamos iniciar uma nova conversa para implementar a funcionalidade.

1. Volte ao Codespace.
2. Se o terminal ainda não estiver aberto, pressione <kbd>Control</kbd>+<kbd>`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
3. Se o Copilot ainda não estiver em execução, use este comando para iniciá-lo:

   ```bash
   copilot --yolo
   ```

4. Inicie uma nova sessão usando o comando slash `/new` e pressionando <kbd>Enter</kbd>.
5. Envie o prompt a seguir para solicitar a mudança:

   ```plaintext
   Show each game's starRating out of 5 in the game cards on the list page. If the rating is null, show "No rating yet". Keep the card layout as it is, add tests, and run the relevant checks.
   ```

O Copilot explorará o projeto, localizará os arquivos usados para exibir os detalhes dos jogos e criará o código necessário. Você acabou de adicionar uma funcionalidade com o Copilot CLI!

## Revise o diff

Todas as mudanças geradas por IA devem ser revisadas antes do merge, mesmo as pequenas. Vamos examinar as mudanças diretamente no Copilot CLI.

1. Digite `/diff` e examine todos os arquivos alterados.
2. Confirme se o cartão do jogo mostra a avaliação numérica quando ela está disponível e `No rating yet` quando `starRating` é `null`.
3. Confirme se os testes cobrem os dois casos.
4. Revise os resultados das verificações executadas pelo Copilot e peça que ele corrija eventuais falhas.
5. Quando terminar a revisão, pressione <kbd>Esc</kbd> para sair da tela de diff.

> [!NOTE]
> Como todas as ferramentas de IA generativa, o Copilot é probabilístico, não determinístico. O código exato pode variar. Revise o comportamento em vez de esperar uma implementação idêntica.

## Confira as mudanças

Não basta ler o código e presumir que funciona. Vamos pedir ao Copilot para iniciar o site e examinar a interface atualizada em um navegador encaminhado pelo Codespaces.

1. Peça ao Copilot para iniciar a aplicação:

   ```plaintext
   Start the app so I can inspect the star-rating change in my browser. Tell me the URL and leave the server running.
   ```

2. Quando o Codespaces informar que a porta `4321` está disponível, selecione **Open in Browser**.
3. Confirme se os cartões dos jogos mostram as avaliações de zero a cinco.
4. Volte ao Copilot e peça que pare o servidor iniciado:

   ```plaintext
   Stop the development server you started.
   ```

## Abra e faça merge do seu primeiro pull request

Você criou a funcionalidade. Agora, crie um pull request (PR) para fazer merge do novo código no projeto.

1. Peça ao agente padrão para fazer commit da mudança:

   ```plaintext
   Commit the reviewed star-rating changes with an appropriate commit message.
   ```

2. Digite `/pr create`. Ao criar o PR, o Copilot CLI envia o commit existente e mostra a URL do PR.
3. Abra o PR mantendo <kbd>Command</kbd> pressionado (Mac) ou <kbd>Ctrl</kbd> (Windows/Linux) e selecionando a URL exibida pelo Copilot CLI.
4. Revise os arquivos alterados e as verificações.
5. Quando estiver tudo pronto, selecione **Merge pull request** e confirme o merge.
6. Volte ao Codespace e saia do Copilot CLI com `/exit`.
7. Atualize seu `main` local:

   ```bash
   git checkout main
   git pull
   ```

## Resumo e próximos passos

Parabéns! Você publicou sua primeira mudança usando o GitHub Copilot CLI. Nesta lição, você:

- iniciou uma conversa focada com o Copilot em um branch de funcionalidade;
- orientou o agente a fazer uma pequena mudança nos cartões dos jogos;
- revisou a mudança com `/diff`;
- executou a aplicação e confirmou a avaliação em estrelas em um navegador encaminhado;
- abriu e fez merge do seu primeiro pull request.

Em seguida, você [começará pela issue de filtragem e usará os modos Plan e Autopilot][next-lesson] para criar uma funcionalidade maior.

## Recursos

- [Sobre o GitHub Copilot CLI][about-copilot-cli]
- [Referência de comandos do Copilot CLI][cli-reference]

[previous-lesson]: ../1-install-copilot-cli/
[next-lesson]: ../3-agent-modes/
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
