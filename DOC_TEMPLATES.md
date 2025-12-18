# CodexAgent 用 ドキュメント索引

個別に分割したテンプレート/方針ドキュメントへのリンク集。各ファイルを更新元とし、本索引は見出しと位置の案内のみを保持する。

- サービス憲章: `SERVICE_CHARTER.md` (責務/非責務とSLOを定義)
- 要件定義 (FR/NFR): `REQUIREMENTS.md` (機能/非機能をAPI単位で明文化)
- インターフェース仕様 (API/Event): `INTERFACE_SPEC.md` (OpenAPI+イベントスキーマ)
- データモデル: `DATA_MODEL.md` (スキーマとインデックス/リレーション)
- ディレクトリ構造・アーキ原則: `ARCHITECTURE.md` (依存方向ルール)
- 運用・デプロイ概要: `OPS_DEPLOY_OVERVIEW.md` (CI/CD・Docker 方針の概要)
- 技術スタック制約: `TECH_STACK_CONSTRAINTS.md` (言語/ライブラリの許可・禁止)
- テスト戦略: `TEST_STRATEGY.md` (UT/IT方針とカバレッジ基準)
- エラー/ログ標準: `ERROR_LOG_STANDARD.md` (RFC7807, JSON Lines ログ)
- Dockerfile方針: `DOCKERFILE_POLICY.md` (ベース/ランタイム/非root/キャッシュ戦略)
- CI/CD仕様: `CICD_SPEC.md` (Lint/Test/Security/Build/Deploy フロー)
- 環境変数レジストリ: `ENV_VARS_REGISTRY.md` (型・必須・Secret・再起動要否)
- Feature Flag方針: `FEATURE_FLAG_POLICY.md` (命名/SDKラッパ/フォールバック)
- フェーズ別タスクブレークダウン: `TASK_PHASES.md` (進行順と依存)
- 実装レポートフォーマット: `IMPLEMENT_REPORT_FMT.md` (Markdown+JSON の提出型)
- フェーズ1プロンプト雛形: `docs/prompts/phase1.md` (開始時指示の雛形)
