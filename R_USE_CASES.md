# ユースケース定義書（テンプレート）

目的: サービスが提供する主要シナリオを明文化し、API/イベント/ドメイン要件との対応を示す。`<placeholder>` を埋めて利用する。

## 記述フォーマット（例）
```yaml
UC-01 FetchOrderHistory:
  actor: EndUser
  trigger: GET /orders/{user_id}
  precondition:
    - user exists
    - authenticated
  main_flow:
    - validate user_id
    - fetch orders (last 2y)
    - sort desc
  exception_flow:
    - user_not_found -> 404 RFC7807
    - db_timeout -> 503 retryable=false
  output: orders[]
  related_api: D_INTERFACE_SPEC.md#/orders
  related_events: []
  acceptance:
    - returns orders in desc created_at
    - p95 < 200ms @ 1k rps
```

## 必須項目チェックリスト
- UseCase ID (UC-xx)
- アクター / トリガー / 前提条件
- メインフロー / 例外フロー
- 期待出力・成功条件
- 関連 API / イベント / ドメインモデル
- 非機能受入 (性能、可用性、監査など)

