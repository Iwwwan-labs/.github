# Contributing to Iwwwan-labs

Thanks for helping improve our projects. This guide applies to every repository in the
`Iwwwan-labs` organization unless that repository says otherwise.

## Before you start

- Search existing issues and pull requests first — someone may already be working on it.
- For anything larger than a small fix, open an issue to agree on the approach before writing code.
- Report security issues privately, following [SECURITY.md](SECURITY.md). Never open a public issue for a vulnerability.

## Branching

Branch off the repository's default branch (`main`) and use a short, descriptive name:

| Prefix | Use for | Example |
| --- | --- | --- |
| `feat/` | New functionality | `feat/user-invitations` |
| `fix/` | Bug fixes | `fix/login-redirect` |
| `docs/` | Documentation only | `docs/api-examples` |
| `refactor/` | Behavior-preserving changes | `refactor/auth-middleware` |
| `chore/` | Tooling, dependencies, maintenance | `chore/bump-node` |

## Commit messages

We follow [Conventional Commits](https://www.conventionalcommits.org/):

```
<type>(<optional scope>): <description>

[optional body]

[optional footer]
```

- Use the imperative mood in the description: "add retry logic", not "added retry logic".
- Keep the first line under 72 characters.
- Reference issues in the footer, for example `Closes #42`.

Examples:

```
feat(api): add pagination to the users endpoint
fix(web): prevent double submit on the checkout form
docs: clarify local setup steps
```

## Pull requests

1. Keep the change focused. One logical change per pull request.
2. Fill in the pull request template — summary, motivation, and how you tested it.
3. Make sure CI passes before requesting review.
4. Request review from the code owners. At least one approval is required to merge.
5. Squash-merge into the default branch. Do not force-push to `main`.

### Definition of done

- [ ] The change is covered by tests, or you have explained why tests are not needed.
- [ ] Documentation is updated when behavior or configuration changes.
- [ ] CI is green.
- [ ] At least one approval from a code owner.

## Code style

- Match the conventions already in the repository.
- Run the formatter and linter before pushing. Most repositories expose these as `npm run lint`, `make lint`, or an equivalent.
- Keep dependencies minimal and justified.

## Questions

See [SUPPORT.md](SUPPORT.md) for where to ask.
