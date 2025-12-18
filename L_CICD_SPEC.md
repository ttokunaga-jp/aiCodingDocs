# CI/CD パイプライン仕様

```yaml
Pipeline_Stages:
  1. Lint:
      - tool: "golangci-lint"
      - strict: true
  2. Test:
      - command: "go test ./... -race -coverprofile=coverage.out"
      - integration: "docker-compose up -d db"
  3. Security Scan:
      - tool: "trivy"
      - dependency_check: "govulncheck"
  4. Build:
      - output: Docker Image
      - tag: Git Commit SHA (short)
  5. Deploy:
      - trigger: push to main only
      - strategy: ArgoCD update / Terraform apply
Environment_Limitations:
  - secrets: GitHub Secrets (`${{ secrets.DB_PASSWORD }}`)
  - build_time_target: "<=5m"
```

