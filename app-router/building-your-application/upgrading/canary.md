---
description: Upgrade your Next.js Application to canary and try out new features.
---

# Canary

## How to upgrade to Next.js Canary

The Next.js canary channel is updated daily with the latest experimental features and bug fixes. It's a great way to try out new features and [give feedback](https://github.com/vercel/next.js/issues) before they are released in a stable version.

To upgrade to canary, make sure you're on the latest version of Next.js and everything is working as expected. See the upgrade guides for more information.

Then, run the following command:

```bash
npm i next@canary
# or
yarn add next@canary
# or
pnpm i next@canary
```

### Features available in canary

The following features are currently available in canary:

**Caching**:

* `"use cache"`
* `cacheLife`
* `cacheTag`
* `dynamicIO`

**Authentication**:

* `forbidden`
* `unauthorized`
* `forbidden.js`
* `unauthorized.js`
* `authInterrupts`
