# Banking System Simulator

A real-time event-driven banking platform built with microservices architecture, demonstrating event sourcing, CQRS, and live transaction processing with fraud detection capabilities.

## Overview

This project showcases production-ready patterns for building scalable, distributed financial systems. It implements event sourcing for complete audit trails, CQRS for optimized read/write operations, and microservices architecture for independent scaling and deployment.

The system processes transactions in real-time, maintains complete transaction history through event sourcing, and provides fraud detection capabilities through rule-based scoring.

## Technology Stack

**Backend Services**
- Node.js with TypeScript
- Express for REST APIs
- PostgreSQL for event store and read models
- RabbitMQ for event-driven messaging
- Redis for caching and session management

**Architecture Patterns**
- Event Sourcing - Complete audit trail with event replay
- CQRS - Separate read and write models
- Microservices - Independently deployable services
- Domain-Driven Design - Rich domain models and aggregates

**Infrastructure**
- Docker for containerization
- Docker Compose for local development
- Kubernetes-ready deployment manifests

## Core Features

### Event Sourcing
Every state change is recorded as an immutable event, providing a complete audit trail and enabling time-travel debugging. Events can be replayed to rebuild application state or create new read models.

### CQRS Architecture
Commands modify state through domain aggregates, while queries read from optimized denormalized views. This separation allows independent scaling and optimization of read and write operations.

### Real-time Processing
Transactions are processed asynchronously through an event bus, enabling real-time balance updates and notifications across all connected clients.

### Fraud Detection
Rule-based fraud detection analyzes transaction patterns, velocity, and amounts to generate risk scores and automatically flag suspicious activity.

### Multi-Currency Support
Native support for multiple currencies (USD, EUR, GBP, JPY, INR) with transaction processing and balance tracking.

## Project Structure

```
banking-system-simulator/
├── libs/
│   ├── domain-models/     - Events, types, aggregates, value objects
│   ├── event-store/       - Event sourcing infrastructure
│   ├── event-bus/         - RabbitMQ messaging layer
│   └── common-utils/      - Shared utilities
├── services/
│   ├── account-service/   - User accounts and authentication
│   ├── transaction-service/ - Payment processing
│   ├── fraud-detection/   - Fraud scoring and alerts
│   └── notification-service/ - Email, SMS, push notifications
├── apps/
│   ├── mobile/            - React Native application
│   ├── web/               - React web application
│   └── admin-dashboard/   - System monitoring
├── infrastructure/
│   ├── docker/            - Docker configurations
│   ├── kubernetes/        - K8s deployment manifests
│   └── terraform/         - Infrastructure as code
└── docs/                  - Architecture and API documentation
```

## Getting Started

### Prerequisites

- Node.js 18 or higher
- Docker and Docker Compose
- PostgreSQL 14+ (provided via Docker)
- RabbitMQ 3.11+ (provided via Docker)

### Installation

Clone the repository:
```bash
git clone https://github.com/AKHIL-149/banking-system-simulator.git
cd banking-system-simulator
```

Start the infrastructure services:
```bash
docker-compose up -d
```

Install dependencies and build shared libraries:
```bash
npm install
npm run build
```

Start the Account Service:
```bash
cd services/account-service
npm install
npm run dev
```

The service will be available at http://localhost:3001

### Testing the API

Register a new user:
```bash
curl -X POST http://localhost:3001/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "email": "user@example.com",
    "password": "SecurePassword123!",
    "fullName": "John Doe",
    "phone": "+1234567890"
  }'
```

Login to receive an authentication token:
```bash
curl -X POST http://localhost:3001/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "user@example.com",
    "password": "SecurePassword123!"
  }'
```

Create a new account (replace TOKEN with the JWT from login):
```bash
curl -X POST http://localhost:3001/api/accounts \
  -H "Authorization: Bearer TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "accountType": "checking",
    "currency": "USD",
    "initialDeposit": 1000
  }'
```

## Architecture

The system follows a microservices architecture with event-driven communication. Services publish domain events to RabbitMQ, which other services consume to update their read models or trigger workflows.

### Event Flow

1. Client sends command to service (e.g., create account)
2. Service loads aggregate from event store
3. Aggregate validates command and generates events
4. Events are persisted to event store
5. Events are published to event bus
6. Subscribed services update read models
7. WebSocket server broadcasts to connected clients

### Data Flow

**Write Path (Commands)**
- Client → API Gateway → Service
- Service → Event Store (write events)
- Service → Event Bus (publish events)

**Read Path (Queries)**
- Client → API Gateway → Service
- Service → Read Database (optimized views)

## Security

- JWT-based authentication with configurable expiration
- Password hashing using bcrypt with salt rounds
- Rate limiting to prevent abuse
- CORS configuration for cross-origin requests
- Input validation using Joi schemas
- Parameterized SQL queries to prevent injection
- Environment-based configuration for secrets

## Scalability

The architecture supports horizontal scaling of all services:

- Stateless services can run multiple instances
- Event bus distributes work across consumers
- Read models can be replicated for query scaling
- Database sharding strategies for event store
- Redis caching layer reduces database load

## Development Roadmap

**Phase 1: Foundation (Complete)**
- Domain models and events
- Event store infrastructure
- Event bus implementation
- Account service with authentication

**Phase 2: Core Services (In Progress)**
- Transaction service
- Fraud detection service
- Notification service
- API gateway

**Phase 3: Real-time Features**
- WebSocket server
- Event stream visualization
- Live balance updates

**Phase 4: Client Applications**
- React Native mobile app
- React web application
- Admin dashboard

**Phase 5: Production Readiness**
- Kubernetes deployment
- CI/CD pipeline
- Monitoring and alerting
- Load testing

## Documentation

- [Architecture Documentation](docs/ARCHITECTURE.md) - Detailed system design
- [Getting Started Guide](GETTING_STARTED.md) - Setup and development
- [Progress Tracker](PROGRESS.md) - Current status and roadmap
- [API Documentation](docs/API.md) - REST API reference

## Testing

```bash
# Run unit tests
npm run test

# Run integration tests
npm run test:integration

# Run end-to-end tests
npm run test:e2e

# Generate coverage report
npm run test:coverage
```

## License

MIT License - This is a portfolio and learning project.

## Technical Highlights

This project demonstrates practical experience with:

- Event-driven architecture and message queuing
- Event sourcing and CQRS patterns
- Microservices design and implementation
- Domain-driven design principles
- TypeScript for type-safe development
- PostgreSQL for transactional consistency
- Real-time data streaming
- RESTful API design
- Authentication and authorization
- Docker containerization
- Infrastructure as code

The codebase follows SOLID principles, implements proper error handling, includes comprehensive logging, and is designed for horizontal scalability and fault tolerance.
