# 要件定義書（Functional / Non-Functional Requirements）

## 機能要件 (FR)
API 単位で正常系・異常系を分離する。

```yaml
FR-01:
  description: ユーザーIDから注文履歴を取得する
  input: user_id, from (optional), to (optional), status (optional)
  output: orders[]
  error:
    - user_not_found
    - invalid_date_range
    - db_timeout
FR-02:
  description: 期間別の注文集計を返す
  input: user_id, granularity (day|month)
  output: summaries[]
  error:
    - user_not_found
    - db_timeout
```

## 非機能要件 (NFR)
CodexAgent の設計判断を縛るため必須。

```yaml
- レイテンシ: p95 < 200ms
- 可用性: 99.9%
- スケーラビリティ: 水平スケール前提 (stateless)
- セキュリティ: OAuth2 (client credentials), mTLS
- 観測性: metrics, logs, traces を必須とし OpenTelemetry を採用
```

