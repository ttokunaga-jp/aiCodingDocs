# 技術スタック・ライブラリ制約書

```yaml
Language:
  - version: "Go 1.25"
  - style_guide: "uber-go/guide"
Allowed_Libraries:
  - WebFramework: "Gin (v1.9.x)"
  - ORM: "GORM (v1.25.x)" or "sqlc (>=1.25, preferred)"
  - Logging: "Zap (1.x)" # JSON Lines必須, RFC7807と整合
  - Testing: "Testify (1.8+)" # mock使用可
Banned_Libraries:
  - "Sirupsen/logrus" # maintenance mode
  - "net/http default mux"
  - "echo", "fiber" # フレームワーク統一のため禁止
Testing/Mock:
  - "testify/mock" allowed
  - "gomock" optional
Observability:
  - Logging: JSON Lines, fields: level, ts, caller, msg, trace_id, span_id
  - Tracing/Metrics: OpenTelemetry 1.x
```
