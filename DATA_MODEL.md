# データモデル定義（Domain Model / DB Schema）

```sql
-- 正規化レベル: 第3正規形
orders (
  id UUID PRIMARY KEY,
  user_id UUID NOT NULL,
  status VARCHAR(16) NOT NULL, -- pending/paid/canceled
  amount INTEGER NOT NULL,
  currency CHAR(3) NOT NULL,
  created_at TIMESTAMP NOT NULL,
  updated_at TIMESTAMP NOT NULL
);

-- 推奨インデックス
CREATE INDEX idx_orders_user_created_at ON orders(user_id, created_at DESC);
CREATE INDEX idx_orders_status_created_at ON orders(status, created_at DESC);

-- ID 方針: UUID v7、DB で生成しない（アプリ側で生成）
-- リレーション: users.id -> orders.user_id (FK)
```
