# Development Phases & Task Breakdown

このプロジェクトは以下の5フェーズで進行する。前フェーズの Completion Criteria を満たすまでは次フェーズへ進まないこと。各フェーズ開始時に「共通プロンプト構成 (下記)」を使って指示を生成し、完了時は `IMPLEMENT_REPORT_FMT.md` の形式でレポートを提出する。

## フェーズプロンプト共通テンプレート

以下をそのまま雛形として、各フェーズ/タスク内容を埋めて CodexAgent に渡す。

````markdown
### 1. 目的 (Goal / Objective)
- <フェーズで達成したい最終ゴール>

### 2. 制約条件 (Constraints)
- <言語/ライブラリ制限、性能/セキュリティ/運用制約など>

### 3. タスク (Tasks)
1. <具体的な作業>
2. <具体的な作業>

### 4. 完了条件 (Completion Criteria)
- <テスト/品質/ドキュメント観点での完了定義>

### 5. 品質チェック・出力フォーマット (Quality & Output Format)
- <命名/構造/テスト報告ルール>
- JSON 例:
```json
{
  "phase": "<phase_name_or_id>",
  "tasksCompleted": [],
  "tasksPending": [],
  "errors": [],
  "nextActions": []
}
```

### 6. 実装報告とドキュメント更新 (Report & Document Update)
- <Implement文書、仕様書へ追記すべき内容>

### 7. 次フェーズのドキュメント修正 (Next Phase Prep)
- <次フェーズへ引き継ぐ変更点/課題>

### 8. メモリ / コンテキスト管理 (Memory / Context)
- <保持すべき重要情報や永続化キー>

### 9. 反復ループ (Plan → Execute → Evaluate → Revise)
- <失敗時の修正サイクル、再実行ルール>

### 10. 停止条件 (Stop Conditions)
- <作業停止/終了条件>
````

## フェーズ定義とタスク

### Phase 1: Project Setup & Domain Definition
**Objective:** プロジェクト構造の確立と、外部依存を持たない純粋なドメインロジックの実装。  
**Dependencies:** なし  
**Tasks:**
1. [Setup] `go.mod`、ディレクトリ構造 (Clean Arch)、Linter 設定の作成
2. [Domain] Entity / Value Object の定義と実装
3. [Domain] Repository Interface の定義 (実装しない)
4. [Domain] Domain Service / UseCase の実装
5. [Test] Domain 層の Unit Test (Mock 使用, coverage 100% 目標)

### Phase 2: Adapter & Persistence Implementation
**Objective:** DB 接続や外部 API クライアントなどインフラ層の実装。  
**Dependencies:** Phase 1  
**Tasks:**
1. [Infra] DB Schema Migration ファイル作成 (SQL)
2. [Infra] Repository Interface の実体実装 (GORM/SQLc)
3. [Infra] Docker Compose (DB コンテナ) の設定
4. [Test] Repository 層の Integration Test (Testcontainers 使用)

### Phase 3: Interface & API Implementation
**Objective:** 外部入力を受け付ける API ハンドラーの実装。  
**Dependencies:** Phase 2  
**Tasks:**
1. [API] OpenAPI/Proto 定義に基づく Router & Handler 実装
2. [API] Request Validation & Error Mapping 実装
3. [API] Middleware (Auth, Logging, Recover) 実装
4. [Test] API Handler の Unit Test (UseCase Mock 使用)

### Phase 4: System Integration & Configuration
**Objective:** アプリとして起動可能な状態にする。  
**Dependencies:** Phase 3  
**Tasks:**
1. [Config] 環境変数読み込み処理 (`config/`) 実装
2. [Main] `cmd/server/main.go` の DI 構築
3. [Ops] Dockerfile 作成 (マルチステージ, 非 root)
4. [Ops] Graceful Shutdown の実装

### Phase 5: Final Review & Refactoring
**Objective:** 運用要件（ログ・メトリクス）の仕上げと E2E テスト。  
**Dependencies:** Phase 4  
**Tasks:**
1. [Obs] 構造化ログ、Metrics (Prometheus)、Tracing 設定
2. [Test] E2E シナリオ (Docker Compose 全体起動でテスト)
3. [Doc] README と API ドキュメントの最終更新

