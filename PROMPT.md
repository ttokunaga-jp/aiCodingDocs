### 1. 目的 (Goal / Objective)
- プロジェクトの骨格を整え、外部依存を持たないドメインロジック一式を実装する（Entity/VO/Repository IF/UseCase）ことで後続フェーズの土台を固める。

### 2. 制約条件 (Constraints)
- 言語: Go 1.21+、スタイル: uber-go/guide
- 外部ライブラリ: 原則禁止。uuid, errors, testing など標準系のみ（モックは手書き）
- アーキ: Clean/Hex。依存方向は domain -> usecase のみ。infra/adapter 禁止
- JSONタグ付与やHTTP依存の追加禁止（Adapter層の責務）
- カバレッジ目標: Domain/UseCase 100% 目標

### 3. タスク (Tasks)
1. `go.mod`、ディレクトリ構造、Linter 設定の作成
2. Entity / Value Object の定義と実装
3. Repository Interface の定義（実装しない）
4. Domain Service / UseCase の実装
5. Domain 層の Unit Test（Mock 使用, coverage 100% 目標）

### 4. 完了条件 (Completion Criteria)
- すべてのドメインビジネスルールがテストで検証済み
- カバレッジ 90%以上（目標 100%）
- ビルド & テストがローカルで通過
- `IMPLEMENT_REPORT_FMT.md` 準拠のレポートを `reports/phase_1_report.md` に出力

### 5. 品質チェック・出力フォーマット (Quality & Output Format)
- 命名/構造: Clean Arch 準拠。domain から外部依存を参照しない
- テスト: 正常系/異常系を分離し、Assertion を明記
- JSON 例:
```json
{
  "phase": "1",
  "tasksCompleted": [],
  "tasksPending": [],
  "errors": [],
  "nextActions": []
}
```

### 6. 実装報告とドキュメント更新 (Report & Document Update)
- 実装した Entity/VO/UseCase の概要と設計意図をレポートに追記
- 追加・変更した依存やファイルパスを JSON セクションに反映

### 7. 次フェーズのドキュメント修正 (Next Phase Prep)
- Repository 実装で必要な追加要件やスキーマ前提をメモ
- 未解決の TODO/リスクを列挙

### 8. メモリ / コンテキスト管理 (Memory / Context)
- 定義した Repository IF 名称
- ドメインルール上の制約（例: バリデーション条件）
- 今後必要になる環境変数の検討事項

### 9. 反復ループ (Plan → Execute → Evaluate → Revise)
- タスクごとにテストを実行し、失敗時は原因と修正案を箇条書きで残す
- 失敗が解消しない場合は 3 回まで修正を試み、それでも不可なら BLOCKED でレポート

### 10. 停止条件 (Stop Conditions)
- すべてのタスク完了かつ完了条件達成
- 重大な依存不足や仕様不明点で進行不能になった場合（BLOCKED としてレポート）
