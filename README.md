> Local publication candidate. Read [release boundaries](PUBLICATION.md) before use or publication.

# Agentic DataOps

Status: Phase 1 architecture, security, and evaluation specifications only. Monitoring, agents, APIs, model inference, and fix validation are not implemented or verified.

The platform will consume MediFlow telemetry, detect anomalies, investigate failures using traceable evidence, recommend fixes, and validate candidates in isolation. It will also run independently against packaged synthetic incident fixtures.

## Documents

- [Architecture and event compatibility](docs/architecture.md)
- [Security model](docs/security-model.md)
- [AI evaluation plan](docs/evaluation-plan.md)
- [Acceptance scenarios](docs/acceptance-scenarios.md)
- [Security policy](SECURITY.md)

## Planned stack and execution

Python, FastAPI, SQLite, explicit agent state transitions, statistical detectors, and an optional local inference provider. There are no application commands, dependencies, model artifacts, build backend, or lockfiles yet. Runtime compatibility must be tested after installation approval.

Current CI is a manual foundation metadata check draft, not an application test suite or security scanner. It has not run on GitHub. Dependency update proposals are disabled in the draft; separate security-update settings require review.

## Independence and operating policy

This folder will become `agentic-dataops` through a reviewed copy-only export. It must not import MediFlow implementation or rely on sibling files at runtime. A later approved contract snapshot will include the canonical MediFlow schema version, source revision, and hash. Self-contained incident fixtures will support reproduction without AWS or model downloads.

Treat external records/logs as untrusted data. No unrestricted shell tools, arbitrary SQL, network access, automatic patch application, paid inference, model downloads, installation, or publication without approval. Every AI capability needs an implemented model path and held-out evaluation; deterministic diagnostics and replays must be labeled. There is no claim of autonomous remediation or production deployment.

## License

Original covered materials use the [MIT License](LICENSE), Copyright (c) 2026 Rohith Varma. Read the [scope and exclusions](LICENSE_SCOPE.md) and [third-party review](THIRD_PARTY.md). This is an architecture-stage project, not an executable application. These files are prepared locally; publication still requires owner approval.
