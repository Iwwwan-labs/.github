# Release

Releases are automated. We do not bump versions or write changelogs by hand.

## How it works

We use [release-please](https://github.com/googleapis/release-please-action) with
Conventional Commits. On every push to `main`:

1. release-please reads the commits since the last release.
2. It opens or updates a release pull request that bumps the version in
   `package.json` and writes the changelog entry.
3. When you merge that pull request, release-please creates the tag and publishes
   the GitHub release with the generated notes.

The reusable workflow lives in
[`Iwwwan-labs/.github`](https://github.com/Iwwwan-labs/.github/blob/main/.github/workflows/release-please.yml).
Repositories call it from `.github/workflows/release.yml`.

The repository must allow Actions to create pull requests
(**Settings → Actions → General → Workflow permissions**). Without it the workflow
fails with `GitHub Actions is not permitted to create or approve pull requests`.
See [`REQUIRED-SETTINGS.md`](../REQUIRED-SETTINGS.md).

## Version numbers

[Semantic Versioning](https://semver.org/): `MAJOR.MINOR.PATCH`.

| Change | Bump | Commit type |
| --- | --- | --- |
| Breaking change | MAJOR | `feat!:` or `BREAKING CHANGE:` in the footer |
| New feature | MINOR | `feat:` |
| Bug fix | PATCH | `fix:` |
| Everything else | none | `chore:`, `docs:`, `ci:`, and similar |

Version numbers only move if your commits use `feat` or `fix`. A month of `chore:`
commits produces no release, which is usually correct.

## Breaking changes

Mark them explicitly:

```text
feat(api)!: require an API key on every route

BREAKING CHANGE: requests without an Authorization header now return 401.
```

Document the migration path in the release notes. A breaking change without a
migration note is a bug.

## A release, end to end

1. Merge your feature pull request into `main` with a `feat:` or `fix:` commit.
2. release-please opens a pull request titled something like
   `chore(main): release 0.2.0`.
3. Review the changelog it generated. Fix the wording by editing the pull request
   if needed.
4. Merge it. The tag and release are created automatically.
5. Confirm the release notes read well. They are what users see.

## Pre-release and hotfix

- Pre-releases use `-alpha.N` or `-beta.N` suffixes and are marked as
  pre-releases in release-please config.
- A hotfix for a shipped version branches from the release tag, gets the minimal
  fix, and is merged back to `main`.
