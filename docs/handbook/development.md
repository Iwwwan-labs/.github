# Development

## The loop

1. Branch from `main`: `feat/`, `fix/`, `docs/`, `refactor/`, or `chore/`.
2. Make the change. Keep it small.
3. Run the checks locally: `lint`, `format:check`, `typecheck`, `test`, `build`.
4. Commit with a Conventional Commit message.
5. Push, open a pull request, get CI green.
6. Squash-merge once reviewed. Delete the branch.

## Commits

```text
<type>(<optional scope>): <description>
```

Imperative mood, first line under 72 characters, no trailing period. Reference
issues in the footer.

```text
feat(auth): add refresh token rotation

Closes #42
```

The type matters: `feat` and `fix` appear in the changelog and drive version
bumps. `chore`, `ci`, `test`, `build`, and `style` are hidden from release notes.

## Branches

Short and descriptive, prefixed by type: `feat/user-invitations`,
`fix/login-redirect`, `docs/api-examples`. Avoid your own name as a branch.

## Pull requests

- One concern per pull request. If you are describing two changes, split it.
- Fill in the template. State what changed and why, not just what files moved.
- Keep it reviewable: under about 400 changed lines is a good target.
- Do not merge your own pull request without a review, unless it is a trivial fix
  and CI is green.
- Delete the branch after merge.

## Code style

Formatting is not a discussion. Prettier decides, and CI enforces it. Run
`npm run format` before committing.

Linting is ESLint with the repository's config. Fix warnings rather than
suppressing them. When you must suppress a rule, use the narrowest scope and
leave a comment explaining why.

## TypeScript

- Strict mode is on. Do not weaken `tsconfig.json` to make code compile.
- Do not use `any`. Prefer `unknown` and narrow it.
- Model states that cannot happen out of existence. A union of valid states beats
  a set of optional booleans.
- Export types you intend to be public. Keep the rest local.

## Dependencies

- Justify every new dependency in the pull request. What does it do that a small
  amount of our own code cannot?
- Prefer one well-maintained package over three small ones.
- For Expo, install with `npx expo install` so versions match the SDK.
- Dependabot opens weekly update pull requests. Treat them like any other change:
  CI must pass, and you read the diff.

## Layout

| Repository | Where code goes |
| --- | --- |
| `template-web` | `src/` for components and logic, tests colocated |
| `template-service` | `src/routes/` for HTTP routes, `src/` for the rest |
| `template-mobile` | `app/` for routes, `src/` for everything else |

Shared design values live in one place: CSS custom properties for web,
`src/theme.ts` for mobile. Do not scatter hard-coded colors and spacing.

## Documentation

- `README.md` says what the repository is and how to run it.
- `AGENTS.md` tells an AI agent the commands and the local rules.
- Longer explanations go in `docs/`.
- Document what a reader cannot infer from the code: a non-obvious invariant, a
  workaround, a deliberate trade-off. Do not narrate the code.
