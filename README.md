# 🚀 WallWhale

A production-ready enterprise server for Steam Workshop content downloads, built with Node.js, TypeScript, and Fastify. Features secure API access, multi-account management, real-time monitoring, and comprehensive audit logging.

## ✨ Key Features

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
