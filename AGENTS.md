# AGENTS.md

This repository contains a TypeScript library (`src/`) and a Docusaurus website
(`website/`). Use npm scripts from the repo root unless noted otherwise.

## Quick Commands

- Install deps (root + website): `npm install` (root `postinstall` installs website)
- Dev (library + demo + website): `npm run start`
- Build all: `npm run build`
- Lint all: `npm run test:lint`
- Unit tests: `npm run test:unit`

## Build / Lint / Test (detailed)

### Build
- Library build (types + bundle): `npm run build`
- Only library bundle: `npm run build:lib`
- Only type declarations: `npm run build:ts`
- Website build: `npm run build:website`
- Website typecheck: `npm run build:ts-website`

### Lint / Format
- Lint all (prettier + eslint + stylelint): `npm run test:lint`
- Prettier check (lib): `npm run lint:prettier`
- Prettier check (website): `npm run lint:prettier-website`
- ESLint (lib): `npm run lint:eslint`
- ESLint (website): `npm run lint:eslint-website`
- Stylelint (lib): `npm run lint:stylelint`
- Stylelint (website): `npm run lint:stylelint-website`
- Auto-fix all: `npm run fix`

### Tests
- Unit tests: `npm run test:unit`
- Single test file: `npm run test:unit -- src/lib/utils/__tests__/utils/random.spec.ts`
- Single test by name: `npm run test:unit -- -t "utils#random"`
- Watch a test: `npm run test:unit -- --watch`

Notes:
- Jest config is `jest.config.js` with `ts-jest` and `jsdom`.
- Tests live under `src/**/__tests__/**/*.spec.ts`.

## Project Structure

- `src/`: library code (TypeScript, strict)
- `src/lib/**`: core features (data, renderer, ticker, options, utils)
- `website/`: Docusaurus site and docs
- `.jest/`: test setup and stubs

## Code Style & Conventions

### Formatting
- Prettier: single quotes, semicolons, trailing commas, print width 100.
- EditorConfig: 2-space indent, final newline, trim trailing whitespace.
- Keep markdown lines unwrapped (EditorConfig allows long lines in `.md`).

### Imports
- Use type-only imports for types: `import type { Foo } from './bar';`
- Prefer explicit named exports (see `src/index.ts`).
- Avoid internal module imports (ESLint `import/no-internal-modules`).

### Types & TypeScript
- `strict: true` in `tsconfig.json`.
- Avoid `any` unless there is no viable alternative.
- Use `object` not `Object`, `string` not `String`, etc.
- Prefer `type`-safe unions and `as const` for option lists.
- Avoid namespaces; prefer ES modules.

### Naming
- `camelCase` for variables/functions, `PascalCase` for types/classes.
- Files: kebab-case or lower-case with hyphens (existing pattern in `src/lib/*`).
- Keep exported identifiers stable; library is public API.

### Functions & Control Flow
- Prefer pure helpers in `src/lib/utils`.
- Avoid `console` statements (ESLint `no-console`).
- Avoid `for...in` over objects (ESLint `guard-for-in`).
- Do not leave commented-out code in committed changes.

### Error Handling
- Fail fast on invalid input with explicit validation (see `validate-options.ts`).
- Return early when type checks fail.
- Use deterministic fallbacks for browser APIs where needed (see worker creation).

### Tests
- Jest with `ts-jest` and `jsdom`.
- Test names use `describe('feature', () => { test('case', ...) })`.
- Keep tests deterministic; avoid random without fixed seed.

### CSS / SCSS
- Stylelint config extends `stylelint-config-sass-guidelines`.
- Max nesting depth: 4.
- Avoid excessive selector specificity (compound selectors <= 5).

## Lint Rules Highlights (non-exhaustive)

- `no-only-tests/no-only-tests`: disallow `.only` in tests.
- `no-duplicate-imports`: keep imports consolidated.
- `import/order`: enforce ordered imports (use existing style in files).
- `@typescript-eslint/consistent-type-imports`: use type-only imports.
- `@typescript-eslint/explicit-member-accessibility`: class members explicit.

## Repository Rules

- No Cursor rules found in `.cursor/rules/` or `.cursorrules`.
- No Copilot rules found in `.github/copilot-instructions.md`.

## Tips for Agents

- Run `npm run test:unit -- <file>` when you touch core logic.
- Run `npm run lint:eslint` and `npm run lint:prettier` for quick checks.
- Keep edits minimal and consistent with existing patterns in `src/lib/**`.
