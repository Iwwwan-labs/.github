# Operations

How we run and debug what we ship.

## Environments

| Environment | Purpose | Branch |
| --- | --- | --- |
| Local | Development | any |
| Preview | Review a change before merge | pull request |
| Production | Live traffic | `main` |

Production deploys come from `main` only. Nothing reaches production that has not
passed CI and a review.

## Health and readiness

Every service exposes a health endpoint. `template-service` ships
`GET /api/health`, returning `{"status":"ok","uptime":<seconds>}`. Use it for both
liveness and readiness until a service needs them to differ.

- Liveness: is the process alive?
- Readiness: can it serve traffic right now (database reachable, dependencies up)?

## Configuration

Configuration comes from the environment, never from code. `template-service`
validates its environment at startup and refuses to boot on a bad value. Fail
loudly at boot rather than mysteriously at request time.

Required variables are listed in `.env.example`. That file is the contract.

## Logging

Structured logs, one JSON object per line. `template-service` uses Fastify's
logger, which emits `level`, `time`, `reqId`, and the request and response.

- Log at the boundary: request in, response out, error raised.
- Include a request id so you can follow one request across services.
- Never log secrets, tokens, or personal data. Mask what you must record.
- Log levels: `error` for things that need a human, `warn` for recoverable
  surprises, `info` for lifecycle events, `debug` for development only.

## Debugging a deployed service

1. Read the health endpoint. Is it alive and ready?
2. Read the logs around the failure. Find the request id.
3. Reproduce locally with the same input.
4. Write the failing test before you fix it.
5. Fix, ship, and confirm with the same signal you started from.

## Incidents

- Stop the bleeding first. Roll back before you understand the cause.
- Write down the timeline as it happens, in a shared place.
- Tell the people affected, plainly, as soon as you know.
- Afterward, write a short retrospective: what happened, why, and what changes
  prevent it. Blameless. The system failed, not a person.

## Containers

`template-service` builds a multi-stage image and runs as a non-root user. Keep it
that way. A container should hold one process, read configuration from the
environment, and write logs to stdout.

## Backups

Anything with state gets a backup. Test the restore, not just the backup. An
untested backup is a hope, not a plan.
