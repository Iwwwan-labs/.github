# .github

Organization-wide community health files, templates, and engineering conventions for **Iwwwan-labs**.

Files in this repository are inherited by every repository in the organization that does not define its own. Edit them here to change the defaults across the whole organization.

## Contents

| Path | Purpose |
| --- | --- |
| `profile/README.md` | Organization profile page shown at https://github.com/Iwwwan-labs |
| `CONTRIBUTING.md` | How to propose changes: branches, commits, and pull requests |
| `CODE_OF_CONDUCT.md` | Expected behavior and enforcement process |
| `SECURITY.md` | How to report a vulnerability privately |
| `SUPPORT.md` | Where to ask questions and get help |
| `CODEOWNERS` | Default reviewers for the organization |
| `.github/ISSUE_TEMPLATE/` | Default issue forms |
| `.github/pull_request_template.md` | Default pull request description |
| `.github/workflows/node-ci.yml` | Reusable Node.js CI (`lint`, `format:check`, `typecheck`, `test`, `build`) |
| `.github/workflows/release-please.yml` | Reusable release automation (version bump, changelog, tag) |
| `docs/CONVENTIONS.md` | Repository naming, labels, commits, and release conventions |

## How these files are used

GitHub falls back to the files in this repository when a repository has no file of its own:

- Community health files (`CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, `SECURITY.md`, `SUPPORT.md`) are picked up from the repository root.
- Issue templates and the pull request template are picked up from `.github/`.
- `CODEOWNERS` at the root applies organization-wide.

See the GitHub documentation on [creating a default community health file](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file) for details.

## Reusable workflows

`node-ci.yml` is the single source of truth for the Node.js verification pipeline.
A repository calls it instead of repeating the steps:

```yaml
jobs:
  verify:
    uses: Iwwwan-labs/.github/.github/workflows/node-ci.yml@main
    with:
      build: true
```

It runs `npm ci`, then `lint`, `format:check`, `typecheck`, `test`, and (when
`build: true`) `build`. The called workflow runs in the caller's repository, so
it reads that repository's `.nvmrc` and scripts.

`release-please.yml` maintains a release pull request from Conventional Commits.
A repository calls it on push to `main`:

```yaml
on:
  push:
    branches: [main]

jobs:
  release:
    uses: Iwwwan-labs/.github/.github/workflows/release-please.yml@main
```

It needs `release-please-config.json` and `.release-please-manifest.json` at the
repository root. Merging the release pull request tags the version and publishes
release notes.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

[MIT](LICENSE) © Iwwwan-labs
