## Change summary
Describe what changed and why.

## Related task and task class
Issue/task ID:
Task class: documentation / bug fix / feature / refactor / infrastructure / security

## Scope and acceptance criteria
- [ ] Scope is documented and limited to the intended change.
- [ ] Each acceptance criterion is addressed.
- [ ] Out-of-scope behavior and known limitations are stated.

## Verification
- [ ] Relevant tests and checks were run; commands and actual results are recorded.
- [ ] Required CI checks pass (if configured for this repository).
- [ ] Important edge cases and failure paths were reviewed.
- [ ] Documentation/configuration was updated where necessary.

## Security, privacy and operations
- [ ] Security, privacy, and data-handling implications were considered for affected markets.
- [ ] No secrets, credentials, or private customer data were committed.
- [ ] Database, infrastructure, and destructive changes have explicit authorization and rollback/recovery consideration.
- [ ] Existing deployment workflows and production resources are preserved.
- [ ] Deployment status is described separately from merge acceptance.

## AI assistance (complete when AI tools materially contributed)
- [ ] AI tool/model and relevant configuration are recorded in the company measurement log.
- [ ] Generated changes were independently reviewed against acceptance criteria.
- [ ] Human corrections and verification effort are recorded.
- [ ] Rework, if any, is classified: Spec gap / Agent error / Requirements change / Unknown.

## Human acceptance
- [ ] A human reviewer verified the implementation against acceptance criteria.
- [ ] Relevant test evidence and material risks were reviewed.
- [ ] Approval for merge is explicit.

**Reminder:** Generated code, passing tests, or an opened PR alone do not constitute acceptance. Production deployment is a separate verified milestone.

## Data engineering and AI Core reporting (when applicable)

- [ ] Data sources, schemas/contracts, quality checks, retention, lineage, and recovery implications were considered where applicable.
- [ ] Any new data technology is justified by workload requirements, operational ownership, security, and total cost; no technology is added solely because it appears in the company reference catalogue.
- [ ] AI Core / engineering measurement events contain only authorized, minimized engineering metadata and exclude customer, financial, identity, voice, credential, and regulated payloads by default.
- [ ] Measurement submission is authenticated, scoped, auditable, and safe to retry; product data and engineering telemetry remain access-controlled and logically separated.
