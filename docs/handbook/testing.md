# Testing

## What we test

Test behavior, not implementation. A test should still pass if you refactor the
internals and keep the behavior the same.

Write the test that fails without your change. If you cannot make it fail first,
you do not yet know what you are fixing.

## What we do not test

- Framework internals, or that a library works.
- Trivial getters and pass-through functions.
- Private functions. Test them through the public behavior that uses them.
- Snapshot tests of large trees. They pass on every change and catch nothing.

## The layers

| Layer | Tool | Use it for |
| --- | --- | --- |
| Unit | Vitest or Jest | Pure logic, small components |
| Integration | Vitest or Jest | A route, a store, a component with its children |
| End to end | Playwright (when a project needs it) | A user path through the real app |

Most tests should be unit or integration. End-to-end tests are slow and flaky;
keep them few and aimed at paths that would hurt to break.

## By repository

**template-web** — Vitest with Testing Library. Query by role and text, not by
test ID. Colocate tests with the code: `Button.tsx` and `Button.test.tsx`.

```tsx
render(<Counter />);
await userEvent.click(screen.getByRole('button', { name: /increment/i }));
expect(screen.getByText('count is 1')).toBeInTheDocument();
```

**template-service** — Vitest. Use `app.inject()` to exercise real HTTP routes
without opening a port. Keep the server factory side-effect free so tests can
build an app per case.

```ts
const app = buildServer();
const res = await app.inject({ method: 'GET', url: '/api/health' });
expect(res.statusCode).toBe(200);
```

**template-mobile** — Jest with the `jest-expo` preset and Testing Library. Test
components, not routes; rendering a route pulls in the whole router. Use
`fireEvent` for interactions.

## Mocks

Do not mock what you can use for real. Prefer a real in-memory implementation, a
real test database, or a real HTTP call to a local server.

Mock only at a process boundary you do not control: a third-party API, a payment
provider, the system clock. When you mock, keep it at the edge and let the real
code run behind it.

## Coverage

Coverage is a signal, not a target. Do not chase a number. A well-tested critical
path matters more than 100 percent on a file nobody reads.

What matters: the happy path works, the obvious failure modes are handled, and
edge cases that have burned us before are locked down by a test.
