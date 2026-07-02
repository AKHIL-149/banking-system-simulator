# Banking System Simulator

A real-time, event-driven banking platform showcasing cloud-native architecture, microservices, and transparent financial operations.

## Description

Real-time event-driven banking platform built with microservices architecture. Features event sourcing, CQRS, and live transaction processing with fraud detection. Tech stack: TypeScript, Node.js, PostgreSQL, RabbitMQ, React Native. Demonstrates cloud-native design, scalability, and production-ready patterns for distributed systems.

## Architecture

Event-Driven Microservices with Event Sourcing & CQRS patterns.

## Tech Stack

- **Backend**: Node.js, TypeScript, Express
- **Databases**: PostgreSQL (Event Store + Read Models)
- **Message Queue**: RabbitMQ
- **Cache**: Redis
- **Clients**: React Native (Mobile), React (Web)
- **DevOps**: Docker, Kubernetes

## Getting Started

```bash
# Install dependencies
npm install

# Start infrastructure
docker-compose up -d

# Start services
npm run dev
```

## License

MIT License - Portfolio/Learning Project
