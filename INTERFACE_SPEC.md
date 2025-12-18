# インターフェース仕様（API / Event / gRPC）

## API 仕様 (OpenAPI)
機械可読形式で例を必ず含める。

```yaml
openapi: 3.0.1
info:
  title: Order History API
  version: 1.0.0
paths:
  /orders/{user_id}:
    get:
      summary: ユーザーの注文履歴取得
      parameters:
        - in: path
          name: user_id
          schema: { type: string, format: uuid }
        - in: query
          name: status
          schema: { type: string, enum: [pending, paid, canceled] }
      responses:
        '200':
          description: OK
          content:
            application/json:
              example:
                orders:
                  - id: "ord_1"
                    amount: 1200
                    status: "paid"
                    created_at: "2024-01-01T10:00:00Z"
        '404':
          description: Not Found
          content:
            application/json:
              example:
                type: "about:blank"
                title: "Resource Not Found"
                detail: "User not found"
                instance: "/orders/123"
                trace_id: "req-abc"
```

## イベント仕様 (Pub/Sub)

```yaml
event: OrderCreated
schema:
  order_id: string
  user_id: string
  status: string
  created_at: timestamp
retry_policy: exponential_backoff
dead_letter: order_created.dlq
```

