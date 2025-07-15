# ロボットクラウドシステム仕様リポジトリ

ロボットサービスのクラウドシステム仕様・設計・API 定義を一元管理

**📚 [→ ドキュメント一覧はこちら](./docs/index.md)**

## ドキュメント運用方法

### 基本方針

- 仕様・設計・API 定義を **1 リポジトリで一元管理**
- 図は Mermaid 記法や PlantUML で記載
- Pull Request ベースで仕様変更をレビュー
- 新しい仕様は `docs/` ディレクトリ以下に配置
- 各ディレクトリには `index.md` でアクセス可能

### ドキュメント作成・更新ルール

#### 📝 新規ドキュメント作成時

1. 適切なディレクトリ配下にファイルを作成
2. 対応するディレクトリの `index.md` にリンクを追加
3. 必要に応じて `docs/index.md` にクイックリンクを追加

#### 🔄 既存ドキュメント更新時

1. 変更理由・影響範囲を明記した Pull Request を作成
2. 関連するドキュメントとの整合性を確認
3. 図や API 仕様の変更は dependencies を確認

#### 📊 図・ダイアグラム作成規則

- **シーケンス図**: Mermaid (`.md`)
- **画面遷移図**: Mermaid (`.md`)
- **状態遷移図**: Mermaid (`.md`)

#### 🔗 リンク・参照規則

- 内部リンクは相対パスを使用
- 外部システムの仕様書は URL で参照
- 図は同一ディレクトリまたは適切なサブディレクトリに配置


## 主要なドキュメント

### 概要・要件

- [システム全体アーキテクチャ](./docs/00_overview/system_architecture.md)
- [機能要件一覧](./docs/10_requirements/functional_requirements.md)
- [非機能要件一覧](./docs/10_requirements/non_functional_requirements.md)

### ユースケース

- [ユースケース概要](./docs/20_usecases/index.md)
- [ユースケース間の関連](./docs/20_usecases/usecase_relationships.md)
- [ロボット管理機能](./docs/20_usecases/UC01_robot_management/index.md)
- [ロボット指令機能](./docs/20_usecases/UC02_robot_command/index.md)
- [データ管理機能](./docs/20_usecases/UC03_data_management/index.md)
- [エラー通知機能](./docs/20_usecases/UC04_error_notification/index.md)

---

> **注意**: 各ディレクトリは `index.md` でアクセス可能です。概要から詳細への段階的な参照が可能な構造になっています。

## ディレクトリ構成 (実際の構成とは異なる場合がある)

```
/
├── docs/                         # 仕様・設計文書
│   ├── 00_overview/              # 概要・全体構成
│   │   └── system_architecture.md    # システム全体の構成・アーキテクチャ
│   │
│   ├── 10_requirements/          # 要件定義（What）
│   │   └── functional_requirements.md     # 機能要件一覧・機能間依存関係
│   │
│   ├── 20_usecases/              # ユースケース定義（Who/When/What）
│   │   ├── index.md                   # ユースケース概要・一覧
│   │   ├── UC01_robot_management/     # ロボット管理機能
│   │   │   ├── index.md               # UC の説明、前提、正常・異常系
│   │   │   ├── sequence.mmd           # Mermaid シーケンス図
│   │   │   ├── api_spec.md            # API 仕様
│   │   │   └── class_diagram.pu       # クラス図（PlantUML）
│   │   ├── UC02_robot_command/        # ロボット指令機能
│   │   │   └── index.md               # UC の説明、前提、正常・異常系
│   │   ├── UC03_data_management/      # データ管理機能
│   │   │   └── index.md               # UC の説明、前提、正常・異常系
│   │   └── UC04_error_notification/   # エラー通知機能
│   │       └── index.md               # UC の説明、前提、正常・異常系
│   │
│   ├── 30_external_design/       # 外部設計（UI/API/I/O）
│   │   ├── screen_transition.mmd      # 画面遷移図
│   │   ├── wireframes/                # UI モック（画像または Figma リンク）
│   │   ├── api_specs/
│   │   │   ├── openapi.yaml           # OpenAPI で書かれた API 定義
│   │   │   └── endpoints.md           # エンドポイント一覧（API と UC の対応）
│   │   └── interface_spec.md          # 他システムやロボットとの I/F 仕様
│   │
│   └── 40_internal_design/       # 内部設計（How）
│       ├── db/
│       │   ├── er_diagram.pu          # ER 図（PlantUML など）
│       │   └── schema.md              # テーブル定義（型、制約、初期値など）
│       ├── modules/
│       │   ├── robot_controller.md    # 各内部モジュールの責任・インターフェース
│       │   └── experiment_logger.md
│       ├── logic/
│       │   ├── state_transition.md    # 状態遷移図（Mermaid）
│       │   └── error_handling.md      # 異常系の処理フロー
│       └── batch/                     # バッチ処理や定期ジョブの設計
│           └── export_logs.md
```

## 各ディレクトリの役割

### メインドキュメント（docs/）

- **[00_overview/](./docs/00_overview/)**: システム全体の構成図やアーキテクチャ概要
- **[10_requirements/](./docs/10_requirements/)**: 機能要件定義・機能間依存関係
- **[20_usecases/](./docs/20_usecases/)**: ユースケース定義・シーケンス図・API 仕様
- **[30_external_design/](./docs/30_external_design/)**: 外部設計（UI/API/I/O）
- **[40_internal_design/](./docs/40_internal_design/)**: 内部設計（データベース・モジュール・ロジック）
