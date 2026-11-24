---
title: "演習 4 - エージェントの監視と管理"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

前の 2 つの演習では、ユーザー体験の改善と機能追加を目的とする 3 つのタスクを Copilot cloud agent に依頼しました。cloud agent は非同期かつ自律的に作業しますが、タスクの進行状況を監視することも重要です。

cloud agent に割り当てたタスクは、GitHub.com の[エージェントページ][agents-page]など、さまざまなツールで管理できます。このミッションコントロールでは、オープンなプルリクエストがあるすべてのエージェントタスクを確認できます。実行内容を調べたり、進行中のセッションに追加の指示を送ったりできます。

このレッスンでは、次の操作を行います。

- エージェントページで cloud agent のタスクを監視します。
- 進行中のセッションに追加の機能を依頼します。

## シナリオ

エージェントにハイコントラストモードを依頼した後、チームはライトモードも追加するよい機会だと考えました。サイトのスタイルと切り替え機能を更新しているため、ハイコントラストに加えてライトモードも実装するよう、エージェントに追加の指示を送ります。

## Copilot cloud agent のタスクを確認する

Copilot cloud agent に割り当てたタスクの現在の状況を確認しましょう。

1. [Copilot agents ページ](https://github.com/copilot/agents)を開きます。
2. メインペインと左ペインのタスクリストを確認します。Copilot に割り当てたタスクが表示されます。次のようなタスクが含まれます。
   - コードベースのドキュメントの更新
   - ゲームを変更する API の生成
   - Web サイトへのハイコントラストモードの追加
3. 実行中のタスクを 1 つ選択し、Copilot が実行した作業を確認します。次のような作業が表示されます。
   - リポジトリのチェックアウト
   - Copilot の作業環境の作成
   - MCP サーバーの設定
   - 割り当てられたタスクを完了するための各種作業

> [!NOTE]
> 表示される手順は、Copilot の作業状況や実施方法によって異なります。

4. 右側に表示されるプルリクエスト (PR) ペインも確認してください。PR と変更されたファイルが表示され、進行状況をさらに監視できます。

## cloud agent に追加の指示を送る

実行中のタスクを確認できたので、ハイコントラストモードの作業中にライトモードの切り替えも追加するよう Copilot に依頼します。

1. ハイコントラストモードの追加に関するセッションを選択します。タイトルは、Copilot が付けた名前や作業状況によって異なります。

    ![ミッションコントロール内のアクセシビリティセッション](../../../_images/ex6-accessibility-session.png)

2. セットアップが完了して作業が始まるまで、セッションを数分間確認します。作業開始後は、次の画面のようなメッセージが表示されます。
3. **Steer active session while Copilot is working** ダイアログに次のプロンプトを入力します。

    ```plaintext
    While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
    ```

    ![エージェントページで、Steer active session while Copilot is working ダイアログが強調表示された cloud agent タスク](../../../_images/ex6-steer-cloud-agent-task.png)

4. <kbd>Enter</kbd> を押してプロンプトを送信します。
5. Copilot がプロンプトを受け取り、作業に取り込む様子を確認します。

## Copilot に作業を任せる

Copilot は更新されたタスクに取り組みます。メッセージを送信した時点で実行中だった手順を終えた後、新しい依頼を作業に反映します。

作業には数分かかります。その間に、ここまでに学んだことを振り返りましょう。

## まとめと次のステップ

このレッスンでは、Copilot cloud agent のタスクを監視し、案内する中心的な場所である Copilot agents ページを確認しました。このミッションコントロールで、進行中および完了したタスクを追跡し、実行中の作業をレビューし、必要に応じて進行中のタスクを変更できます。

次のことを確認しました。

- ミッションコントロールとエージェントページで cloud agent のタスクを監視する
- 進行中のセッションに追加機能を依頼する

Copilot がアクセシビリティ機能を実装している間に、Copilot が作成した[プルリクエストを改善する][next-lesson]方法を確認しましょう。

## リソース

- [Copilot agents ページ][agents-page]
- [カスタムエージェントについて][custom-agents]

---

| [← 前のレッスン: カスタムエージェント][previous-lesson] | [次のレッスン: Copilot の作業を改善する →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
