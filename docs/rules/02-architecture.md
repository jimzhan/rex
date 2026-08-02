# Architecture Guidelines: Distributed Systems Design

Defines the structural blueprint for large-scale distributed web applications.

## 1. Layering & Component Boundaries
- **Strict 4-Tier Separation:**
  1.  **Presentation:** Handles HTTP/WebSocket interactions (e.g., Controllers/Gateways).
  2.  **Application:** Orchestrates use cases (e.g., Services/Handlers).
  3.  **Domain:** Contains core business logic, entities, and value objects. **Must not** have external dependencies.
  4.  **Infrastructure:** Implements interfaces for persistence, messaging, and external APIs.
- **Dependency Inversion:** High-level modules must not depend on low-level modules. Both must depend on abstractions (Interfaces/Abstract Classes).
- **Bounded Contexts:** Services must communicate via well-defined APIs, not direct database access or shared internal libraries (except common utilities).

## 2. High-Availability & Fault Tolerance
- **Health Checks:** Implement `/health` endpoints. Pods must fail liveness probes if degraded.
- **Circuit Breakers:** Use circuit breakers for all external API calls. Fallback mechanisms must be defined for critical paths.
- **Retry with Backoff:** Implement exponential backoff and jitter for transient failures. Idempotency keys are mandatory for state-changing operations.

## 3. Scalability Principles
- **Statelessness:** Services must be horizontally scalable. Session state must be externalized to Redis/Memcached.
- **Queueing:** Offload long-running tasks (e.g., report generation, email sending) to asynchronous workers via Message Queues (e.g., RabbitMQ, SQS).

