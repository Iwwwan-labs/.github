# Required repository settings

Some settings cannot be applied through the API with the organization's automation
token. GitHub returns `403 Resource not accessible by integration` for repository
settings, rulesets, Pages, and Dependabot alerts. Set these by hand, once per
repository, in the GitHub web UI.

Work through this list for every new repository. It takes about five minutes.

## 1. Enable GitHub Pages — `website` only

**Settings → Pages → Build and deployment → Source: GitHub Actions.**

Without this, the `Deploy to GitHub Pages` workflow fails at
`actions/configure-pages` with `Create Pages site failed`. Once enabled, every
push to `main` deploys automatically to
<https://iwwwan-labs.github.io/website/>.

## 2. Allow Actions to create pull requests — every repository

**Settings → Actions → General → Workflow permissions.**

- Select **Read and write permissions**.
- Tick **Allow GitHub Actions to create and approve pull requests**.
- Save.

release-please opens a release pull request. With this off, the Release workflow
fails with:

```text
release-please failed: GitHub Actions is not permitted to create or approve pull requests.
```

This is the reason the `Release` workflow is red on `template-web`,
`template-service`, and `template-mobile` until it is set.

## 3. Protect `main` — every repository

**Settings → Rules → Rulesets → New branch ruleset.** Target `main`.

- Require a pull request before merging (1 approval).
- Require status checks to pass: **CI**.
- Block force pushes.
- Restrict deletions.

Once set, nobody can push straight to `main` and CI must be green before merge.
The convention in [`CONVENTIONS.md`](CONVENTIONS.md) already says this; the ruleset
enforces it.

## 4. Repository metadata — every repository

**Settings → General.** Set the description and topics, and tick
**Template repository** for the `template-*` repositories.

| Repository | Description | Topics | Template |
| --- | --- | --- | --- |
| `.github` | Organization profile, community health files, and engineering conventions | `community-health` | no |
| `website` | Iwwwan-labs agency landing page | `landing-page`, `static-site`, `agency` | no |
| `template-web` | Starter: Vite + React + TypeScript web app with tests and CI | `template`, `vite`, `react`, `typescript`, `starter` | yes |
| `template-service` | Starter: Fastify + TypeScript backend service with tests, Docker, and CI | `template`, `fastify`, `typescript`, `nodejs`, `docker`, `starter` | yes |
| `template-mobile` | Starter: Expo + React Native + TypeScript mobile app with tests and CI | `template`, `expo`, `react-native`, `typescript`, `starter` | yes |

Set the homepage of `website` to `https://iwwwan-labs.github.io/website/`.

## 5. Code security — every repository

**Settings → Code security and analysis.**

- Enable **Dependabot alerts**.
- Enable **Dependabot security updates**.
- Enable **Secret scanning** and **Push protection**.
- Enable **CodeQL analysis** (default setup).

## 6. Organization settings

**Organization settings.**

- Set the display name, description, location, and a public email.
- Add a website URL once Pages is live.
- Create teams (`engineering`, `design`) and give them repository access.
- Create the private `docs` repository for internal documentation, then move the
  handbook there if that is preferred.

## Verifying

After the changes, these should hold:

| Check | Expected |
| --- | --- |
| `website` → Actions → Deploy to GitHub Pages | green |
| `template-*` → Actions → Release | green, or a release pull request opens |
| Pushing directly to `main` | rejected |
| A pull request with failing CI | cannot merge |
