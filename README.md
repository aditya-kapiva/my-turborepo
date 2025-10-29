# Monorepo

This is a monorepo setup using npm workspaces.

## What's inside?

This monorepo includes the following packages/apps:

### Apps and Packages

- `docs`: a [Next.js](https://nextjs.org/) app
- `web`: another [Next.js](https://nextjs.org/) app
- `@repo/ui`: a stub React component library shared by both `web` and `docs` applications
- `@repo/eslint-config`: `eslint` configurations (includes `eslint-config-next` and `eslint-config-prettier`)
- `@repo/typescript-config`: `tsconfig.json`s used throughout the monorepo

Each package/app is 100% [TypeScript](https://www.typescriptlang.org/).

### Utilities

This monorepo has some additional tools already setup for you:

- [TypeScript](https://www.typescriptlang.org/) for static type checking
- [ESLint](https://eslint.org/) for code linting
- [Prettier](https://prettier.io) for code formatting

### Build

To build all apps and packages, run the following command:

```sh
npm run build
```

You can build a specific package by navigating to its directory:

```sh
cd apps/docs
npm run build
```

### Develop

To develop all apps and packages, run the following command:

```sh
npm run dev
```

You can develop a specific package by navigating to its directory:

```sh
cd apps/web
npm run dev
```

## Useful Links

- [npm workspaces](https://docs.npmjs.com/cli/v10/using-npm/workspaces)
- [Next.js](https://nextjs.org/)
- [TypeScript](https://www.typescriptlang.org/)
- [ESLint](https://eslint.org/)
- [Prettier](https://prettier.io)
