<img src="docs/images/banner.png"  />

[![Codacy Badge](https://api.codacy.com/project/badge/Grade/468af095477348da81b1024bc73dcb7a)](https://app.codacy.com/gh/MIKTHATGUY/WallWhale?utm_source=github.com&utm_medium=referral&utm_content=MIKTHATGUY/WallWhale&utm_campaign=Badge_Grade)
[![GitHub Stars](https://img.shields.io/github/stars/MIKTHATGUY/WallWhale?style=social)](https://github.com/MIKTHATGUY/WallWhale) [![Issues](https://img.shields.io/github/issues/MIKTHATGUY/WallWhale)](https://github.com/MIKTHATGUY/WallWhale/issues) [![License](https://img.shields.io/github/license/MIKTHATGUY/WallWhale)](LICENSE) [![Node Version](https://img.shields.io/badge/node-%3E%3D18.0.0-brightgreen)](https://nodejs.org/)

[![Docker](https://img.shields.io/badge/docker-ready-blue?logo=docker)](https://hub.docker.com) [![TypeScript](https://img.shields.io/badge/typescript-5.9-blue?logo=typescript)](https://typescriptlang.org) [![Fastify](https://img.shields.io/badge/fastify-5.5-green?logo=fastify)](https://fastify.io) [![Prisma](https://img.shields.io/badge/prisma-6.14-purple?logo=prisma)](https://prisma.io)

**WallWhale** is a production-ready server for downloading and hosting Steam
Workshop content with enterprise features. Built with TypeScript, Fastify,
and Prisma, it provides secure API access, multi-account Steam integration,
audit logging, and comprehensive monitoring. The system supports bulk downloads,
automated deployments, and scales horizontally with Docker and Kubernetes.

Get started in 60 seconds:

```bash
# Docker (recommended)
docker-compose up -d
curl http://localhost:3000/health

# Local development
npm install && npm run db:push && npm run setup && npm run dev
```

## Core components

**API Server** (`src/index.ts`, `src/routes/`) - Fastify web server with
authentication, rate limiting, and OpenAPI documentation. Handles download
requests, user management, and real-time monitoring endpoints.

**Download Engine** (`src/services/downloadService.ts`, `src/utils/depotDownloader.ts`) -
Orchestrates Steam Workshop downloads using the DepotDownloader binary.
Manages concurrent downloads, queue processing, and retry logic.

**Database Layer** (`prisma/schema.prisma`, `src/plugins/prisma.ts`) - Prisma
ORM with SQLite/PostgreSQL support. Stores user accounts, download history,
audit logs, and system configuration.

**Authentication System** (`src/plugins/auth.ts`, `src/utils/crypto.ts`) -
Dual authentication with JWT tokens and API keys. Supports role-based access
control and session management.

**CLI Tools** (`src/commands/`, `src/utils/`) - Command-line interface for
server setup, certificate management, direct downloads, and maintenance
operations.

**File Hosting** (`src/utils/fileHosting.ts`, `src/utils/directDownload.ts`) -
Static file server with password protection, download tracking, and bandwidth
limiting for serving downloaded workshop content.

**Monitoring & Logging** (`src/plugins/audit.ts`, `src/utils/audit.ts`) -
Comprehensive audit logging, Prometheus metrics, health checks, and
structured JSON logging for production observability.

**Security Layer** (`src/utils/certificates.ts`, `src/plugins/register.ts`) -
TLS certificate management, input validation, CORS configuration, and
secure headers for production deployments.

## API workflow

Download a workshop item:

```bash
curl -X POST http://localhost:3000/v1/downloads \
  -H "Authorization: Bearer your-api-key" \
  -H "Content-Type: application/json" \
  -d '{"workshopId": "123456789", "steamAccount": "account_name"}'
```

Monitor progress:

```bash
curl http://localhost:3000/v1/downloads/download-id \
  -H "Authorization: Bearer your-api-key"
```

## Production deployment

Docker Compose with external database:

```bash
# Set environment variables
export DATABASE_URL="postgresql://user:pass@host:5432/wallwhale"
export JWT_SECRET="your-jwt-secret"

# Deploy
docker-compose -f docker-compose.prod.yml up -d

# Verify deployment
curl https://your-domain.com/health
```

## How to contribute

1. Fork the repo and create a branch for your change.
2. Install and run the app locally:

```cmd
copy .env.example .env
npm install
npm run dev
```

3. Run tests and linters before submitting a PR:

```cmd
npm run test
npm run lint
```

4. Open a PR describing the change and linking related issues.

See `docs/CONTRIBUTING.md` for detailed guidelines.

## Docs & quick links

- Features · docs/FEATURES.md
- Architecture · docs/ARCHITECTURE.md
- Configuration · docs/CONFIGURATION.md
- API · docs/API.md
- CLI · docs/CLI.md
- Development · docs/DEVELOPMENT.md
- Security · docs/SECURITY.md
- Troubleshooting · docs/TROUBLESHOOTING.md

## Support

- Issues: https://github.com/MIKTHATGUY/WallWhale/issues
- Docs: `docs/` folder in this repository

## Acknowledgements

Built for the Steam Workshop community. Thanks to contributors listed on the GitHub contributors tab.

---

If anything is unclear, open an issue and we’ll help you get started.

- **🔐 Enterprise Security** - JWT authentication, API keys, role-based access, audit logging
- **⚡ High Performance** - Concurrent downloads, intelligent queuing, rate limiting
- **🏗️ Production Ready** - Docker support, health checks, monitoring, auto-scaling
- **🎮 Steam Integration** - Multi-account support, workshop downloads, automated authentication
- **📊 Monitoring** - Prometheus metrics, structured logging, real-time health checks
- **🔧 Developer Friendly** - TypeScript, comprehensive testing, modular architecture

## 🚀 Quick Start

### Docker (Recommended)

```bash
# Clone the repository
git clone https://github.com/wallwhale/wallwhale.git
cd wallwhale

# Start with Docker Compose
docker-compose up -d

# Check health
curl https://localhost:3000/health
```

### Local Development

```bash
# Install dependencies
npm install

# Set up environment
cp .env.example .env
# Edit .env with your configuration

# Initialize database
npm run db:generate
npm run db:push
npm run db:seed

# Generate certificates (development)
npm run cert:mkcert

# Start development server
npm run dev
```

## 🏗️ Architecture

**Enterprise-grade microservice architecture:**

- **API Server** - Fastify-based REST API with OpenAPI documentation
- **Download Engine** - Multi-threaded WallWhale integration
- **Database Layer** - Prisma ORM with PostgreSQL/SQLite support
- **Authentication** - JWT + API key dual authentication system
- **Monitoring** - Prometheus metrics, structured logging, health checks
- **Security** - TLS encryption, rate limiting, audit trails

## 📚 Documentation

### Quick Links
- **[Features](docs/FEATURES.md)** - Enterprise features and capabilities
- **[Architecture](docs/ARCHITECTURE.md)** - System design and components  
- **[API Reference](docs/API.md)** - Complete API documentation
- **[Configuration](docs/CONFIGURATION.md)** - Environment setup and options
- **[Security](docs/SECURITY.md)** - Security model and best practices
- **[Development](docs/DEVELOPMENT.md)** - Development setup and workflow
- **[CLI Tools](docs/CLI.md)** - Command-line interface and automation
- **[Troubleshooting](docs/TROUBLESHOOTING.md)** - Common issues and solutions
- **[Contributing](docs/CONTRIBUTING.md)** - How to contribute to the project

### Core Documentation
- **Configuration**: Environment variables, database setup, TLS certificates
- **API Usage**: Authentication, endpoints, rate limiting, error handling
- **Security**: Encryption, network security, audit logging, best practices
- **Operations**: Deployment, monitoring, scaling, maintenance
- **Development**: Local setup, testing, code standards, workflows

## 🔧 CLI Tools

Comprehensive command-line interface for server management:

```bash
# Certificate management
npm run cert:setup              # Interactive certificate wizard
npm run cert:mkcert            # Generate trusted dev certificates
npm run cert:letsencrypt       # Production Let's Encrypt certificates

# Direct downloads (no server required)
npm run cli download direct -i "123456789" -a "steam_account"

# File hosting and sharing
npm run cli download host -i "123456789" -p 8080 --password "secret"

# Server management
npm run health                 # Health check
npm run config:validate        # Validate configuration
npm run db:migrate            # Database migrations
```

## 🛠️ API Usage

### Authentication

```bash
# Using API Key
curl -H "Authorization: Bearer your-api-key" \
     https://localhost:3000/v1/downloads

# Using JWT Token
curl -H "Authorization: Bearer jwt-token" \
     https://localhost:3000/v1/downloads
```

### Download Workshop Item

```bash
curl -X POST https://localhost:3000/v1/downloads \
  -H "Authorization: Bearer your-api-key" \
  -H "Content-Type: application/json" \
  -d '{
    "workshopId": "123456789",
    "steamAccount": "your_steam_account"
  }'
```

### Monitor Download

```bash
# Get download status
curl https://localhost:3000/v1/downloads/download-id \
  -H "Authorization: Bearer your-api-key"

# Stream real-time logs
curl https://localhost:3000/v1/downloads/download-id/logs \
  -H "Authorization: Bearer your-api-key" \
  -H "Accept: text/event-stream"
```

## 🔐 Security Features

- **Multi-Layer Authentication** - JWT tokens + API keys with scope-based permissions
- **TLS Encryption** - End-to-end encryption with Let's Encrypt integration
- **Rate Limiting** - Configurable per-user and global rate limits
- **Audit Logging** - Comprehensive audit trail for all operations
- **Input Validation** - Strict input validation and sanitization
- **Network Security** - CORS configuration, secure headers, IP whitelisting

## 📊 Monitoring & Operations

- **Health Checks** - `/health` endpoint with detailed system status
- **Metrics** - Prometheus metrics for performance monitoring
- **Logging** - Structured JSON logging with configurable levels
- **Auto-Scaling** - Docker Compose and Kubernetes support
- **Backup** - Automated database and configuration backups

## 🌐 Deployment Options

### Docker Compose (Production)
```bash
# Production deployment
docker-compose -f docker-compose.prod.yml up -d

# With external database
docker-compose -f docker-compose.external-db.yml up -d
```

### Kubernetes
```bash
# Deploy to Kubernetes
kubectl apply -f k8s/

# Scale deployment
kubectl scale deployment wallwhale-server --replicas=3
```

### Traditional Server
```bash
# Production build
npm run build

# Start production server
npm run start:prod
```

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guide](docs/CONTRIBUTING.md) for details on:

- **Development Setup** - Local environment configuration
- **Coding Standards** - TypeScript style guide and best practices
- **Testing Guidelines** - Unit, integration, and e2e testing
- **Pull Request Process** - Code review and merge workflow

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

- **Documentation**: Check the `/docs` directory for comprehensive guides
- **Issues**: Report bugs and request features on [GitHub Issues](https://github.com/wallwhale/wallwhale/issues)
- **Discussions**: Ask questions in [GitHub Discussions](https://github.com/wallwhale/wallwhale/discussions)
- **Troubleshooting**: See [Troubleshooting Guide](docs/TROUBLESHOOTING.md) for common issues

## 🏆 Enterprise Ready

WallWhale is designed for enterprise environments with:

- **High Availability** - Multi-instance deployment with load balancing
- **Scalability** - Horizontal scaling with Docker and Kubernetes
- **Security** - Enterprise-grade security features and audit compliance
- **Monitoring** - Production-ready observability and alerting
- **Support** - Comprehensive documentation and community support

---

**Built with ❤️ for the Steam Workshop community**
