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

## Environment Setup
Ensure Node.js (v18+) and npm are installed locally. Clone the repository, run `npm install` to fetch dependencies, and create a `.env` file based on `.env.example`. Database migrations are handled via TypeORM; use `npm run migration:run` to apply pending migrations and `npm run migration:generate` to create new ones after entity changes. Docker Compose is available for local database setup if preferred.

## Performance Guidelines
Optimize database queries by selecting only needed fields and utilizing proper indexes. Leverage NestJS caching with `@nestjs/cache-manager` for frequently accessed data. Implement pagination for list endpoints to prevent large response payloads. Monitor bundle size with `npm run build:analyze` and avoid importing entire libraries when specific modules suffice.

## Error Handling & Logging
Use NestJS built-in exception filters for consistent error responses. Implement structured logging with context using the project's configured logger. Log warnings and errors appropriately, avoiding sensitive information in logs. For external service failures, implement retry mechanisms with exponential backoff where applicable.

## API Documentation
API documentation is auto-generated using Swagger. Access it locally at `http://localhost:3000/api` when running the development server. Maintain OpenAPI decorators on all endpoints, including proper response status codes, examples, and descriptions. Update documentation for any breaking changes or new features.

## Deployment & CI/CD
The application is containerized with Docker; use `docker build` to create production images. Environment-specific configurations are managed through environment variables passed at runtime. CI pipeline runs on every push, performing lint, tests, security scans, and building artifacts. Deployment follows a GitOps pattern with main branch auto-deploying to staging and tagged releases to production.

## Contributing & Issue Reporting
File issues with clear reproduction steps, environment details, and expected vs actual behavior. For bug fixes, create a branch from `main` prefixed with `fix/`. For features, use `feature/`. All contributions require passing tests and adherence to the established code style. Prior discussions for major changes are encouraged through issues or design documents in `memory-bank/`.

## Troubleshooting
For common development issues: clear node_modules and reinstall if encountering strange errors. Check `.env` configuration for database connection issues. Verify TypeScript compilation with `npm run build` when runtime errors occur. Use `npm run test:debug` for stepping through failing tests in debug mode.
