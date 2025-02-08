---
description: >-
  Learn how to enable the experimental `authInterrupts` configuration option to
  use `forbidden` and `unauthorized`.
---

# authInterrupts

The `authInterrupts` configuration option allows you to use `forbidden` and `unauthorized` APIs in your application. While these functions are experimental, you must enable the `authInterrupts` option in your `next.config.js` file to use them:

```ts
import type { NextConfig } from 'next'

const nextConfig: NextConfig = {
  experimental: {
    authInterrupts: true,
  },
}

export default nextConfig
```

```js
module.exports = {
  experimental: {
    authInterrupts: true,
  },
}
```
