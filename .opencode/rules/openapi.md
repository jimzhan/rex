# RESTful API Design Instructions

Maintain a predictable, secure, and deterministic RESTful API surface optimized for both human developers and AI tool-calling clients.

## 1. Core Architectural Constraints
* **State Management**: All endpoints must be completely stateless. Session data must not be stored on the server.
* **Controller Pattern**: Use final, single-action invokable controllers (one class/file per endpoint).
* **ID Strategy**: Never use auto-incrementing integer IDs. Expose only cryptographically secure UUIDv7 or ObjectId to the client.

## 2. Resource Naming & URI Conventions
* **Casing**: Use `kebab-case` for all URI paths (e.g., `/api/users`).
* **Nouns**: Path segments must use plural nouns to represent resources (e.g., `/api/books`, not `/api/getBook`).
* **Nesting**: Limit resource nesting to a maximum of one level deep (e.g., `/api/authors/{id}/books`). For deeper relationships, flatten the path and use query filters.

## 3. Request & Response Standardization
* **Payload Format**: All request bodies and response envelopes must use `camelCase` JSON fields.
* **HTTP Methods**: Enforce strict semantic mapping:
  * `GET`: Fetch resource(s). Must be idempotent and side-effect free.
  * `POST`: Create a resource. Non-idempotent.
  * `PUT`: Replace a resource entirely or create it if the ID is client-generated. Idempotent.
  * `PATCH`: Partially update a resource. Non-idempotent.
  * `DELETE`: Remove a resource. Idempotent.
* **Discovery Route**: Provide a front-door `GET /api/discover` endpoint returning column types, validation constraints, and schema metadata so LLMs can dynamically map capabilities.

## 4. Error Handling & Machine Readability
All non-2xx responses must return a standardized JSON error object following the RFC 7807 (Problem Details) specification:
```json
{
  "type": "https://example.com",
  "title": "Bad Request",
  "status": 400,
  "detail": "The provided email address is already registered.",
  "instance": "/api/v1/users",
  "errors": {
    "email": ["Must be a valid, unique email address."]
  }
}
```

## 5. Security & Rate Limiting Guardrails
* **Least Privilege**: Generate tightly-scoped, short-lived tokens. Avoid broad "admin" tokens.
* **Rate Limits**: Implement standard tier limits. Always return machine-actionable rate limit headers:
  * `X-RateLimit-Limit`
  * `X-RateLimit-Remaining`
  * `X-RateLimit-Reset`
* **429 Handling**: Ensure `429 Too Many Requests` responses include a `Retry-After` header to prevent AI client retry storms.

## 6. Versioning & Deprecation Policy
* **Versioning**: Route via `X-Api-Version` header. Missing/invalid → latest version. Valid (e.g., v1) → specific version. URL stays `/api/resources`.
* **Sunset**: On deprecation, inject RFC 8594 Sunset header via middleware with the exact removal date.

## 7. Verification & Definition Workflows
* Every route modification requires a corresponding update to the OpenAPI 3.1 schema definition file (`/docs/openapi.yaml`).
* Ensure all schemas are explicit, fully descriptive, and block unknown properties (`additionalProperties: false`) to safeguard against LLM hallucinations.

