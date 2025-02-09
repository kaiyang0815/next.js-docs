---
description: Use the new Rust compiler to compile MDX files in the App Router.
---

# mdxRs

For experimental use with `@next/mdx`. Compiles MDX files using the new Rust compiler.

```js
const withMDX = require('@next/mdx')()

/** @type {import('next').NextConfig} */
const nextConfig = {
  pageExtensions: ['ts', 'tsx', 'mdx'],
  experimental: {
    mdxRs: true,
  },
}

module.exports = withMDX(nextConfig)
```
