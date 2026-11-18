# Security

## Reporting

Report vulnerabilities privately, following
[`SECURITY.md`](https://github.com/Iwwwan-labs/.github/blob/main/SECURITY.md).
Never open a public issue for a vulnerability. Never write a proof of concept into
a public repository.

## Secrets

A secret never belongs in a repository. Not in code, not in a test fixture, not in
a comment, not in a commit you intend to delete later. Git remembers.

- Local development: `.env` files, gitignored. Commit `.env.example` with keys and
  no values.
- CI: repository or organization secrets, referenced as `${{ secrets.NAME }}`.
- Deployed services: the platform's secret store, injected as environment
  variables.
- If a secret is committed, rotate it first. Removing the commit is not enough;
  assume it is already compromised.

## Dependencies

- Dependabot alerts and security updates are enabled on every repository.
- Dependabot opens weekly pull requests for npm and GitHub Actions. Review the
  diff and merge when CI is green.
- A security update jumps the queue. Treat it as urgent, not as one of five open
  update pull requests.
- Run `npm audit` when you touch dependencies. Do not add a dependency that
  brings a known high-severity issue.

## Access

- Least privilege. Grant the smallest role that lets someone do their job.
- Teams, not individuals, own repositories. `@iwwwan-io` is the fallback owner.
- Automation uses a token scoped to what it needs, never a personal token.
- Remove access when someone leaves. Review the member list quarterly.

## Code

- Validate input at the boundary. Do not trust the client.
- Parameterize database queries. Never build SQL by string concatenation.
- Escape output. Use the framework's escaping; do not write your own.
- Authenticate before you authorize, and authorize on the server, never only in
  the UI.
- Log events, not secrets. Review what you log before you ship it.

## Supply chain

- Pin GitHub Actions to a version tag, and review what a new major version
  changes before adopting it.
- Prefer well-maintained dependencies with a public history over obscure ones.
- Be careful with install scripts. A dependency that runs code at install time
  needs a reason.
