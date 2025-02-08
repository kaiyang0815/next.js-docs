# staticGeneration\*

The `staticGeneration*` options allow you to configure the Static Generation process for advanced use cases.

```ts
import type { NextConfig } from 'next'

const nextConfig: NextConfig = {
  experimental: {
    staticGenerationRetryCount: 1,
    staticGenerationMaxConcurrency: 8,
    staticGenerationMinPagesPerWorker: 25,
  },
}

export default nextConfig
```

```js
const nextConfig = {
  experimental: {
    staticGenerationRetryCount: 1,
    staticGenerationMaxConcurrency: 8,
    staticGenerationMinPagesPerWorker: 25,
  },
}

export default nextConfig
```

### Config Options

The following options are available:

* `staticGenerationRetryCount`: The number of times to retry a failed page generation before failing the build.
* `staticGenerationMaxConcurrency`: The maximum number of pages to be processed per worker.
* `staticGenerationMinPagesPerWorker`: The minimum number of pages to be processed before starting a new worker.
