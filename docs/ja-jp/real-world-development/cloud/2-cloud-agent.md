---
title: "演習 2 - GitHub Copilot cloud agent"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 前のレッスン: カスタム指示][previous-lesson] |
|:--|

多くの組織が技術的負債に悩んでいます。未解決のセキュリティ問題、更新が必要なレガシーコード、実装する時間がなくバックログに残り続ける機能のリクエストなどがあります。GitHub Copilot cloud agent は、コードの更新や機能の追加などを自律的に実行できます。作業が完了すると、人がレビューできるドラフトの PR を作成します。時間のかかる作業を任せることで、開発者はより大きな課題に集中できます。

この演習では、Copilot cloud agent で次のことを確認します。

- コード生成環境をカスタマイズする
- 操作を安全に行う
- スコープを明確にした issue の重要性
- issue を Copilot に割り当てる

## シナリオ

Tailspin Toys には、解消したい技術的負債があります。最初のサイトを開発した委託先は、ドキュメントを十分に作成しませんでした。まず、アプリケーション内のエクスポートされたすべての関数に TSDoc のドキュメントコメントを追加します。

また、デザインチームはゲームを見つけやすくしたいと考えています。各ゲームの詳細ページに同じカテゴリのゲームを表示し、利用者がほかのゲームも引き続き閲覧できるようにします。まずはユーザー受け入れテストで UX を試すための実装が必要です。現在は優先度の高い別の issue があるため、この機能は後回しになっています。

どちらも、優先順位が低くなりやすいタスクです。Copilot cloud agent に割り当てると、非同期に作業を進めてもらい、ほかの作業を続けた後で、結果をレビューできます。

## GitHub Copilot cloud agent について

[GitHub Copilot cloud agent](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent) は、人の開発者と同様に、バックグラウンドでタスクを実行できます。[GitHub issue を Copilot に割り当てる][assign-issue]方法など、複数の方法で作業を依頼できます。割り当てると、Copilot は進行状況を追跡するドラフトのプルリクエストを作成し、環境を準備して、タスクに取り組みます。作業中も完了後もセッションを確認できます。提案された解決策のレビュー準備ができると、プルリクエストで通知されます。

## 適切なスコープの指示が重要

GitHub Copilot に魔法はありません。考える作業を省略できるわけではありません。単純に見える操作でも、詳しく調べると複雑さがあります。[Copilot cloud agent に依頼するタスクのスコープ][cloud-agent-best-practices]を慎重に決めてください。AI ペアプログラマーとして扱い、段階を踏んで学び、試し、必要に応じて調整します。生成 AI が加わっても、ソフトウェア開発の基本は変わりません。

## このリポジトリのカスタム指示

前の演習では、カスタム指示とその役割を確認しました。カスタム指示を実際に使ったことがあれば、`.github/copilot-instructions.md` が機能することを確認できています。まだの場合は、cloud agent に作業を割り当てる前に、このリポジトリに含まれる指示ファイルを読み、後でその影響を確認できるようにしましょう。

リポジトリの GitHub Web UI、または起動済みの codespace で次のファイルを開きます。

- `.github/copilot-instructions.md` — TypeScript の規約と TSDoc のドキュメントコメントに関する **Code standards** セクションを確認します。
- `.github/instructions/unit-tests.instructions.md` — `applyTo` フロントマターが `**/*.test.ts` に適用されることを確認します。

次のセクションで `Code lacks documentation` issue を cloud agent に割り当てるとき、作成された PR に TSDoc コメント、TypeScript の規約、コメントヘッダーが反映されているか確認してください。後の演習で PR をレビューするときに、改めて注目します。

## Copilot cloud agent の開発環境を設定する

誰がコードを書く場合でも、通常は開発環境やセットアップスクリプトが必要です。タスクを Copilot に割り当てる場合も同様で、Copilot はソフトウェアエンジニアのように作業します。

Cloud agent は作業環境に [GitHub Actions][github-actions] を使います。`.github/workflows/copilot-setup-steps.yml` に設定する[専用のセットアップワークフロー][setup-workflow]を作成すると、作業前に必要な開発ツールと依存関係をインストールできます。学習をスムーズに進めるため、このラボでは事前に設定されています。単一 Astro アプリ用に Node.js、プロジェクト依存関係、E2E テスト用ブラウザー、マイグレーションとシードが済んだ SQLite データベースを利用できます。

```yaml
name: "Copilot Setup Steps"

# リポジトリの Actions タブからセットアップ手順をテストできます
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # 必要な手順に対して最低限の権限を設定します。Copilot には独自の操作用トークンが付与されます。
    permissions:
      # セットアップでリポジトリをクローンする場合 (たとえば依存関係をインストールする場合) は、`contents: read` 権限が必要です。クローンしない場合、セットアップ完了後に Copilot が自動でクローンします。
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # フロントエンド / アプリのセットアップ - Node.js (アプリ全体は Astro + Drizzle/libSQL)
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # ビルドとテストに必要なローカル SQLite データベースをマイグレーションしてシードします。
      - name: Set up the database
        run: npm run db:setup
```

