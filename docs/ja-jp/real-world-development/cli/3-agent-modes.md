---
title: "レッスン 3 - エージェントモード: Plan と Autopilot"
description: "Plan で進め方を決め、Autopilot で issue からフィルター機能を構築し、Interactive モードで結果をレビューします。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

まず、プロジェクトに小さな機能を追加しました。より大きな変更には、さらにしっかりしたプロセスが必要です。GitHub Copilot CLI は、組織の既存のワークフローに沿って、適切な方法で適切なものを構築できるよう設計されています。このレッスンから、エージェント主導の標準的な開発プロセスに沿って進めます。issue から新しい機能を作成し、コードが有効で、機能が期待どおりに動作することを確かめ、最終的にプロジェクトにマージします。

> [!NOTE]
> 機能の作業では、同じ会話とブランチを使い続けます。通常、ファイルの種類や作業ごとにブランチや PR を分けますが、ここでは主な概念に集中するため手順を簡略化します。

このレッスンでは、次の操作を行います。

- GitHub issue から Copilot の新しい会話を開始します。
- Plan モードで要件を決めます。
- Autopilot モードで新しい機能を実装します。
- コードをレビューします。
- 転送されたブラウザーで機能を手動で検証します。

この機能の作業を続けながら、リポジトリの指示を更新し、既存の `quality-checks` スキルをカスタマイズし、MCP による検証を追加して QA エージェントを作成し、機能の PR を作成します。

## シナリオ

Tailspin Toys のカタログが増え、利用者はカテゴリやパブリッシャーでゲームを絞り込む必要があります。バックログの issue には機能が記載されていますが、カテゴリを組み合わせるなど、コーディング前に合意が必要な詳細もあります。Plan モードで決定し、Autopilot には範囲を明確にした実装を許可します。

## 背景

AI コーディングエージェントを開発ワークフローに加えても、基本は変わりません。むしろ、より重要になります。多くの開発者は、次のような手順で作業します。

1. 作業内容を説明する issue から始めます。
2. 構築するものを計画します。
3. コードを構築してレビューします。
4. テストを実行してコードを検証します。
5. 新しい機能を手動で確認します。
6. プルリクエスト (PR) を作成します。
7. コードレビューと継続的インテグレーションが成功したら、コードをマージします。

> [!NOTE]
> 詳細はチームや組織によって異なりますが、多くは上記の流れに沿っています。

標準的な手順に沿うことで、AI が生成したコードが要件を満たし、手作業で書いたコードと同じレビューのプロセスを経ることを確認できます。

## 会話モード

**会話モード**は、エージェントにどの程度の自律性を与えるかを制御します。<kbd>Shift</kbd>+<kbd>Tab</kbd> でモードを切り替えます。

- **Interactive**: エージェントが変更を提案し、次に進む前に入力を待ちます。
- **Plan**: エージェントが最初に計画を作成し、プロジェクトファイルの編集はできません。
- **Autopilot**: エージェントが自律的にコードを書き、テストを実行し、タスクが完了するまで反復します。

まず Plan モードで計画をレビューし、その後 Autopilot で実装します。

## issue から始める

フィルター機能を始める前に Codespace に戻り、リポジトリとターミナルを準備します。

1. Codespace に戻ります。停止している場合は、再起動してから続けます。
2. 星評価の PR がマージされていることを確認します。
3. ターミナルが開いていない場合は、<kbd>Control</kbd>+<kbd>\`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux) を押します。
4. `main` を更新し、フィルター機能用のブランチを作成します。

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

5. Copilot CLI を起動します。

   ```bash
   copilot --yolo
   ```

6. <kbd>Tab</kbd> を 2 回押して **Issues** タブを開きます。
7. <kbd>A</kbd> を押してすべての issue を表示します。
8. 矢印キーで **Allow users to filter games by category and publisher** というタイトルの issue を選択します。
9. <kbd>C</kbd> を押して issue をプロンプトに追加し、**Session** タブに戻ります。

プロンプトの先頭に `#7` (または同様の番号) が表示されます。`#` を使うと、GitHub 上の issue やプルリクエスト (PR) をコンテキストに追加できます。

