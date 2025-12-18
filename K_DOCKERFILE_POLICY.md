# Dockerfile 方針書

- Build: `golang:1.25` など公式最新安定版。
- Runtime: `gcr.io/distroless/static-debian11` もしくは Alpine。
- 要件:
  1. マルチステージでビルドと実行を分離。
  2. 実行時は非 root (`USER nonroot:nonroot` など具体名を指定)。
  3. `go mod download` をソースコピー前に実行しキャッシュを効かせる。
  4. JST (Asia/Tokyo) 設定。
  5. PID1 を適切に設定しシグナルハンドリング可能にする。

## スケルトン例
```Dockerfile
# Build stage
FROM golang:1.25-bullseye AS builder
WORKDIR /app
COPY go.mod go.sum ./
RUN go mod download
COPY . .
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -o server ./cmd/server

# Runtime stage
FROM gcr.io/distroless/static-debian11
WORKDIR /app
COPY --from=builder /app/server /app/server
ENV TZ=Asia/Tokyo
USER nonroot:nonroot
ENTRYPOINT ["/app/server"]
```

## キャッシュ最適化
- 依存取得 (`go mod download`) をソースコピー前に実行し、変更がない場合はビルドキャッシュを再利用。
- `CGO_ENABLED=0` を指定し、distroless/static と組み合わせて最小イメージにする。

## シグナル/エントリポイント
- `ENTRYPOINT` をバイナリに設定し、SIGTERM/SIGINT で Graceful Shutdown するハンドラーをアプリ側で実装。
