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

- Branch names: `feat/`, `fix/`, `docs/`, `chore/`.
- Commits follow [Conventional Commits](https://www.conventionalcommits.org/).
- Never push directly to `main`. Open a pull request.
- Every repository has an `AGENTS.md`. Read the local one before editing code
  there; it lists the exact commands and rules for that stack.
- Add `Co-authored-by: openhands <openhands@all-hands.dev>` to agent commits.
- User-facing conversation is in Indonesian. Code, comments, commit messages,
  and repository documentation are in English.

## Verification before pushing

Each template repository ships the same verification contract. Run all of it and
confirm it passes before committing:

```bash
npm ci
npm run lint
npm run format:check
npm run typecheck   # template-mobile also, template-service also
npm test
npm run build       # template-web and template-service only
```

CI runs the same steps on push and pull request. A red check means the change is
not done.

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

## Adding a repository

1. Create it under the org with a `main` branch.
2. Add `README.md`, `AGENTS.md`, `LICENSE` (MIT), `.gitignore`, and a CI
   workflow under `.github/workflows/`.
3. Match the structure and scripts of the existing templates for that stack.
4. Verify locally, then push. Confirm the CI run is green.
