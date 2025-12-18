# Feature Flag 方針書

- SDK 利用: OpenFeature/LaunchDarkly/ConfigCat をラッパ経由で呼び出す。
- 命名: `[service]_[layer]_[feature_name]` 例 `order_api_use_new_discount_logic`。
- Fallback: 取得失敗時は安全側（新機能は `false`）。
- Context: `user_id`/`tenant_id` を必ず渡す。
- トグル種別: Release / Ops / Permission。
- コード例: `if featureFlag.IsEnabled(ctx, "order_api_use_new_discount_logic", user) { ... }`

