# Constitution
---
description: Guiding principles from 12factor.net for software. **DO NOT** change it. 
---

1. **Codebase** – Maintain a single codebase per application, tracked in version control, with multiple deploys across distinct environments.
2. **Dependencies** – Explicitly declare and isolate all dependencies, never relying on implicit system-wide packages.
3. **Config** – Store all configuration that varies between environments (credentials, endpoints, etc.) in environment variables, not in code.
4. **Backing Services** – Treat all external services (databases, caches, message queues) as attached resources, swappable via configuration without code changes.
5. **Build, Release, Run** – Strictly separate the build (transform code into executable bundle), release (combine build with config), and run (execute the app) stages.
6. **Processes** – Execute the application as one or more stateless, share-nothing processes, with persistent data stored solely in backing services.
7. **Port Binding** – Export services by binding to a port and listening for incoming requests, making the app self-contained as a web server.
8. **Concurrency** – Scale horizontally by running multiple process types (e.g., web, worker) and leveraging the operating system's process model.
9. **Disposability** – Maximize robustness by enabling fast startup and graceful shutdown, allowing processes to be instantly terminated or restarted.
10. **Dev/Prod Parity** – Keep development, staging, and production environments as similar as possible to minimize time gaps and configuration drift.
11. **Logs** – Treat log output as a continuous stream of time-ordered events, writing to stdout and leaving aggregation and routing to the execution environment.
12. **Admin Processes** – Run one-off administrative or maintenance tasks (e.g., database migrations, console scripts) in the exact same environment as the regular long-running processes.
