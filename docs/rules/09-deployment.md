# CI/CD & Production Release Standards

Defines the pipeline, containerization, and observability requirements.

## 1. CI/CD Pipeline Standards
- **Pipeline Trigger:** Code push to `main` triggers the staging pipeline. Tag creation triggers the production pipeline.
- **Stages:**
    1.  **Build:** Build Docker image.
    2.  **Test:** Run Unit/Integration tests.
    3.  **Security Scan:** Vulnerability scanning.
    4.  **Deploy:** Deploy.
- **Rollback:** The pipeline must support one-click rollback to the previous image tag.

## 2. Containerization Norms
- **Base Image:** Use `distroless` or `alpine` for minimal attack surface.
- **User:** The application must run as a non-root user inside the container.
- **Read-Only:** Root filesystem must be read-only. Logs must be written to `stdout/stderr`.
- **Image Tagging:** Use Git commit SHA for immutable tags.

## 3. Rolling Update Rules
- **Strategy:** RollingUpdate with `maxSurge: 25%` and `maxUnavailable: 0` to ensure zero downtime.
- **Readiness Probe:** The new pod must pass the readiness probe before traffic is routed to it.
- **Resource Limits:** Define `requests` and `limits` for CPU and Memory.

## 4. Observability Requirements
- **Logging:** JSON structured logging. All logs must include `traceId`, `serviceName`, and `environment`.
- **Metrics:** Expose `/metrics` endpoint for Prometheus scraping. Track: Request Rate, Error Rate, and Latency (RED method).
- **Alerting:** Define SLOs. Alerts must trigger if Error Rate > 5% for 5 minutes.
