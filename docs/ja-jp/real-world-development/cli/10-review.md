---
title: "レッスン 10 - 振り返りと次のステップ"
description: "Copilot CLI のワークフロー、2 つのプルリクエスト、再利用可能なカスタマイズ、参考資料を振り返ります。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

GitHub Copilot CLI を使い、Tailspin Toys の一連のワークフローに取り組みました。次のことを行いました。

- Codespace を準備し、Copilot CLI をインストールして、プロジェクトを確認し、登録済みのフィルター機能の issue を見つけました。
- 星評価を追加し、転送されたブラウザーで結果を確認して、最初のプルリクエスト (PR) を手動でマージしました。
- フィルター機能の issue から始め、Plan モードでアプローチを決め、Autopilot モードで構築して、Interactive モードでレビューしました。
- カスタム指示でエージェントを導き、既存の `quality-checks` スキルをカスタマイズして、ユニットテスト、lint、型チェックを実行しました。
- Playwright Model Context Protocol (MCP) サーバーを追加し、実際のブラウザーでフィルター機能を確認しました。
- quality assurance (QA) カスタムエージェントを作成して選択し、要件、カバレッジ、スキルの実行結果、ブラウザーの根拠を確認しました。
- フィルター機能の変更全体をレビューし、Agent Merge による PR のマージを許可しました。
- コンテキスト、モデル、共有、省略可能な cloud agent への委任に使うスラッシュコマンドを確認しました。

## 完了した作業

このワークショップでは、更新済みの `main` からそれぞれ独自のブランチを作成し、2 つの PR を完了しました。

1. **星評価:** 既存の `starRating` と、評価なしの状態をゲームカードに表示します。
2. **フィルター機能と品質向上のワークフロー:** フィルターを実装し、指示を更新して機能に適用し、`quality-checks` のレポートをカスタマイズし、QA プロファイルを作成して、関連するテストを追加します。

フィルター機能の計画から PR 作成まで、同じ会話とブランチを使いました。ワークショップを簡潔にするため、これらの変更を 1 つの PR にまとめました。

## 複数の方法で検証する

自動テスト、自分でのブラウザー確認、MCP を通じた Copilot のブラウザー操作という複数の方法でコードを確認しました。`quality-checks` スキルはユニットテスト、lint、型チェックを実行し、新しい形式で報告しました。QA はこれらの結果と、要件およびテストカバレッジのレビューをまとめて PR の確認を支援しました。

追加するテストでは、実際に不足している部分を補います。QA の実行でテストを追加する必要がないと判断される場合もあります。マージを許可する前にコードと根拠を確認し、変更後は影響する検証結果を更新してください。

## ベストプラクティス

Copilot に与えるコンテキストとツールが、作業結果を左右します。このワークショップでは、指示を更新し、スキルをカスタマイズし、QA プロファイルを作成して、MCP サーバーを設定しました。会話をまたいでカスタマイズを再利用し、チームのニーズに合わせて調整できます。指示は標準を設定し、スキルは反復可能なタスクを記述し、カスタムエージェントは専門的な役割を定義し、MCP サーバーは外部ツールに接続します。エージェントの要約だけでなく、実際の変更とツールの結果を確認してください。

タスクに応じて**モードとモデル**を選びます。構築の前にアプローチを考えるには **Plan**、範囲を絞った変更を自分で確認しながら進めるには **Interactive**、範囲が明確なタスクを任せるには **Autopilot** を使います。定型的な編集には高速なモデルを、複雑な作業にはより高性能なモデルを選びます。

インフラストラクチャと同じように、コンテキストも重要です。構築するもの、目的、方法を明確に説明すると、出力が大きく変わります。

## さらに試す

主要なワークフローを確認できました。ほかにも、次の CLI 機能を試せます。

- `/review` でコードレビューエージェントに変更を分析してもらう
- `/rubber-duck` で問題を整理し、別の視点を得る
- `/fleet` で独立したサブタスクを並行して調整する
- `/worktree` で別のタスクを分離する
- `/delegate` でタスクを Copilot cloud agent に送る

## 次のステップ

ツールの使い方を上達させるには、継続して使うことが一番です。製品コード、趣味のコード、長い間作りたいと思っていた小さなアプリなどで活用してください。チームと学んだ内容を共有し、ほかの人からも学びましょう。ドキュメントも確認してください。

ターミナルから Tailspin Toys を拡張する場合は、省略可能な [Foundry Backer Concierge シリーズ][foundry]に進んでください。別の環境での作業を比較するには、[VS Code ワークショップ][vscode]、[GitHub Copilot app ワークショップ][app]、[Copilot cloud agent ワークショップ][cloud]を確認してください。

## リソース

- [GitHub Copilot CLI について][about-cli]
- [Copilot CLI コマンドリファレンス][cli-reference]
- [Copilot CLI をカスタマイズする][customize-cli]
- [Copilot CLI でプルリクエストを管理する][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
