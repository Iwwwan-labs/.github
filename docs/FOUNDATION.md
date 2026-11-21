# Iwwwan-labs organization foundation

**Status:** Initial operating charter  
**Business model:** Hybrid — client services and an owned product studio  
**First operating priority:** Engineering foundation

## Mission

Iwwwan-labs is the parent organization for software engineering, AI-enabled delivery, client engagements, and independently owned digital products. We use a shared engineering system so client work and internal products can move quickly without weakening quality, security, or ownership.

## Business model

The organization operates through two complementary tracks:

1. **Agency services** — discovery, design, engineering, integration, automation, and ongoing delivery for clients.
2. **Product studio** — research, build, launch, and operate products owned by Iwwwan-labs.

Both tracks use the same engineering standards and delivery controls. Client-specific data, credentials, intellectual property, and deployment environments must remain isolated from internal products and from other clients.

## Repository taxonomy

| Pattern | Purpose | Default visibility | Current status |
| --- | --- | --- | --- |
| `.github` | Organization profile, shared community files, conventions, reusable workflows | Public | Exists |
| `website` | Public organization website | Public | Exists |
| `template-*` | Reusable project starters | Public | `template-web`, `template-service`, `template-mobile` exist |
| `clients-*` | Client-specific delivery repositories | Private | Future convention; none confirmed |
| `internal-*` | Internal tools, automation, and operations | Private | Future convention; none confirmed |
| Product repositories | Independently operated Iwwwan-labs products | Decide per product | Existing product repositories must be inventoried before migration |

Repository names use lowercase kebab-case. Existing repositories are preserved; renaming, transferring, archiving, or changing visibility requires a separate explicit decision.

## Operating principles

- **Private by default for sensitive work.** Client work, internal operations, credentials, and non-public product plans belong in private repositories.
- **Least privilege.** Give people and automations only the access needed for their task.
- **Pull requests as the change boundary.** Work on feature branches, run checks, review diffs, then merge.
- **Human approval for consequential actions.** AI agents may inspect issues, implement scoped changes, run checks, push feature branches, and open pull requests. They must not merge, deploy, change repository/org security settings, permissions, or secrets without explicit approval.
- **Traceability.** Work should link to an issue, pull request, decision record, or release.
- **Separation of duties.** Client assets and secrets must not be copied into shared templates, public repositories, logs, or unrelated projects.
- **Small reversible changes.** Prefer incremental pull requests over broad, hard-to-review changes.

## Delivery lifecycle

1. Capture the request as an issue with scope and acceptance criteria.
2. Triage priority, workstream (agency, product, platform), risk, and owner.
3. Assign an engineer or agent with minimum required access.
4. Implement on a dedicated branch and run relevant checks.
5. Open a pull request with test evidence and linked issue.
6. Review the diff and CI results.
7. Obtain explicit human approval before merge; obtain separate approval before deployment where applicable.
8. Record release and operational follow-up.

## Initial organization workstreams

| Workstream | Responsibility | Initial focus |
| --- | --- | --- |
| Foundation | Governance and engineering platform | Repository map, standards, templates, CI, access and security review |
| Agency | Client delivery | Repeatable discovery-to-delivery process; isolate each client |
| Product studio | Owned products | Product selection, validation, roadmap, and product-specific repositories |
| AI engineering | Agent-assisted delivery | Scoped agent roles, permissions, review gates, and audit trail |

## Stage 1 — Foundation exit criteria

- [x] Confirm hybrid business model and foundation-first priority.
- [x] Inventory the current organization repositories.
- [ ] Validate repository purpose, visibility, metadata, and template flags.
- [ ] Align organization profile and repository documentation with the actual state.
- [ ] Standardize issue and pull request intake.
- [ ] Review CI workflows and required checks for each repository.
- [ ] Review access, branch protection, secret scanning, dependency security, and vulnerability reporting settings.
- [ ] Document agent permissions and human approval gates.
- [ ] Establish a single organization-level project/operations view.

Items that require GitHub organization or repository settings changes are audit-only until explicitly approved and applied.

## Current repository inventory

The initial audit found five public repositories, each using `main` as its default branch:

- `.github`
- `website`
- `template-web`
- `template-service`
- `template-mobile`

This inventory is a point-in-time snapshot. Update it when repositories are created, transferred, archived, or change visibility.

## Decision log

| Decision | Outcome |
| --- | --- |
| Organization role | Parent organization for engineering, agency, and owned products |
| Business model | Hybrid: agency services + product studio |
| First priority | Foundation |
| Existing repositories | Preserve; no bulk migration or renaming |
| AI agent changes | Feature branch and pull request workflow |
| Merge and deployment | Explicit human approval required |
| Security, permissions, and secrets | No changes without explicit approval |
