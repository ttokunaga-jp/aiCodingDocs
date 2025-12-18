# 運用・デプロイ仕様（概要）

- Docker: マルチステージ、非 root 実行、Distroless もしくは Alpine。
- CI/CD: Lint -> Test -> Security Scan -> Build -> Deploy の順で GitHub Actions を想定。
- 環境変数: `.env.example` を用意し Config はコード化。
- Feature Flag: トグル種別定義と SDK ラッパを用意。

