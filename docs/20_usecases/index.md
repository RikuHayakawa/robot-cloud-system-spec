**[← ドキュメント一覧に戻る](../index.md)**

# ユースケース概要

## アクター一覧

- **管理者**: 管理画面から指令を出したり情報を閲覧する人
- **ロボット**: 指令に応じて行動し、状態やエラーを返すハードウェア
- **Slack**: システムからの通知を受け取る外部サービス

## ユースケース一覧

* UC01 - [ロボット管理機能](UC01_robot_management/index.md)
* UC02 - [ロボット指令機能](UC02_robot_command/index.md)
* UC03 - [データ管理機能](UC03_data_management/index.md)
* UC04 - [エラー通知機能](UC04_error_notification/index.md) 


## 全体ユースケース図

```mermaid
graph TD
    Admin["👤 管理者"]
    Robot["🤖 ロボット"]
    Slack["💬 Slack"]

    subgraph ロボット管理機能
        UC1-1(UC1-1: ロボット個体を登録する)
        UC1-2(UC1-2: ロボット情報を管理する)
        UC1-3(UC1-3: ロボット接続を確認する)
    end

    subgraph ロボット指令機能
        UC2-1(UC2-1: ロボットに指令を送信する)
        UC2-2(UC2-2: 指令実行結果を報告する)
        UC2-3(UC2-3: 指令状況を確認する)
    end

    subgraph データ管理機能
        UC3-1(UC3-1: データを記録する)
        UC3-2(UC3-2: データを閲覧する)
        UC3-3(UC3-3: 実験セッションを管理する)
    end

    subgraph エラー通知機能
        UC4-1(UC4-1: エラーを検知・通知する)
        UC4-2(UC4-2: エラー情報を確認する)
    end

    %% ロボット管理機能の関係
    Admin --- UC1-1
    Admin --- UC1-2
    Admin --- UC1-3
    Robot --- UC1-3

    %% ロボット指令機能の関係
    Admin --- UC2-1
    Robot --- UC2-2
    Admin --- UC2-3

    %% データ管理機能の関係
    Robot --- UC3-1
    Admin --- UC3-2
    Admin --- UC3-3

    %% エラー通知機能の関係
    Robot --- UC4-1
    Admin --- UC4-2
    UC4-1 --- Slack
```


## ユースケース間の関連

各ユースケース間の関連性と依存関係については、以下のドキュメントを参照してください：
📖 **[ユースケース間の関連](usecase_relationships.md)**

## 関連ドキュメント

- [機能要求仕様](../10_requirements/functional_requirements.md)
