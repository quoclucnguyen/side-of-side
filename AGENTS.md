# Repository Guidelines

## Project Structure & Module Organization
The NestJS application lives under `src/`, with `main.ts` bootstrapping NestFactory, `app.module.ts` wiring providers, and feature-specific folders such as `src/users/` for domain modules. Unit specs sit next to their targets as `*.spec.ts`, while end-to-end tests live in `test/` alongside `jest-e2e.json`. Compiled assets are emitted to `dist/`; do not edit files there. Shared product notes and context for contributors are stored in `memory-bank/`—review these before proposing architectural changes.

## Build, Test, and Development Commands
Use `npm run start:dev` for a watch-mode API server, or `npm run start:debug` when you need an inspector attached. Run `npm run build` to compile TypeScript into `dist/`, and `npm run start:prod` to execute that output locally. `npm run lint` applies ESLint with auto-fixes, while `npm run format` enforces Prettier on `src/` and `test/`. Favor `npm run test`, `npm run test:watch`, `npm run test:cov`, and `npm run test:e2e` depending on depth; always lint and test before pushing.

## Coding Style & Naming Conventions
TypeScript is required, keeping files camelCased (`users.service.ts`, `create-user.dto.ts`). Classes and providers use PascalCase, while instances, variables, and file-scoped constants use camelCase. Stick to Prettier defaults (2-space indent, single quotes, semicolons) and leverage the project ESLint config, which warns on floating promises and unsafe arguments; only introduce `any` when no precise contract exists and document why. Swagger decorators already exist in several modules—mirror their pattern when exposing new endpoints.

## Testing Guidelines
Jest drives both unit (`*.spec.ts`) and e2e (`*.e2e-spec.ts`) suites. When adding functionality, accompany it with a spec that mirrors the file path, e.g., `src/users/users.service.spec.ts`. Keep coverage high by running `npm run test:cov` and avoid regressions in `coverage/`. For HTTP flows, extend `test/app.e2e-spec.ts` or add new specs referencing SuperTest. Tests should arrange-act-assert, mocking external services rather than reaching into live integrations.

## Commit & Pull Request Guidelines
Git history follows Conventional Commits (`feat:`, `refactor:`, etc.), so prefix messages accordingly and keep subject lines under 72 characters. Each PR should describe the change, link any tracked issue, list verification commands, and include screenshots or cURL snippets for API changes. Ensure CI-critical commands (`npm run lint`, `npm run test`, `npm run test:e2e`) pass locally before requesting review, and mention any configuration updates or new environment variables within the PR body.

## Security & Configuration Tips
Environment variables are consumed via `@nestjs/config` and TypeORM—store them in a local `.env` ignored by Git and document additions in the PR. Never commit credentials, and scrub sample data before sharing logs. When touching dependencies, highlight security-sensitive upgrades (e.g., `pg`, `typeorm`) so reviewers can perform targeted checks.
