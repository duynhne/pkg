# pkg - Shared Go Library

> AI Agent context for understanding this repository

## 📋 Overview

This repository contains shared Go packages used across all microservices in the monitoring platform. It provides common utilities and abstractions to ensure consistency and reduce code duplication.

## 🏗️ Architecture

```
pkg/
├── logger/
│   ├── clog/          # slog-based logger with clog wrapper
│   │   └── logger.go  # TracingHandler, Setup(), context helpers
│   └── zerolog/       # zerolog-based logger
│       └── logger.go  # Setup(), context helpers
├── go.mod
└── go.sum
```

## 📦 Packages

### `logger/clog`

Structured logging using Go's standard `log/slog` with [chainguard-dev/clog](https://github.com/chainguard-dev/clog) wrapper. Features:

- **TracingHandler**: Middleware that injects `trace_id` and `span_id` from OpenTelemetry context
- **Setup(level)**: Initialize global logger with JSON output and tracing support
- **Context helpers**: `WithLogger()`, `FromContext()`, `InfoContext()`, `ErrorContext()`, etc.

```go
import "github.com/duynhne/pkg/logger/clog"

func main() {
    clog.Setup("info")
    clog.InfoContext(ctx, "server started", "port", 8080)
}
```

### `logger/zerolog`

Alternative logger using [rs/zerolog](https://github.com/rs/zerolog). Features:

- **Setup(level)**: Initialize global zerolog with Unix timestamp format
- **WithContext()**: Attach logger to context with automatic trace injection
- **FromContext()**: Retrieve logger from context

```go
import "github.com/duynhne/pkg/logger/zerolog"

func main() {
    zerolog.Setup("debug")
    log := zerolog.FromContext(ctx)
    log.Info().Msg("ready")
}
```

## 🔧 Dependencies

| Package | Version | Purpose |
|---------|---------|---------|
| `github.com/chainguard-dev/clog` | v1.8.0 | slog wrapper with context |
| `github.com/rs/zerolog` | v1.34.0 | High-performance structured logging |
| `go.opentelemetry.io/otel/trace` | v1.39.0 | Trace context extraction |

## 🛠️ Development

### Build & Test

```bash
# Download dependencies
go mod download

# Run tests
go test -v ./...

# Run tests with race detection
go test -race ./...

# Run linter
golangci-lint run
```

### Local Development

When developing services that depend on this package locally:

```go
// In service's go.mod, add replace directive for local development:
replace github.com/duynhne/pkg => ../pkg
```

## 🚀 CI/CD

This repo uses reusable GitHub Actions from [shared-workflows](https://github.com/duyhenryer/shared-workflows):

- **go-check.yml**: Tests and linting on PRs
- **sonarqube.yml**: SonarCloud analysis

## 📐 Code Style

- Follow standard Go conventions
- Use context-based logging for traceability
- All public functions should have doc comments
- Log levels: debug, info, warn, error

## 🔗 Used By

- `auth-service`
- `user-service`
- `product-service`
- `cart-service`
- `order-service`
- `review-service`
- `notification-service`
- `shipping-service`

## 📝 Versioning

Uses semantic versioning. Services should depend on specific tags:

```go
require github.com/duynhne/pkg v1.0.0
```
