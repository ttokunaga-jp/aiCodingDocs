# ディレクトリ構造 & アーキテクチャ規約

```text
/ (repo root)
 ├─ cmd/
 │   └─ server/
 ├─ internal/
 │   ├─ domain/
 │   ├─ usecase/
 │   ├─ adapter/
 │   └─ infra/
 ├─ api/           # OpenAPI/Proto
 ├─ configs/
 └─ tests/
```

## アーキテクチャ原則
- Clean/Hexagonal を前提に依存方向は `domain -> usecase -> adapter/infra` のみ許可。
- domain から infra 参照禁止。adapter からのみ infra を参照。
- DTO 変換は adapter 層で行い、domain モデルを外部露出しない。

