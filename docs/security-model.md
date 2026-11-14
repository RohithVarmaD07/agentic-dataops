# DataOps security model

Status: proposed controls, not implemented protections.

## Assets and trust boundaries

Protect source files, local credentials, approved evidence, incident history, tool authorization, model configuration, and evaluation integrity. Evidence payloads, logs, code comments, model outputs, and suggested patches are untrusted. The owner and native approval mechanism are the authority for consequential actions.

| Threat | Planned control | Required verification |
| --- | --- | --- |
| Instructions embedded in logs | Separate evidence from policy; structured outputs; enforced tool allowlist | Injection suite cannot cause extra permissions or prohibited calls |
| Path traversal and symlink escape | Resolve paths under approved roots; reject links outside roots | Adversarial path fixtures rejected before file access |
| Arbitrary shell/SQL execution | Named diagnostic operations with typed arguments; no free-form shell tool; read-only bounded queries | Disallowed operations fail closed |
| Credential or data exposure | Synthetic-only input, redaction, no outbound network by default, loopback API | Seeded sensitive markers absent from output and model requests |
| Resource exhaustion | Payload, query, output, token, step, process, disk, and time budgets | Each limit terminates safely with an audit record |
| Untrusted candidate tests | Approved sandbox with filesystem/process/network restrictions and no secrets | Canary tests demonstrate denied access; otherwise execution remains blocked |
| Evidence tampering | Hash verification, evidence index, transactional state, provenance | Modified artifacts rejected; local hashes do not prove external authenticity |
| Unauthorized fix application | Recommendations only; original workspace immutable during validation | Original hashes unchanged and explicit approval required for application |
| Dependency/supply-chain risk | Reviewed versions/licenses, lockfiles, pinned Actions, least-privilege CI | Approved scans and lockfile reproduction before release |

## Initial budgets to validate

Proposed starting bounds: 64 KiB event payload, 50 evidence references/event, 1 MiB text/evidence read, 10 diagnostic steps, 30 seconds/diagnostic operation, 120 seconds/investigation, and 5 minutes/candidate validation. Tune only using measured workloads. Model token/context limits depend on the approved model and must be recorded. Truncation must be visible rather than presented as complete evidence.

API binds to loopback initially. No remote access, authentication deployment, browser-exposed execution endpoint, or production credentials. Add authentication and authorization before any approved shared hosting. Do not treat CORS as authentication.

Audit logs record who/what initiated a transition, accepted tool arguments, sanitized results, source/evidence hashes, denied requests, and resource-limit outcomes. They do not store secrets or unlimited raw prompts. Retention and export redaction must be documented before running a public demonstration.

Phase 1 changes no host security settings, installs no sandbox, and grants no extra agent permissions. Existing approval requirements remain enabled.
