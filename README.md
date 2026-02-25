# Monorepo Template

pnpm + Turborepo monorepo with Husky, lint-staged, commitlint, and Prettier pre-configured.

## Stack

- **pnpm workspaces** — package manager
- **Turborepo** — task orchestration & caching
- **Husky** — Git hooks
- **lint-staged** — run linters only on staged files
- **commitlint** — enforce conventional commit format
- **Prettier** — code formatting

## Getting started

```bash
# 1. Install dependencies
pnpm install

# 2. Initialize Husky (REQUIRED — run once after cloning)
pnpm prepare

# 3. Start all apps in dev mode
pnpm dev
```

> **Note:** `pnpm prepare` runs `husky` to install the Git hooks defined in `.husky/`.
> You must run it once after cloning the repo, or Husky hooks won't activate.

## Project structure

```
.
├── apps/                  # Application packages (Next.js, NestJS, etc.)
│   ├── web/
│   └── api/
├── packages/              # Shared packages (types, utils, ui, config, etc.)
├── .husky/
│   ├── pre-commit         # Runs lint-staged
│   └── commit-msg         # Runs commitlint
├── commitlint.config.js   # Conventional commits rules
├── .prettierrc            # Prettier config
├── turbo.json             # Turborepo task pipeline
└── pnpm-workspace.yaml    # Workspace definition
```

## Adding a new app

```bash
# Create the app directory
mkdir -p apps/my-new-app
cd apps/my-new-app

# Add a package.json with a unique "name" field
# Then add it to turbo.json tasks as needed
```

## Husky hooks

| Hook          | What it does                                     |
| ------------- | ------------------------------------------------ |
| `pre-commit`  | Runs `lint-staged` (Prettier on staged files)    |
| `commit-msg`  | Validates commit message format (commitlint)     |

### Reinitializing Husky on a new machine

```bash
pnpm prepare
```

This is equivalent to `husky` — it sets up the `.git/hooks` symlinks.

## Commit message format

Follows [Conventional Commits](https://www.conventionalcommits.org/):

```
<type>(<scope>): <description>

[optional body]
```

Allowed types: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `perf`, `style`, `ci`, `build`, `revert`

## Turbo tasks

| Command          | Description                        |
| ---------------- | ---------------------------------- |
| `pnpm dev`       | Start all apps in parallel (watch) |
| `pnpm build`     | Build all packages in order        |
| `pnpm lint`      | Lint all packages                  |
| `pnpm test`      | Run all unit tests                 |
| `pnpm test:e2e`  | Run all E2E tests                  |
| `pnpm format`    | Format all files with Prettier     |
