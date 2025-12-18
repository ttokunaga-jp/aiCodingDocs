# Implementation Report Template

各フェーズ完了時に `reports/phase_<n>_report.md` をこのフォーマットで生成すること。特に JSON ブロックは機械読み取り前提のため構文エラー禁止。

````markdown
# Phase [X] Implementation Report

## 1. Overview
- **Status**: [COMPLETED / INCOMPLETE / BLOCKED]
- **Date**: YYYY-MM-DD
- **Target Tasks**: 実施したタスク ID を列挙 (例: 1-1, 1-2)

## 2. Implemented Changes
- 主要なパッケージ・構造体・関数の概要と設計意図を箇条書きで記載
- 例: `internal/domain/user.go`: User Entity を追加。ID は UUID を採用。
- 例: `internal/usecase/create_user.go`: バリデーションロジックを実装。

## 3. Test Results
- **Unit Tests**: Pass: [N], Fail: [N]
- **Coverage**: [N]%
- **Integration Tests**: Pass: [N]
- **Known Issues**: 失敗やスキップしたテストがあれば記述

## 4. Deviations from Requirements
- 要件や設計と異なる実装をした場合、その理由を明記。なければ "None"。

## 5. Next Phase Preparation
- 次フェーズで必要な情報 (追加環境変数、マイグレーション実行の要否など) を列挙

---
<!-- MACHINE READABLE SECTION: DO NOT EDIT STRUCTURE -->
```json
{
  "phase": "1",
  "status": "COMPLETED",
  "tasksCompleted": ["1-1", "1-2"],
  "tasksPending": ["1-3"],
  "errors": [
    {"msg": "Integration test failed on DB timeout", "impact": "retry", "action": "increase timeout"}
  ],
  "nextActions": ["rerun integration after increasing timeout"],
  "artifacts": [
    "internal/domain/user.go",
    "internal/domain/user_test.go"
  ],
  "dependencies_added": [
    "github.com/google/uuid"
  ],
  "env_vars_required": [
    "APP_ENV"
  ],
  "todo_list": [
    "Review error messages for i18n"
  ],
  "context_memory": {
    "user_repository_interface_name": "UserRepository",
    "last_migration_version": "202310101200"
  }
}
```
---
````
