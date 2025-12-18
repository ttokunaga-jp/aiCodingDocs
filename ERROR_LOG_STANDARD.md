# エラーハンドリング & ログ出力標準

```json
{
  "type": "about:blank",
  "title": "Resource Not Found",
  "detail": "Order ID xxx does not exist",
  "instance": "/orders/xxx",
  "trace_id": "req-12345"
}
```

- ログ形式: JSON Lines。必須フィールド `level`, `ts`, `caller`, `msg`, `trace_id`, `span_id`。
- 禁止: `fmt.Println`。

