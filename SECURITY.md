# Security policy

No supported release, running API, or remote service exists. The [security model](docs/security-model.md) specifies planned controls; they are not yet implemented or tested.

Use synthetic telemetry and local evidence only. Never submit credentials, real patient data, or private logs to a model. Untrusted evidence cannot grant tools, change policy, or authorize execution. Default model-provider mode is disabled until an approved provider is implemented and evaluated.

No automatic application of fixes to the original workspace, Git history, remote repository, or deployed service. A validated recommendation is not approval to apply it. Diagnostic tools must be allowlisted and bounded; patch verification requires a genuine process/resource/network boundary, not merely a temporary directory.

Security checks, dependency scans, injection tests, and private vulnerability reporting configuration are release prerequisites. No scanner has run. Keep findings private for owner review; a verified private reporting channel must be configured before publication. Do not invent an email address or claim a response SLA.
