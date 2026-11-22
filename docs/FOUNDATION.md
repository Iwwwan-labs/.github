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
| `template-*` | Reusable project starters copied for new work | Public | `template-web`, `template-service`, `template-mobile` exist |
| `clients-*` | Client-specific delivery work | Private | Future convention; none confirmed |
| `internal-*` | Internal tools, automation, and operations | Private | Future convention; none confirmed |
| Product repositories | Independently operated Iwwwan-labs products | Decide per product | Existing product repositories must be inventoried before migration |

Repository names use lowercase kebab-case. Existing repositories are preserved; renaming, transferring, archiving, or changing visibility requires a separate explicit decision.

## Operating principles

- **Private by default for sensitive work.** Client work, internal operations, credentials, and non-public product plans belong in private repositories.
- **Least privilege.** Give people and automations only the access needed for their task.
- **Pull requests as the change boundary.** Work on feature branches, run checks, review diffs, then merge.
- **Single-maintainer governance.** `iwwwan-io` is currently the sole human maintainer. Rulesets do not require PR approval or Code Owner review because a second independent reviewer is not available.
- **Human control of consequential actions.** AI agents may inspect issues, implement scoped changes, run checks, push feature branches, and open pull requests. They must not merge, deploy, change repository/org security settings, permissions, or secrets without explicit approval from `iwwwan-io`.
- **Traceability.** Work should link to an issue, pull request, decision record, or release.
- **Separation of duties.** Client assets and secrets must not be copied into shared templates, public repositories, logs, or unrelated projects.
- **Small reversible changes.** Prefer incremental pull requests over broad, hard-to-review changes.

## Delivery lifecycle

1. Capture the request as an issue with scope and acceptance criteria.
2. Triage priority, workstream (agency, product, platform), risk, and owner.
3. Assign an engineer or agent with minimum required access.
4. Implement on a dedicated branch and run relevant checks.
5. Open a pull request with test evidence and linked issue.
6. The maintainer reviews the diff, scope, and required CI/security check results.
7. The maintainer explicitly decides whether to merge. Deployment requires a separate explicit approval.
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
- [x] Validate repository purpose, visibility, metadata, and template flags.
- [x] Establish active main-branch rulesets on all five repositories.
- [x] Configure required CI and CodeQL checks on the three templates and required website static checks.
- [x] Configure Dependabot and push-protection controls on the repositories, based on maintainer confirmation; feature availability and secret-scanning status still require a separate verified inventory.
- [x] Document single-maintainer governance and AI-agent approval boundaries.
- [ ] Standardize issue and pull request intake.
- [ ] Complete the security-settings evidence inventory, including secret scanning and alert status where API/UI evidence is available.
- [ ] Establish a single organization-level project/operations view.

Settings that require GitHub organization or repository changes remain subject to explicit maintainer approval.

## Current repository inventory

The organization currently has five public repositories, all using `main` as the default branch, not archived, and with Issues enabled. The following snapshot was checked on 2026-11-22.

| Repository | Purpose | GitHub template flag | Active main ruleset | Required status checks |
| --- | --- | --- | --- | --- |
| `.github` | Organization profile and shared standards | Off | Yes | None configured |
| `website` | Public organization website | Off | Yes | `Static website checks` |
| `template-web` | Web project starter | On | Yes | `verify / verify`, `analyze / Analyze JavaScript and TypeScript` |
| `template-service` | Service project starter | On | Yes | `verify / verify`, `analyze / Analyze JavaScript and TypeScript` |
| `template-mobile` | Mobile project starter | On | Yes | `verify / verify`, `analyze / Analyze JavaScript and TypeScript` |

All five active rulesets block branch deletion and non-fast-forward updates. All five use zero required approving reviews, consistent with the current single-maintainer model. Required status checks are enforced on the website and three templates; `.github` currently has no required status check configured.

The three template repositories have GitHub Template mode enabled. Their CI, CodeQL, and Release workflows have completed successfully on their latest checked `main` commits during this audit.

Security controls such as Dependency Graph, Dependabot alerts/security updates, and push protection were applied by the maintainer through GitHub settings. The connector used for this audit cannot independently verify all of those security-setting states. Secret scanning availability and activation must not be assumed from push protection alone.

Update this inventory when repositories are created, transferred, archived, or change visibility. Recheck live settings before making operational decisions.

## Decision log

| Decision | Outcome |
| --- | --- |
| Organization role | Parent organization for engineering, agency, and owned products |
| Business model | Hybrid: agency services + product studio |
| First priority | Foundation |
| Existing repositories | Preserve; no bulk migration or renaming |
| Maintainer model | Single human maintainer: `iwwwan-io` |
| AI agent changes | Feature branch and pull request workflow |
| Merge | Explicit maintainer decision; no required second-person approval |
| Deployment | Separate explicit maintainer approval required |
| Security, permissions, and secrets | No changes without explicit approval |
