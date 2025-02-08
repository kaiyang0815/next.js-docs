---
description: Learn how to enable the useCache flag in Next.js.
---

# useCache

The `useCache` flag is an experimental feature in Next.js that enables the `use cache` directive to be used independently of `dynamicIO`. When enabled, you can use `use cache` in your application even if `dynamicIO` is turned off.

### Usage

To enable the `useCache` flag, set it to `true` in the `experimental` section of your `next.config.ts` file:

```ts
import type { NextConfig } from 'next'

const nextConfig: NextConfig = {
  experimental: {
    useCache: true,
  },
}

export default nextConfig
```

When `useCache` is enabled, you can use the following cache functions and configurations:

* The `use cache` directive
* The `cacheLife` function with `use cache`
* The `cacheTag` function