一般的な GitHub ワークフローと同じですが、重要な点があります。

- `copilot-setup-steps` という 1 つのジョブがあり、Copilot が PR の作業を始める前に GitHub Actions で実行されます。
- `workflow_dispatch` トリガーが設定されているため、リポジトリの **Actions** タブから手動で実行できます。Copilot が実行するのを待たずに、正常に動作するかテストできます。

## ドキュメントを追加する

ドキュメントが重要なのは誰もが理解していますが、多くのプロジェクトでは情報が古かったり、ドキュメントが不足していたりします。このような技術的負債は放置されやすく、生産性を下げ、コードベースの保守や新しい開発者の受け入れを難しくします。Copilot はドキュメントの作成に役立つため、cloud agent に依頼するのに適したタスクです。バックグラウンドでドキュメントを作成してもらい、後の演習で結果をレビューします。

1. 新しいブラウザータブで github.com のリポジトリを開きます。
2. **Issues** タブを選択します。
3. **New issue** を選択します。
4. **Blank issue** を選択します。
5. **Title** に `Code lacks documentation` と入力します。
6. **Description** に次の内容を入力します。

    ```plaintext
    Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
    ```

7. **Create** を選択します。
8. 右側にある **Assign to Copilot** を選択して、割り当てダイアログを開きます。

  ![issue への Copilot の割り当て](../../../_images/shared-assign-copilot.png)

9. **Assign** を選択します。
10. **Pull Requests** タブを選択します。
11. 新しく作成された PR を開きます。タイトルは `[WIP]: Code lacks documentation` のようなものです。PR が一覧に表示されない場合は、少し待ってからブラウザーを更新します。
12. 数分後、Copilot が To Do リストを作成したことを確認できます。

> [!NOTE]
> Copilot の To Do リストが PR に表示されるまで、数分かかることがあります。Copilot は環境を作成し (前述のワークフローを実行します)、プロジェクトを分析して、問題に取り組む方法を決めています。

13. リストと、Copilot が実行するタスクを確認します。
14. PR のタイムラインを下にスクロールし、Copilot が issue の作業を開始したことを示す更新を確認します。
15. **View session** ボタンを選択します。

  ![Copilot のセッションビュー](../../../_images/ex4-view-session.png)

> [!CAUTION]
> 表示を更新しないと、状態の更新が表示されないことがあります。

16. ライブセッションをスクロールして、Copilot の作業を確認します。コードを調べて状態を理解し、計画を考えて、コードを作成する様子を確認できます。

完了まで数分かかることがあります。Copilot cloud agent の主な利点は、ほかの作業を続けている間にタスクを非同期で進められることです。この利点を活かすため、別のタスクも Copilot cloud agent に割り当ててから、アプリへの機能追加に取り組みましょう。

## ゲーム詳細ページに関連ゲームのセクションを追加する

Copilot cloud agent の大きな利点の 1 つは、作業を分担できることです。デザインチーム向けの関連ゲームの追加にそれほど時間がかからなくても、その時間を別の作業に使えます。Copilot cloud agent に割り当てましょう。

1. github.com のリポジトリに戻ります。
2. **Issues** タブを選択します。
3. **New issue** を選択します。
4. 空のテンプレートを使うため、**Blank issue** を選択します。
5. **Title** に `Show related games on the game details page` と入力します。
6. **Description** に次の内容を入力します。

    ```markdown
    We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
    ```

7. **Create** を選択して issue を作成します。
8. 右側にある **Assign to Copilot** を選択します。

  ![issue への Copilot の割り当て](../../../_images/shared-assign-copilot.png)

9. **Assign** を選択します。

少しすると、issue の最初のコメントに 👀 が表示され、Copilot が作業を開始したことを確認できます。

![issue で Copilot が作業中であることを示す目の絵文字](../../../_images/ex4-issue-eyes-emoji.png)

Copilot が 2 つ目の依頼に取り組んでいます。Copilot cloud agent はソフトウェアエンジニアと同じように作業するため、常に監視する必要はありません。完了後にレビューできます。次は、カスタムエージェントの作成と使用を確認します。

## まとめと次のステップ

このレッスンでは、[GitHub Copilot cloud agent][copilot-agents]を確認しました。cloud agent に issue を割り当てて、非同期に作業してもらえます。技術的負債の解消、新機能の作成、別のフレームワークからのコード移行などに利用できます。

次のことを確認しました。

- コード生成環境のカスタマイズ
- 操作を安全に行うこと
- スコープを明確にした issue の重要性
- issue の Copilot への割り当て

Copilot がバックグラウンドで作業している間に、次はカスタムエージェントを作成して使用します。[Copilot cloud agent は MCP サーバーも利用でき][cloud-agent-mcp]、前のモジュールで確認したカスタム指示にも対応しています。

## リソース

- [Copilot cloud agent について][copilot-agents]
- [GitHub issue を Copilot に割り当てる][assign-issue]
- [Copilot cloud agent のセットアップワークフローに関するベストプラクティス][cloud-agent-best-practices]

| [次のレッスン: カスタムエージェント →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
