---
description: Enable experimental support for Lightning CSS.
---

# useLightningcss

Experimental support for using [Lightning CSS](https://lightningcss.dev), a fast CSS bundler and minifier, written in Rust.

```ts
import type { NextConfig } from 'next'

const nextConfig: NextConfig = {
  experimental: {
    useLightningcss: true,
  },
}

export default nextConfig
```

```js
/** @type {import('next').NextConfig} */
const nextConfig = {
  experimental: {
    useLightningcss: true,
  },
}

module.exports = nextConfig
```
