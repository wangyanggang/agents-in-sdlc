---
title: "レッスン 1 - GitHub Copilot app をインストールする"
description: "GitHub Copilot app をインストールし、テンプレートから作成したリポジトリを接続して、ワークスペースを確認し、クイックチャットを試します。"
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

[**GitHub Copilot app**][about-copilot-app] は、エージェント主導の開発に使うデスクトップアプリケーションです。GitHub Copilot CLI を基盤として GitHub とネイティブに統合されているため、リポジトリ、ブランチ、CI パイプラインをすぐに利用できます。複数のエージェントを、それぞれ独立したワークスペースで並行して動かし、作業を指示して繰り返しタスクを自動化するワークフローに適しています。Node.js のインストールとプロジェクトのコピーが完了したので、アプリをインストールしてリポジトリを接続します。

このレッスンでは、次の操作を行います。

- GitHub Copilot app をインストールしてサインインします。
- GitHub リポジトリからプロジェクトをアプリに追加します。
- テンプレートによって用意されたバックログを含め、ワークスペースを確認します。
- クイックチャットを試して、アプリについて質問します。

## シナリオ

チームは、増え続けるバックログに対応するため、AI エージェントを導入しています。Copilot app では、Issue の選択、エージェントの実行、変更のレビュー、プルリクエストのマージを一か所から指示できます。このレッスンでは、アプリをインストールして接続し、プロジェクトについての会話を始められるようにします。

> [!NOTE]
> 対象となる Copilot プランが必要です。Copilot Free、Copilot Student、または有料プラン (Pro、Pro+、Business、Enterprise) を利用してください。Copilot Business または Copilot Enterprise を使用している場合、管理者が **GitHub Copilot app** ポリシーを有効にしておく必要があります。

## GitHub Copilot app をインストールして構成する

GitHub Copilot app を使用するには、まずアプリをインストールします。Windows、macOS、Linux 向けのバージョンが用意されています。アプリをインストールして認証し、Tailspin Toys リポジトリを追加しましょう。

1. ブラウザーで [GitHub Copilot app のランディングページ][download-app]を開きます。
2. 使用しているプラットフォーム向けのアプリをダウンロードし、ページの手順に従ってインストールします。
3. インストール後、アプリを開きます。
4. **Sign in to GitHub** を選択し、GitHub.com または GHE.com アカウントでサインインします。データ所在地に対応した GitHub Enterprise Cloud を使用している場合は **GitHub Enterprise Cloud** を選択し、求められたら `*.ghe.com` のホスト名を入力します。

   GitHub Enterprise Server を使用している場合は、まずクラウドアカウントでオンボーディングを完了します。その後、**Settings** を開き、**Accounts**、**Add account**、**GitHub Enterprise Server** の順に選択します。[Enterprise Server のサインインガイド][ghes-sign-in]に従って、ブラウザーでアプリを認証します。

5. オンボーディング中にリポジトリを選択する画面が表示された場合は、テンプレートから作成した Tailspin Toys リポジトリを選択します。リポジトリの選択をスキップし、オンボーディング後に追加することもできます。
6. テーマを選択するよう求められたら選び、オンボーディングを完了します。
7. サイドバーの **Sessions** でリポジトリを探します。すでに一覧にある場合は、再度追加する必要はありません。
8. まだ接続されていない場合は、**Sessions** の横にある **+** を選択して新しいセッションを作成し、**Add GitHub repository** を選択します。前提条件のレッスンで控えた所有者名とリポジトリ名を入力します。
9. サイドバーにリポジトリが表示されていることを確認します。このレッスンで使うレイアウトでは、`tailspin-toys` などのリポジトリフォルダーが **Sessions** の下にまとまり、各リポジトリの下に個々のセッションが表示されます。

## ワークスペースを確認する

プロジェクトを接続したら、各領域を確認しましょう。サイドバーには次の領域があります。

