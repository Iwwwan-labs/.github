# AGENTS.md

Persistent context for AI agents working in the Iwwwan-labs organization.

## What this organization is

Iwwwan-labs is an AI-powered digital product and software engineering agency in
Indonesia. This `.github` repository holds the organization profile
(`profile/README.md`), community health files, issue and pull request templates,
and shared conventions in `docs/CONVENTIONS.md`.

## Repositories

| Repository | Stack | Purpose |
| --- | --- | --- |
| `.github` | Markdown | Org profile, community health files, conventions |
| `website` | Static HTML and CSS | Public landing page |
| `template-web` | Vite 6, React 18, TypeScript | Web app starter |
| `template-service` | Fastify 5, TypeScript, Node 22 | Backend service starter |
| `template-mobile` | Expo SDK 52, React Native, TypeScript | Mobile app starter |

All repositories are public and default to `main`.

## Working conventions

- Branch names: `feat/`, `fix/`, `docs/`, `chore/`, `refactor/`.
- Commits follow [Conventional Commits](https://www.conventionalcommits.org/).
- Never push directly to `main`. Open a pull request.
- Every repository has an `AGENTS.md`. Read the local one before editing code
  there; it lists the exact commands and rules for that stack.
- Add `Co-authored-by: openhands <openhands@all-hands.dev>` to agent commits.
- User-facing conversation is in Indonesian. Code, comments, commit messages,
  and repository documentation are in English.

## Verification before pushing

The pipeline is defined once, in
[`.github/workflows/node-ci.yml`](.github/workflows/node-ci.yml), and each template
calls it from its own `.github/workflows/ci.yml`. Run the same steps locally and
confirm they pass before committing:

```bash
npm ci
npm run lint
npm run format:check
npm run typecheck
npm test
npm run build       # not in template-mobile
```

Prettier checks YAML too. Run `npm run format` after editing any `.yml` file, or
`format:check` fails in CI.

Releases are automated. Do not bump versions or edit changelogs by hand;
release-please opens a release pull request from Conventional Commits.

## Known constraints

- GitHub Pages must be enabled by hand once per new repository
  (**Settings → Pages → Source: GitHub Actions**). The deploy workflow cannot
  create the Pages site itself; the integration token is not allowed to.
  See the `website` README.
- `react-test-renderer` must be pinned to the React version in use. A floating
  version pulls React 19 and breaks `npm install` for React 18 projects.
- The `@/` path alias must stay in sync between `tsconfig.json` and the bundler
  config (`vite.config.ts` for web, `babel.config.js` for mobile). Changing one
  without the other breaks either the editor or the build.
- Dependabot ignores major updates in the templates. Templates pin a known-good
  stack, and a grouped major bump splits coupled packages (React,
  React Native, Expo) across the production and development groups, which breaks
  `npm ci`. Upgrade a major deliberately, in its own pull request.
- GitHub App tokens cannot enable Pages, change repository settings, manage
  rulesets, or create repositories and teams. Those need the web UI.

## Adding a repository

1. Create it under the org with a `main` branch.
2. Add `README.md`, `AGENTS.md`, `LICENSE` (MIT), `.gitignore`, and a CI
   workflow under `.github/workflows/`.
3. Match the structure and scripts of the existing templates for that stack.
4. Verify locally, then push. Confirm the CI run is green.
