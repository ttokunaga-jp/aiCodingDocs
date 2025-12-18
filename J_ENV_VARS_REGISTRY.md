# 環境変数レジストリ（GCPデプロイ前提：汎用テンプレート）

GitHub Secrets には CI に必要な最小限のみ、Prod 用の機密は GCP Secret Manager にのみ置く方針。サービス個別の値は `<placeholder>` を埋めて利用する。

## 1. アプリケーション動作制御
| 変数名 | 型 | Local (.env) | CI (GitHub) | Prod (GCP) | Secret | 再起動要否 | 説明 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `APP_ENV` | enum | `local` | `ci` | Env: `production` | No | Yes | 環境識別子 |
| `LOG_LEVEL` | enum | `debug` | `info` | Env: `info` | No | No | ログ詳細度 |
| `SKIP_EXTERNAL_CALLS` | bool | `false` | `true` | Env: `false` | No | No | 外部API/サービス呼び出しをモック化 (CI は true 推奨) |
| `MOCK_DEPENDENCIES` | bool | `false` | `true` | Env: `false` | No | No | 依存サービスをモックするか |

## 2. 外部API・認証
| 変数名 | Local (.env) | CI (GitHub) | Prod (GCP) | 説明 |
| :--- | :--- | :--- | :--- | :--- |
| `API_BASE_URL` | `http://localhost:9000` | - | Env: `https://api.example.com` | 外部APIのベースURL |
| `API_KEY_PRIMARY` | `dev-key-123` | - | sm://`api-key-primary` | 外部APIキー |
| `API_KEY_SECONDARY` | (任意) | - | sm://`api-key-secondary` | 予備/別環境用キー |
| `API_TIMEOUT_SEC` | `30` | `10` | Env: `60` | API 呼び出しタイムアウト |
| `API_AUTH_METHOD` | `api_key` | `none` | Env: `mtls` | 認証方式（api_key/basic/oauth/mtlsなど） |
| `MTLS_CLIENT_CERT_PATH` | - | - | sm://`mtls-client-cert` | mTLS クライアント証明書 |
| `MTLS_CLIENT_KEY_PATH` | - | - | sm://`mtls-client-key` | mTLS 秘密鍵 |

## 3. サービス間連携 (内部マイクロサービス)
| 変数名 | Local (.env) | CI (GitHub) | Prod (GCP) | Secret | 説明 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `SERVICE_A_URL` | `http://localhost:8081` | - | Env: `https://service-a.internal` | No | サービスAのエンドポイント |
| `SERVICE_B_URL` | `http://localhost:8082` | - | Env: `https://service-b.internal` | No | サービスBのエンドポイント |
| `SERVICE_A_AUTH_TOKEN` | `dev-token-a` | - | sm://`service-a-token` | Yes | サービスA認証トークン |
| `SERVICE_B_AUTH_TOKEN` | `dev-token-b` | - | sm://`service-b-token` | Yes | サービスB認証トークン |

## 4. インフラ・ミドルウェア
| 変数名 | Local (.env) | CI (GitHub) | Prod (GCP) | Secret | 説明 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `DB_HOST` | `localhost` | `localhost` (container) | Env: `<db-host>` | No | DB ホスト |
| `DB_USER` | `app` | `app` | sm://`db-user` | Yes | DB ユーザー |
| `DB_PASS` | `app-pass` | `ci-pass` | sm://`db-pass` | Yes | DB パスワード |
| `DB_NAME` | `app` | `app` | Env: `<db-name>` | No | DB 名 |
| `KAFKA_BROKERS` | `localhost:9092` | - | Env: `<kafka-host>:9092` | No | Kafka ブローカー |
| `KAFKA_USE_TLS` | `false` | `false` | Env: `true` | No | TLS 利用可否 |
| `KAFKA_SASL_USER` | - | - | sm://`kafka-sasl-user` | Yes | Kafka 認証ユーザー |
| `KAFKA_SASL_PASS` | - | - | sm://`kafka-sasl-pass` | Yes | Kafka 認証パス |
| `PORT` | `8080` | `8080` | Env: `8080` | No | サーバー待受ポート |

---
### 運用ガイド
- Local: `.env` にすべて記載し実サービス/ローカル依存を使って検証。
- CI: コストと速度重視。外部呼び出しはモック化し、高価なキーは登録しない。
- Prod (GCP): セキュリティ重視。機密は Secret Manager (`sm://...`) 経由で注入し、GitHub Secrets には本番キーを置かない。

---
### 運用ガイド
- Local: `.env` にすべて記載し実サービス/ローカル依存を使って検証。
- CI: コストと速度重視。外部呼び出しはモック化し、高価なキーは登録しない。
- Prod (GCP): セキュリティ重視。機密は Secret Manager (`sm://...`) 経由で注入し、GitHub Secrets には本番キーを置かない。