- **New** - Copilot との新しいチャットセッションを開始します。
- **Pull requests** - アプリの GitHub ネイティブ統合を使ってプルリクエストを参照および絞り込み、CI 状態を確認し、レビューします。アプリを離れる必要はありません。
- **Issues** - Issue を参照および絞り込み、Issue からセッションを開始します。
- **Automations** — スケジュールまたはオンデマンドで実行する、保存済みのエージェントタスクです。To Do リストの管理、定期的なプロジェクト保守、その他の面倒な作業を任せるのに役立ちます。振り返りでは次のステップとして紹介し、別の演習にはしません。
- **Customize** - MCP サーバー、プラグイン、スキルなどを Copilot app に追加します。Playwright MCP の設定で使用します。
- **Chats** — 独自のブランチやワークスペースを必要としない、質問やブレインストーミング向けの軽い会話です。最初のチャットを開始した後に表示されます。表示されていない場合は、**Sessions** の横にある **+** を選択して最初のチャットを開始します。
- **Sessions** — リポジトリフォルダーと、その中のエージェントセッションをまとめます。`tailspin-toys` などのリポジトリ名を選択するとリポジトリのビューが開き、その下のセッションを選択すると会話に戻ります。セッションはそれぞれ独立したワークスペースで実行され、変更が競合せずに複数のセッションを同時に実行できます。星評価を追加するレッスンで最初のセッションを開始します。

ワークショップを進めながら、ワークスペースを確認していきます。

> [!TIP]
> 迷ったときは Copilot に質問しましょう。操作方法がわからない場合や、何かが可能かどうか知りたい場合は、Copilot に尋ねると案内してくれます。

### 用意されたバックログを確認する

バックログのないプロジェクトはほとんどなく、Tailspin Toys も例外ではありません。テンプレートからリポジトリを作成したときに用意されたバックログを確認しましょう。

1. サイドバーの **Sessions** で、個別のセッションではなく Tailspin Toys のリポジトリフォルダーを選択します。次に、リポジトリの上部ナビゲーションで **Issues** を選択します。
2. Issue 番号を決めつけず、次のタイトルを探します。

   - Allow users to filter games by category and publisher
   - Update our repository coding standards

3. Issue を選択して詳細を読みます。各 Issue はエージェントセッションの開始点にもなります。最初の小さな変更を完了した後、フィルター機能の Issue から作業を開始します。

> [!NOTE]
> **Issues** と **Pull requests** の一覧は自動的に絞り込まれ、Copilot app に追加したリポジトリの項目だけが表示されます。ほかのリポジトリの作業項目を確認するには、そのリポジトリもアプリに追加してください。

## クイックチャットを試す

アプリ自体について質問すると、アプリに慣れることができます。その用途には **quick chat** が適しています。Quick chat ではブランチや worktree を作成せずに質問やブレインストーミングができます。セッションを必要としない、その場限りの質問に最適です。

1. サイドバーの **Chats** の横にある **+** を選択して、新しいチャットを開きます。**Chats** がまだ表示されない場合は、**Sessions** の横にある **+** を選択して最初のチャットを開始します。チャットの開始後に **Chats** が表示されます。
2. アプリのセッションがどのように動作するかを尋ねます。

   ```plaintext
   How does the GitHub Copilot app use worktrees?
   ```

3. 会話ビューで回答を読みます。各セッションが独立した git worktree で実行されるため、変更が競合せずに複数のエージェントを並行して動かせることがわかります。会話はいつでも続けられ、新しいチャットも開始できます。

## まとめと次のステップ

GitHub Copilot app をインストールし、プロジェクトを接続して、ワークスペースを確認しました。次の操作を学びました。

- アプリをインストールして GitHub にサインインする
- GitHub リポジトリからプロジェクトを追加する
- ワークスペースを確認し、**Issues** でバックログを見つける
- クイックチャットで、その場限りの質問をする

次は[最初のエージェントセッションを開始し][next-lesson]、ゲームカードに星評価を表示します。

## リソース

- [GitHub Copilot app について][about-copilot-app]
- [GitHub Copilot app の概要][getting-started]
- [GitHub Copilot app でエージェントセッションを操作する][agent-sessions]

[next-lesson]: ../2-add-star-rating/
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
[getting-started]: https://docs.github.com/copilot/how-tos/github-copilot-app/getting-started
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
[download-app]: https://gh.io/app
[ghes-sign-in]: https://docs.github.com/enterprise-server@3.22/copilot/copilot-on-ghes/sign-in-on-copilot-app
