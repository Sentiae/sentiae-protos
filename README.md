# Sentiae Protocol Buffers

This repository contains the Protocol Buffer definitions for all Sentiae microservices. It serves as the single source of truth for service contracts and generates Go client libraries for gRPC communication between services.

## Repository Structure

```
sentiae-protos/
├── api/proto/                 # Protocol buffer definitions
│   ├── auth/v1/              # Authentication service protos
│   └── identity/v1/          # Identity service protos
├── gen/go/                   # Generated Go code (auto-generated)
├── .github/workflows/        # CI/CD workflows
├── buf.yaml                  # Buf configuration
├── buf.gen.yaml             # Buf code generation configuration
├── go.mod                   # Go module definition
└── README.md                # This file
```

## Services

### Authentication Service (`api/proto/auth/v1/`)
Contains protocol buffer definitions for user authentication, session management, and authorization.

### Identity Service (`api/proto/identity/v1/`)
Contains protocol buffer definitions for user identity management, profile data, and user relationships.

## Usage

### In Go Projects

Add this module as a dependency to your Go project:

```bash
go get github.com/Sentiae/sentiae-protos@latest
```

Import the generated services in your Go code:

```go
import (
    authv1 "github.com/Sentiae/sentiae-protos/gen/go/api/proto/auth/v1"
    identityv1 "github.com/Sentiae/sentiae-protos/gen/go/api/proto/identity/v1"
)
```

## Development

### Prerequisites

- Go 1.21+
- [Buf CLI](https://docs.buf.build/installation)

### Local Development

1. Clone the repository:
```bash
git clone https://github.com/Sentiae/sentiae-protos.git
cd sentiae-protos
```

2. Install dependencies:
```bash
go mod tidy
```

3. Generate Go code from proto files:
```bash
buf generate
```

4. Run linting:
```bash
buf lint
```

### Adding New Proto Files

1. Create your `.proto` files in the appropriate service directory under `api/proto/`
2. Follow the established versioning pattern (`v1`, `v2`, etc.)
3. Run `buf generate` to generate Go code
4. Commit both the proto files and generated code
5. The CI/CD pipeline will automatically create a new release

### Code Generation

This repository uses [Buf](https://buf.build/) for protocol buffer compilation and code generation. The configuration is defined in:

- `buf.yaml`: Main Buf configuration (linting, breaking change detection)
- `buf.gen.yaml`: Code generation configuration (Go plugins)

Generated Go code is placed in `gen/go/` and follows the source-relative path structure.

## Versioning

This repository follows semantic versioning (SemVer):

- **Major version**: Breaking changes to existing proto definitions
- **Minor version**: New proto definitions or backward-compatible changes
- **Patch version**: Bug fixes, documentation updates, or other non-breaking changes

### Releases

Releases are automated through GitHub Actions:

- **Automatic**: Push to `main` branch triggers a patch release
- **Manual**: Use the "Release Proto Module" workflow with version type selection

Each release:
1. Generates fresh Go code from proto definitions
2. Runs tests to ensure code quality
3. Creates a Git tag with semantic version
4. Publishes a GitHub release
5. Makes the module available via `go get`

## Breaking Changes

When making breaking changes to proto definitions:

1. Create a new version directory (e.g., `v2/`)
2. Maintain backward compatibility by keeping older versions
3. Update service implementations to support multiple versions during transition
4. Use a major version bump when releasing

## Contributing

1. Fork the repository
2. Create a feature branch
3. Add or modify proto definitions
4. Generate and test the code locally
5. Submit a pull request

## License

This repository is part of the Sentiae project and follows the same licensing terms.