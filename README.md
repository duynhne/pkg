# pkg

Shared Go library for monitoring platform microservices.

## Features

- **Logging**: Zerolog implementation with structured JSON output
- **Tracing**: OpenTelemetry span helpers
- **Common utilities**: Shared code across services

## Installation

```bash
go get github.com/duynhne/pkg
```

## Usage

```go
import "github.com/duynhne/pkg/logger/zerolog"

func main() {
    zerolog.Setup("info")
    zerolog.Info("Application started")
}
```

## License

MIT
