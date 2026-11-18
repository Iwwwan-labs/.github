# Getting started

## What you need

- Node.js 22 (`nvm use` reads the `.nvmrc` in each repository).
- npm 10 or newer.
- Git, configured with your name and email.
- Docker, only for `template-service`.

## Pick a repository

| Repository | Use it for |
| --- | --- |
| `template-web` | Browser applications: Vite, React, TypeScript |
| `template-service` | Backend services and APIs: Fastify, TypeScript, Node |
| `template-mobile` | Mobile applications: Expo, React Native, TypeScript |
| `website` | The agency landing page: static HTML and CSS |

## Get it running

```bash
git clone https://github.com/Iwwwan-labs/<repository>.git
cd <repository>
nvm use
npm ci
```

Then check that the baseline is green before you change anything:

```bash
npm run lint
npm run format:check
npm run typecheck
npm test
npm run build      # not in template-mobile
```

Starting the app:

| Repository | Command |
| --- | --- |
| `template-web` | `npm run dev` |
| `template-service` | `npm run dev` |
| `template-mobile` | `npm start`, then `i`, `a`, or `w` |
| `website` | `python3 -m http.server 8000` |

## Starting a new project from a template

1. On GitHub, use **Use this template** on the `template-*` repository you need.
2. Name it following [`CONVENTIONS.md`](../CONVENTIONS.md): lowercase, hyphens, no
   framework name unless the repository is itself a template.
3. Rename the package and app identifiers.
4. Replace the example screen or route with your first real one.
5. Update `README.md` and `AGENTS.md` for the new project.
6. Push `main`, then confirm CI is green.

## Where things are

Every repository follows the same shape:

```text
<repository>/
├── .github/workflows/   CI and release automation
├── src/                 application code
├── README.md            what it is and how to run it
├── AGENTS.md            guidance for AI agents
├── CODEOWNERS           who reviews what
└── .editorconfig        formatting defaults for editors
```
