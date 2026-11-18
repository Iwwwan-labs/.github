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

## Merging

- Squash-merge into `main`. One commit per pull request.
- At least one approving review from a code owner before merge.
- CI must be green.
- Delete the branch after merge.

## Releases

- Tag releases with [Semantic Versioning](https://semver.org/): `vMAJOR.MINOR.PATCH`.
- Generate release notes from Conventional Commits.
- Document breaking changes in the release notes under a "Breaking changes" heading.

## Security

- Enable secret scanning, Dependabot alerts, and CodeQL default setup on every repository.
- No secrets in the repository, ever. Use organization or repository secrets.
- Apply least privilege to teams and to automation tokens.

## Documentation

- Every repository has a `README.md` explaining what it is and how to run it.
- Longer documentation lives in a `docs/` directory or the `docs` repository.
- Keep a `AGENTS.md` at the repository root when AI agents work in the repository.
