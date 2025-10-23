# 🧱 Go Clean Architecture

**A Production-Ready Golang Backend Template**  
**Clean Architecture | SOLID Principles | Domain-Driven Design | Testable | DevOps Ready**

---

## 📘 Overview

`go-clean-architecture` is a **scalable and maintainable Go backend project template** that follows:

- **Clean Architecture**: Separates business logic from frameworks and infrastructure  
- **Domain-Driven Design (DDD)**: Focuses on core business logic through domain entities  
- **SOLID Principles**: Each component has a single responsibility and dependencies flow inward  
- **Testability**: Easy to unit test services, repositories, and handlers  
- **DevOps Ready**: Includes Docker, Docker Compose, Kubernetes manifests, and CI/CD pipeline  

This template is ideal for **microservices**, **REST APIs**, and **internal backend services**.

---

## 🧩 Features

- Modular, layered architecture
- Handler → Service → Repository → Domain separation
- Middleware support (authentication, logging, rate limiting)
- Configurable via `config.yaml`
- Built-in rate limiter and utility functions
- Unit and integration tests
- OpenAPI/Swagger support
- Docker, Docker Compose, Kubernetes deployment manifests
- CI/CD workflow with GitHub Actions
- Makefile for common tasks (build, run, test)

---

## 📂 Project Structure

```
go-clean-architecture/
├── cmd/
│   └── server/
│       └── main.go              # Application entry point
├── internal/
│   ├── domain/                  # Core business entities & rules
│   ├── handler/                 # HTTP handlers (API layer)
│   ├── service/                 # Business logic (use cases)
│   ├── repository/              # Data persistence layer
│   ├── middleware/              # Logging, auth, rate limiter, etc.
│   └── server/                  # Router & server bootstrap
├── pkg/
│   ├── models/                  # DTOs and reusable models
│   ├── utils/                   # Helpers/utilities
│   └── ratelimiter/             # Reusable rate limiter
├── api/
│   └── openapi/                 # OpenAPI/Swagger specs
├── configs/
│   └── config.yaml              # Application configuration
├── deployments/
│   ├── docker/
│   │   ├── Dockerfile
│   │   └── docker-compose.yaml
│   └── k8s/
│       └── deployment.yaml
├── scripts/                     # Build, test, deploy scripts
├── test/                        # Unit and integration tests
├── .github/workflows/           # CI/CD pipelines
├── Makefile                     # Common commands
├── go.mod                        # Module definition
└── README.md                     # Project documentation
```

---

## ⚙️ Layer Responsibilities

| Layer | Purpose |
|-------|---------|
| **cmd/server/** | Application entry point; minimal code, only bootstraps server |
| **internal/server/** | Sets up router, middleware, dependency injection, and starts server |
| **internal/handler/** | Handles HTTP requests, encodes/decodes, and forwards to service layer |
| **internal/service/** | Business logic, orchestration of domain entities and repository operations |
| **internal/repository/** | Data access: interacts with DB, caching, external services |
| **internal/domain/** | Core business models and validation rules, framework-agnostic |
| **internal/middleware/** | Authentication, logging, rate limiting, error handling |
| **pkg/** | Reusable libraries (models, utils, ratelimiter) that can be imported outside the project |
| **configs/** | Configuration files (YAML/JSON) |
| **deployments/** | Docker and Kubernetes manifests |
| **scripts/** | Build, test, deploy automation scripts |
| **test/** | Unit and integration tests |
| **api/openapi/** | API specifications (OpenAPI/Swagger) |

---

## Architecture Overview

```
flowchart TD
    A[Client] --> B[Middleware (Auth/RateLimit/Logger)]
    B --> C[Handler (API)]
    C --> D[Service Layer]
    D --> E[Repository Layer]
    E --> F[Domain Layer]
```

- **Dependencies flow inward:** outer layers (HTTP, DB) depend on inner layers (service, domain)  
- **Domain layer** is framework-agnostic → easy to reuse and test  
- Middleware, router, and server setup are **isolated from business logic**

---

## 🔧 Configuration

All settings are centralized in `configs/config.yaml`:

```yaml
server:
  port: 8080

database:
  host: localhost
  port: 5432
  user: admin
  password: secret
  name: go_clean

ratelimiter:
  requestsPerMinute: 100
```

- Load configs via a utility function (`pkg/utils/config_loader.go`)  
- Supports different environments (development, staging, production)

---

## 🚀 Building & Running

### Run locally
```bash
make run
```

### Build binary
```bash
make build
```

### Run with Docker
```bash
docker build -t go-clean-architecture:latest .
docker run -p 8080:8080 go-clean-architecture
```

### Run with Docker Compose
```bash
docker-compose up --build
```

---

## 🧪 Testing

### Run all tests
```bash
make test
```

- Unit tests: `test/user_service_test.go`  
- Integration tests: `test/user_handler_test.go`  
- Uses dependency injection and mock repositories for isolation

---

## 🧱 Middleware

- **Authentication:** JWT, API key validation  
- **Rate Limiter:** In-memory or Redis token bucket  
- **Logger:** Logs request and response  
- **Recovery:** Handles panics gracefully

All middleware are in `internal/middleware/` and registered in `internal/server/router.go`.

---

## 📈 Deployment

### Docker
- `deployments/docker/Dockerfile` — Multi-stage build for lightweight binary
- `docker-compose.yaml` — Multi-service setup

### Kubernetes
- `deployments/k8s/deployment.yaml` — Deployment, service, and configmaps

---

## 🔁 CI/CD

GitHub Actions pipeline in `.github/workflows/ci-cd.yaml`:

- Runs lint and tests on every push
- Builds Docker image
- Optionally deploys to cloud

---

## 🧩 Makefile Commands

| Command | Description |
|---------|------------|
| `make run` | Run locally |
| `make build` | Build binary |
| `make test` | Run all tests |
| `make docker-build` | Build Docker image |
| `make lint` | Run code linter |
| `make ci` | Run full CI pipeline |

---

## 🏗️ Contributing

1. Fork the repository  
2. Create a feature branch (\`git checkout -b feature/my-feature\`)  
3. Commit your changes (\`git commit -m "Add feature"\`)  
4. Push and open a PR  

Follow the **existing code structure**, **naming conventions**, and **Clean Architecture principles**.

---

## 📝 Summary

\`go-clean-architecture\` provides:

- **Clean separation of concerns**
- **Scalable and maintainable project structure**
- **Middleware and rate-limiting support**
- **Testable code with mocks**
- **Docker, Kubernetes, CI/CD ready**
- **OpenAPI documentation support**

> Use this template as a starting point for your Go backend services or microservices — it’s both a **starter kit** and a **developer guide**.
