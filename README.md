# pkg

Shared Go packages for monitoring platform microservices.

## 📦 Packages

- **logger/clog** - slog-based structured logging with OpenTelemetry tracing
- **logger/zerolog** - zerolog-based structured logging with OpenTelemetry tracing

## 🚀 Installation

```bash
go get github.com/duynhne/pkg@latest
```

## 📖 Usage

### Clog Logger

```go
import "github.com/duynhne/pkg/logger/clog"

func main() {
    clog.Setup("info")
    clog.InfoContext(ctx, "server started", "port", 8080)
}
```

### Zerolog Logger

```go
import "github.com/duynhne/pkg/logger/zerolog"

func main() {
    zerolog.Setup("debug")
    log := zerolog.FromContext(ctx)
    log.Info().Msg("ready")
}
```

## 🛠️ Development

```bash
go mod download
go test -v ./...
golangci-lint run
```

## 📝 License

MIT
