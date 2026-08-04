# CI/CD & Production Release Standards

Defines the pipeline, containerization, and observability requirements.

## 1. CI/CD Pipeline Standards
- **Pipeline Trigger:** Code push to `main` triggers the staging pipeline. Tag creation triggers the production pipeline.
- **Stages:**
  1. **Lint** Statically analyzes source codes.
  2. **Test** Runs unit and integration tests.
  3. **Build** Compiles code, bundles assets,
  4. **Scan** Performs security & vulnerability checks.
  5. **Stage** Deploys artifact for final live‑environment validation.
  6. **e2e** Runs end-to-end user-journey tests.
  7. **Deploy** Promotes to production .
- **Rollback:** The pipeline must support one-click rollback to the previous image tag.
- **Artifact Repository:** Push Docker images to AWS ECR / GAR / Docker Hub with Git SHA tags.
- **Deployment Strategy:** Blue/Green or Canary deployments for zero-downtime releases.
- **Feature Flags:** Integrate LaunchDarkly / Flagsmith to decouple deployment from release.


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
- **Alerting:** Define SLOs. Alerts must trigger if Error Rte > 5% for 5 minutes.
