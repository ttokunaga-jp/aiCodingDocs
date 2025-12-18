# テスト戦略・カバレッジ基準

```markdown
- Unit Test: Domain/UseCase は 100% Mock 使用。DB 接続禁止。
- Integration Test: Handler から DB までの貫通。Testcontainers 必須。
- Coverage Goal: Line coverage > 80% (UseCase 層 > 95%)
- Naming: Test[Func]_[Condition]_[Expected]
```

