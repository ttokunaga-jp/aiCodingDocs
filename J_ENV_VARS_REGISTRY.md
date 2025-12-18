# 環境変数レジストリ

| 変数名 | 型 | 必須 | デフォルト | Secret | 再起動要否 | 例値 | 説明 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `PORT` | int | No | 8080 | No | Yes | 8080 | アプリケーションポート |
| `ENV` | enum | Yes | - | No | Yes | dev | `dev`, `stg`, `prod` |
| `DB_HOST` | string | Yes | - | No | Yes | db.internal | R/W 用ホスト |
| `DB_PASS` | string | Yes | - | Yes | Yes | (unset) | Secret。ログ出力禁止 |
| `LOG_LEVEL` | enum | No | `info` | No | No | debug | `debug`, `info`, `warn`, `error` |
| `OTEL_EXPORTER_ENDPOINT` | url | No | - | No | No | https://otel-collector:4317 | OpenTelemetry 送付先 |
| `FEATURE_FLAGS_KEY` | string | No | - | Yes | No | (unset) | Feature Flag SDK Key |
