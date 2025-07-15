**[← 概要・全体構成に戻る](./index.md)**

## サーバーインスタンス構成

ロボット管理システムは、**GraphQL API サーバー**と **gRPC over MQTT Proxy** を中心とした効率的でスケーラブルなアーキテクチャを採用。

## アーキテクチャ図

```mermaid
graph TD
    Admin[管理者/フロントエンド]
    Robot[ロボット]

    subgraph AWS
        DynamoDB[DynamoDB （構造化データ）]
        Timestream[Timestream （時系列データ）]
        IoTCore[AWS IoT Core （MQTTブローカー）]
        SNS[SNS（通知）]
        APIGateway[API Gateway （HTTP API）]
        Cognito[Cognito（認証）]

        subgraph LambdaCluster
            LambdaAPI[Lambda（API処理）]
            LambdaIoT[Lambda（IoT操作専用）]
            LambdaResponse[Lambda（ロボット応答処理）]
        end

        subgraph CloudWatch
            ErrorAlarm[エラーアラーム]
            LogGroup[CloudWatch Logs]
        end
    end

    %% 管理者との通信（認証付きAPI Gateway）
    Admin -->|認証付きHTTPS| Cognito
    Cognito -->|認証連携| APIGateway
    APIGateway --> LambdaAPI

    %% LambdaAPIがDB操作
    LambdaAPI -- データ取得/登録 --> DynamoDB
    LambdaAPI -- 時系列データ参照 --> Timestream

    %% LambdaIoTがIoT Core操作
    LambdaAPI -- 指令・制御リクエスト --> LambdaIoT
    LambdaIoT -- MQTT Publish --> IoTCore

    %% ロボットとのMQTT双方向通信
    Robot <-- MQTT-コマンド --> IoTCore
    Robot --> IoTCore

    %% IoT Coreからの応答トリガー
    IoTCore -- MQTTルール --> LambdaResponse
    LambdaResponse -- 結果記録 --> DynamoDB
    LambdaResponse -- ログ保存 --> Timestream

    %% CloudWatch監視・ログ集約
    LambdaAPI -- ログ/メトリクス --> LogGroup
    LambdaIoT -- ログ/メトリクス --> LogGroup
    LambdaResponse -- ログ/メトリクス --> LogGroup
    LogGroup -- エラーログ監視 --> ErrorAlarm
    ErrorAlarm -- アラート --> SNS
    SNS -- 通知 --> Slack[Slack]

    %% 補足: IP制限やWAFはAPI Gatewayの付帯機能として想定


```

## アーキテクチャの特徴

### 主要コンポーネント

- **GraphQL API サーバー**: 管理者向けの効率的なデータ取得・操作
- **gRPC over MQTT Proxy**: ロボットとの高性能・型安全な通信
- **AWS IoT Core**: MQTT メッセージングによる IoT デバイス通信
- **DynamoDB**: 指令・状態・エラー情報の永続化
- **Timestream**: 時系列データの効率的な保存・分析

## 主な利点

### 1. **GraphQL API サーバー**

- **効率的なデータ取得**: 必要なデータのみを 1 回のリクエストで取得可能
- **型安全性**: GraphQL スキーマによる強力な型チェック
- **リアルタイム通信**: GraphQL Subscriptions で WebSocket 経由のリアルタイム更新
- **フロントエンド開発効率**: 柔軟なクエリ構造でフロントエンド開発が効率化

### 2. **gRPC over MQTT Proxy**
- **高性能通信**: gRPC の効率的なシリアライゼーション（Protocol Buffers）
- **型安全性**: 強力な型定義とコード生成
- **双方向通信**: ストリーミング対応でリアルタイム制御が可能
- **既存 MQTT インフラ活用**: AWS IoT Core の既存インフラを活用

### 3. **アーキテクチャ**

- **スケーラビリティ**: GraphQL と gRPC の両方が水平スケーリングに適している
- **開発効率**: 型安全性とコード生成による開発効率向上
- **運用性**: 明確な責任分離とモニタリング

## 実装上の考慮点

### GraphQL サーバー

- **Apollo Server** または **GraphQL Yoga** の使用
- **Dataloader** による N+1 問題の解決
- **GraphQL Subscriptions** でリアルタイム更新

### gRPC over MQTT Proxy

- **Protocol Buffers** による効率的なシリアライゼーション
- **MQTT トピック設計** で gRPC メッセージの適切なルーティング

