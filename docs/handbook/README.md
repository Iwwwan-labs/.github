# Engineering handbook

How we build and ship software at Iwwwan-labs. This is the working reference
behind [`docs/CONVENTIONS.md`](../CONVENTIONS.md): the rules are there, the
reasoning and the recipes are here.

If a page here contradicts a repository's own `AGENTS.md`, the repository wins for
that repository. Otherwise this is the default.

## Pages

| Page | Read it when |
| --- | --- |
| [getting-started.md](getting-started.md) | You are new and need a working environment |
| [development.md](development.md) | You are about to write code |
| [testing.md](testing.md) | You are deciding what to test and how |
| [release.md](release.md) | You are shipping a version |
| [security.md](security.md) | You handle secrets, dependencies, or reports |
| [operations.md](operations.md) | You run or debug a deployed service |

## The short version

- Start from a `template-*` repository. Do not hand-roll a stack.
- Branch, open a pull request, get CI green. Never push to `main`.
- Keep changes small. A pull request that needs a long explanation is too big.
- Write the test that would fail without your change.
- Document what a future reader cannot infer from the code.
- Treat secrets as radioactive: never in a repository, never in a log.

## What we optimize for

**Reversibility.** Small, reviewable changes that are easy to undo. We would rather
ship a narrow change today and follow up than hold a large one open.

**A single way to do things.** One CI pipeline, one label set, one release process.
Consistency is worth more than a locally optimal choice.

**Boring infrastructure.** Standard tools, standard layouts, standard versions.
Novelty belongs in the product, not the plumbing.
