# ロボットクラウドシステム仕様リポジトリ

ロボットサービスのクラウドシステム仕様・設計・API 定義を一元管理

## ディレクトリ構成例

```
robot-cloud-system-spec/
├── README.md                # このファイル
├── architecture/            # システム構成図・アーキテクチャ図
│   ├── system_architecture.md
│   └── system_architecture.png
├── usecase/                 # ユースケース図・利用シナリオ
│   └── usecase_diagram.md
├── sequence/                # シーケンス図・主要フロー
│   ├── robot_command_flow.md
│   └── ...
├── entity/                  # エンティティ図・ER図・データ構造
│   └── er_diagram.md
├── state/                   # 状態遷移図
│   └── robot_state_machine.md
├── api/                     # API仕様（OpenAPI, GraphQL, etc.）
│   ├── openapi.yaml
│   └── graphql_schema.graphql
├── proto/                   # gRPC/Protocol Buffers定義
│   └── robot_control.proto
└── docs/                    # その他設計資料・補足説明
    └── implementation_guide.md
```

## 各ディレクトリの役割

- **architecture/**: システム全体の構成図やアーキテクチャ概要
- **usecase/**: ユースケース図や利用シナリオの説明
- **sequence/**: 主要な処理・通信フローのシーケンス図
- **entity/**: データ構造や ER 図、クラス図
- **state/**: ロボットや指令などの状態遷移図
- **api/**: REST, GraphQL 等の API 仕様書
- **proto/**: gRPC/Protocol Buffers の仕様定義（.proto ファイル）
- **docs/**: 実装ガイドや補足資料

## 管理方針

- 仕様・設計・API 定義を**1 リポジトリで一元管理**
- 図は Mermaid 記法や画像（PNG/SVG）で記載
- .proto ファイルもこのリポジトリでバージョン管理
- Pull Request ベースで仕様変更をレビュー

---

> **サンプルやテンプレートが必要な場合は、各ディレクトリに雛形ファイルを追加してください。**
