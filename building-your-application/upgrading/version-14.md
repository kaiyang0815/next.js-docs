---
description: Upgrade your Next.js Application from Version 13 to 14.
---

# Version 14

### Upgrading from 13 to 14

To update to Next.js version 14, run the following command using your preferred package manager:

```bash
npm i next@next-14 react@18 react-dom@18 && npm i eslint-config-next@next-14 -D
```

```bash
yarn add next@next-14 react@18 react-dom@18 && yarn add eslint-config-next@next-14 -D
```

```bash
pnpm i next@next-14 react@18 react-dom@18 && pnpm i eslint-config-next@next-14 -D
```

```bash
bun add next@next-14 react@18 react-dom@18 && bun add eslint-config-next@next-14 -D
```

> **Good to know:** If you are using TypeScript, ensure you also upgrade `@types/react` and `@types/react-dom` to their latest versions.

#### v14 Summary

* The minimum Node.js version has been bumped from 16.14 to 18.17, since 16.x has reached end-of-life.
* The `next export` command has been removed in favor of `output: 'export'` config. Please see the [docs](https://nextjs.org/docs/app/building-your-application/deploying/static-exports) for more information.
* The `next/server` import for `ImageResponse` was renamed to `next/og`. A codemod is available to safely and automatically rename your imports.
* The `@next/font` package has been fully removed in favor of the built-in `next/font`. A codemod is available to safely and automatically rename your imports.
* The WASM target for `next-swc` has been removed.
