---
title: "レッスン 8 - 機能の PR を作成してマージする"
description: "フィルター機能、指示、スキルの更新、QA プロファイル、テストをまとめてレビューし、Agent Merge を使って PR を作成します。"
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

フィルター機能の実装、指示の更新、スキルの更新、quality assurance (QA) プロファイル、テストはすべて 1 つのブランチに保存されています。これらをまとめてレビューし、プルリクエストを作成します。星評価のプルリクエスト (PR) は自分でマージしました。今回は **Agent Merge** にプロセスを管理してもらいます。

> [!NOTE]
> 通常は、機能、指示、スキル、QA エージェントの変更を複数の PR に分けます。ワークショップを簡潔にするため、フィルター機能と品質向上のワークフロー全体を 1 つのセッションとブランチで進め、この PR にまとめました。

このレッスンでは、次の操作を行います。

- Agent Merge と、マージまでのライフサイクルを自動化する方法を学びます。
- 機能 PR の全体と検証の根拠を確認します。
- レビュー後にのみ Agent Merge に許可を与え、PR がマージされたことを確認します。

## シナリオ

フィルター機能のワークフローでは、Copilot を使って機能を計画、実装、検証しました。Tailspin Toys では、マージの許可を開発者が管理しながら、PR の残りの作業を自動化したいと考えています。

## Agent Merge について

**Agent Merge** は、GitHub Copilot app でプルリクエストをマージするために必要な残りの作業を自動化します。有効にすると、アプリのセッションがプルリクエストを確認し、CI チェックの失敗、レビューコメント、必要なリベースなど、マージを妨げているものに対処します。GitHub が許可すると、Copilot が PR をマージします。バックグラウンドで実行され、アプリを再起動しても継続し、PR がマージされると自動的に停止します。

これまでは自分で **Merge pull request** を選択しました。Agent Merge に任せることもできますが、コードの編集やマージには、引き続き明示的な許可が必要です。マージを許可する前に、許可する操作と作業内容をレビューしてください。

## Agent Merge で PR を管理する

コードの作成とレビューが完了したので、Agent Merge に PR のプロセスを管理させます。

1. エージェントピッカーで **Default agent** を選択します。
2. **Create PR** の横にあるドロップダウンを選択します。
3. **Agent Merge** を選択します。ボタンが **Agent Merge** に変わります。
4. **Agent Merge** ボタンを選択してプロセスを開始します。ドロップダウンの項目を選ぶだけでは開始されません。

Agent Merge のプロセスが始まり、次の作業を行います。

- タイトルと説明を付けてプルリクエストを作成します。
- Issue からセッションを開始した場合は、説明本文で関連する Issue を参照します。
- ターゲットブランチにリベースするか、マージ競合に対処します。
- CI を監視し、すべてのチェックが成功することを確認します。
- 他の開発者や Copilot code review からのフィードバックを確認し、コメントを解決するための変更を加えます。
- すべてのチェックが成功したら、必要に応じて PR を自動的にマージします。

すべてのチェックが成功した後、Agent Merge が PR をマージできるようにします。

5. マージを許可する前に、PR の差分と検証の根拠をレビューします。
6. **Agent Merge** の横にあるドロップダウンを選択します。
7. **Merge pull request** の横にチェックが付いていることを確認します。
8. 次のプロンプトで、エージェントに明示的にマージを依頼します。

    ```plaintext
    Merge the PR once all required checks and approvals pass. Do not bypass repository protections.
    ```

9. 進行状況を確認し、報告された問題を解決します。続行前に PR の状態が **Merged** になっていることを確認してください。マージ許可が有効になっていることや、エージェントが動作中であることだけでは、マージ完了の確認になりません。

> [!IMPORTANT]
> Agent Merge は、リポジトリの保護や権限不足を回避しません。続行前に、それらの問題を解決してください。

## まとめと次のステップ

コードの生成、テストと検証、プルリクエストのプロセスなど、開発プロセスの複数の部分を自動化しました。このレッスンでは、次の操作を行いました。

- Agent Merge と、マージまでのライフサイクルを自動化する方法を学びました。
- 機能 PR の全体と検証の根拠を確認しました。
- レビュー後に Agent Merge に許可を与え、PR がマージされたことを確認しました。

次は[既存のキャンバスを使い、トリアージキャンバスを作成して][next-lesson]、エージェントと一緒に作業を確認、計画、視覚化する方法を学びます。

## リソース

- [GitHub Copilot app で Issue とプルリクエストを管理する][managing-issues-prs]
- [GitHub Copilot app について][about-copilot-app]

[next-lesson]: ../9-canvases/
[managing-issues-prs]: https://docs.github.com/copilot/how-tos/github-copilot-app/managing-issues-and-pull-requests
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
