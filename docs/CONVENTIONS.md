# Engineering conventions

Organization-wide defaults for every repository in `Iwwwan-labs`. A repository may
override these, but the override should be deliberate and documented in that
repository.

## Repository naming

| Prefix | Use for | Visibility | Example |
| --- | --- | --- | --- |
| *(none)* | Products and services we operate | Public or private | `website`, `api-gateway` |
| `template-` | Starter repositories copied for new work | Public | `template-web` |
| `clients-` | Per-client delivery work | Private | `clients-acme-store` |
| `internal-` | Internal tooling and automation | Private | `internal-deploy-bot` |
| `.github` | Organization profile and shared files | Public | `.github` |

Rules:

- Lowercase, words separated by hyphens. No spaces or underscores.
- Be descriptive, not clever. `template-web` beats `awesome-starter-kit`.
- Do not encode the language or framework in the name unless the repository is a template.

## Default branch

`main`. Never `master`. Never force-push to `main`.

## Branch naming

| Prefix | Use for |
| --- | --- |
| `feat/` | New functionality |
| `fix/` | Bug fixes |
| `docs/` | Documentation only |
| `refactor/` | Behavior-preserving changes |
| `chore/` | Tooling, dependencies, maintenance |

## Commit messages

[Conventional Commits](https://www.conventionalcommits.org/):

```
<type>(<optional scope>): <description>
```

Allowed types: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`,
`build`, `ci`, `chore`, `revert`.

## Labels

Every repository uses this base set. Add domain-specific labels as needed.

| Label | Color | Use for |
| --- | --- | --- |
| `bug` | `#d73a4a` | Something is not working |
| `enhancement` | `#a2eeef` | New feature or request |
| `documentation` | `#0075ca` | Documentation improvements |
| `triage` | `#fbca04` | Needs to be reviewed and categorized |
| `good first issue` | `#7057ff` | Good entry point for newcomers |
| `help wanted` | `#008672` | Extra attention is needed |
| `blocked` | `#b60205` | Waiting on something else |
| `wontfix` | `#ffffff` | Will not be worked on |
| `dependencies` | `#0366d6` | Dependency updates |

## Pull requests and merging

Iwwwan-labs currently operates with a single human maintainer: `iwwwan-io`.
The repository rulesets therefore do not require approving reviews or Code Owner
approval. Do not add an approval requirement until another qualified reviewer is
available and the policy is deliberately changed.

- All changes to `main` go through a pull request; do not push directly to `main`.
- The maintainer reviews the diff, scope, and check results before merging.
- Required CI and CodeQL checks must pass wherever configured by the repository ruleset.
- Resolve review conversations before merge.
- Use squash merge by default to keep one logical commit per pull request.
- Delete the feature branch after merge.
- AI agents may prepare branches and pull requests, but must not merge them.

## Releases

- Tag releases with [Semantic Versioning](https://semver.org/): `vMAJOR.MINOR.PATCH`.
- Generate release notes from Conventional Commits.
- Document breaking changes in the release notes under a "Breaking changes" heading.
- Release automation may prepare release pull requests; the maintainer controls merging.

## Deployment

- Deployment is a separate consequential action from merging.
- Keep production deployment manual or behind an explicit maintainer-controlled approval.
- AI agents must not trigger production deployment without explicit approval.

## Security

- Enable Dependency Graph, Dependabot alerts, Dependabot security updates, and push protection where supported.
- Enable secret scanning where available for the repository and plan.
- Use CodeQL for supported languages and repository configurations.
- No secrets in the repository, ever. Use organization or repository secrets.
- Apply least privilege to teams and automation tokens.
- Treat security-setting availability as plan- and repository-dependent; do not document a control as enabled without verification.

## AI agent permissions

AI agents may inspect issues, implement scoped changes on feature branches, run checks,
and open pull requests. They must not merge, deploy, or change organization/repository
security settings, permissions, or secrets without explicit approval from `iwwwan-io`.

## Documentation

- Every repository has a `README.md` explaining what it is and how to run it.
- Longer documentation lives in a `docs/` directory or the `docs` repository.
- Keep an `AGENTS.md` at the repository root when AI agents work in the repository.