## フィルター機能を計画する

計画を立てると、機能を実装したりタスクを実行したりする前に、アプローチを決められます。複雑な作業では、時間をかけて計画を立てると効果的です。Plan モードに切り替えて、Copilot に計画を作成してもらいます。

1. <kbd>Shift</kbd>+<kbd>Tab</kbd> を押して Plan モードに切り替えます。プロンプトの下に **Plan** と表示されていることを確認します。
2. 前の手順で追加した issue の後に、次のプロンプトを入力します。

   ```plaintext
   Create a plan for implementing this feature.
   ```

Copilot はプロジェクトを調べ、適切な方法を判断して計画を作成します。

3. フィルターの動作について質問された場合は、好みに応じて回答します。正解は 1 つではありません。
4. 計画が完成したら、<kbd>Control</kbd>+<kbd>E</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>E</kbd> (Windows/Linux) を押して展開します。
5. 計画全体を確認します。
6. 自分の決定と合わない部分があれば、Copilot に修正を依頼します。

## Autopilot を承認する

計画を作成してレビューできたので、実装に進みます。Autopilot モードで Copilot に作業を任せます。

Autopilot では、Copilot が問題を反復的に処理し、完了したと判断するまで作業を続けます。

1. **Accept plan and build on autopilot (recommended)**、またはインストール済みのバージョンにある同様のオプションを選択します。
2. プロンプトの下に **Autopilot** と表示されていることを確認します。
3. Copilot が計画に沿って反復し、コードを生成してテストを実行する様子を確認します。

> [!NOTE]
> 承認すると、すぐに実装が始まることがあります。必ず計画を先にレビューしてください。依存関係が不足している、またはポートが競合していると報告された場合は、セットアップの問題を解決してからチェック結果を確認してください。

## 実装をレビューして検証する

ほかのコードと同じように、生成されたコードもマージ前にレビューします。コードを確認し、サイトを実行して問題がないか確認しましょう。

1. <kbd>Shift</kbd>+<kbd>Tab</kbd> を押して Interactive モードに切り替えます。モード表示に **Plan** や **Autopilot** がないことを確認します。
2. `/diff` を入力し、フィルター機能とテストを確認します。
3. 結果を issue および計画で決めた内容と比較します。
4. レビューが終わったら <kbd>Esc</kbd> を押して差分表示を閉じます。
5. プロジェクトのチェック結果を確認し、失敗があれば修正を依頼します。

## 新しい機能を試す

コードがよさそうでも、実際に動くか確認しましょう。前と同じようにアプリを起動し、Codespaces の転送ポートからサイトを開きます。

1. Copilot にアプリの起動を依頼します。

   ```plaintext
   Start the app so I can try the filtering feature in my browser. Tell me the URL and leave the server running.
   ```

2. Codespaces でポート `4321` が利用可能と表示されたら、**Open in Browser** を選択します。
3. カテゴリ、パブリッシャー、計画で決めた組み合わせを試します。
4. リセットと結果が空の場合の動作が、issue と合意内容に一致することを確認します。
5. Codespace に戻り、起動した開発サーバーを停止するよう Copilot に依頼します。

## まとめと次のステップ

異なる会話モードを使い、機能を構築してレビューしました。このレッスンでは、次の操作を行いました。

- GitHub issue から Copilot の新しい会話を開始しました。
- Plan モードで要件を決めました。
- Autopilot モードで機能を実装しました。
- コードをレビューしました。
- 転送されたブラウザーで機能を手動で検証しました。

次は、[カスタム指示を使って][next-lesson]コード生成の動作をさらに確認し、文書化された慣行に従うようにします。

## リソース

- [GitHub Copilot CLI の Autopilot][autopilot]
- [Copilot CLI コマンドリファレンス][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
