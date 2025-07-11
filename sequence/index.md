# シーケンス図・主要フロー

このディレクトリには、ロボット管理システムの主要な処理フローのシーケンス図を格納しています。

## 概要

システムの各機能における通信フローや処理の流れを、シーケンス図を用いて詳細に記述しています。これにより、フロントエンド、バックエンド、ロボット間の相互作用を明確に理解できます。

## 利用技術

- **GraphQL**: 管理者とフロントエンド間の効率的なデータ取得
- **gRPC over MQTT**: ロボットとの高性能・型安全な通信
- **AWS IoT Core**: MQTT メッセージングによる IoT デバイス通信

## シーケンス図一覧

### [ロボット指令の通信フロー](robot_command_flow.md)

管理者からロボットへの指令送信から、実行結果の返信までの詳細な通信フローを説明しています。

**主な内容：**

- GraphQL Mutation による指令送信
- gRPC over MQTT Proxy による通信中継
- エラーハンドリング
- 実装例（TypeScript）

**対象ユースケース：**

- UC2-1: ロボットに指令を送信する
- UC2-2: 指令実行結果を報告する
- UC2-3: 指令状況を確認する

## 今後追加予定

- エラー通知のシーケンス図
- 時系列データ収集のシーケンス図
- イベントログ管理のシーケンス図
- システム起動・停止のシーケンス図

## 参考資料

- [システム構成図](../architecture/index.md)
- [ユースケース図](../usecase/index.md)
