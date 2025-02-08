---
description: Learn how to configure your application with next.config.js.
---

# next.config.js

Next.js can be configured through a `next.config.js` file in the root of your project directory (for example, by `package.json`) with a default export.

```js
// @ts-check

/** @type {import('next').NextConfig} */
const nextConfig = {
  /* config options here */
}

module.exports = nextConfig
```

### ECMAScript Modules

`next.config.js` is a regular Node.js module, not a JSON file. It gets used by the Next.js server and build phases, and it's not included in the browser build.

If you need [ECMAScript modules](https://nodejs.org/api/esm.html), you can use `next.config.mjs`:

```js
// @ts-check

/**
 * @type {import('next').NextConfig}
 */
const nextConfig = {
  /* config options here */
}

export default nextConfig
```

> **Good to know**: `next.config` with the `.cjs`, `.cts`, or `.mts` extensions are currently **not** supported.

### Configuration as a Function

You can also use a function:

```js
// @ts-check

export default (phase, { defaultConfig }) => {
  /**
   * @type {import('next').NextConfig}
   */
  const nextConfig = {
    /* config options here */
  }
  return nextConfig
}
```

#### Async Configuration

Since Next.js 12.1.0, you can use an async function:

```js
// @ts-check

module.exports = async (phase, { defaultConfig }) => {
  /**
   * @type {import('next').NextConfig}
   */
  const nextConfig = {
    /* config options here */
  }
  return nextConfig
}
```

#### Phase

`phase` is the current context in which the configuration is loaded. You can see the [available phases](https://github.com/vercel/next.js/blob/5e6b008b561caf2710ab7be63320a3d549474a5b/packages/next/shared/lib/constants.ts#L19-L23). Phases can be imported from `next/constants`:

```js
// @ts-check

const { PHASE_DEVELOPMENT_SERVER } = require('next/constants')

module.exports = (phase, { defaultConfig }) => {
  if (phase === PHASE_DEVELOPMENT_SERVER) {
    return {
      /* development only config options here */
    }
  }

  return {
    /* config options for all phases except development here */
  }
}
```

### TypeScript

If you are using TypeScript in your project, you can use `next.config.ts` to use TypeScript in your configuration:

```ts
import type { NextConfig } from 'next'

const nextConfig: NextConfig = {
  /* config options here */
}

export default nextConfig
```

The commented lines are the place where you can put the configs allowed by `next.config.js`, which are [defined in this file](https://github.com/vercel/next.js/blob/canary/packages/next/src/server/config-shared.ts).

However, none of the configs are required, and it's not necessary to understand what each config does. Instead, search for the features you need to enable or modify in this section and they will show you what to do.

> Avoid using new JavaScript features not available in your target Node.js version. `next.config.js` will not be parsed by Webpack or Babel.

This page documents all the available configuration options:

### Unit Testing (experimental)

Starting in Next.js 15.1, the `next/experimental/testing/server` package contains utilities to help unit test `next.config.js` files.

The `unstable_getResponseFromNextConfig` function runs the `headers`, `redirects`, and `rewrites` functions from `next.config.js` with the provided request information and returns `NextResponse` with the results of the routing.

> The response from `unstable_getResponseFromNextConfig` only considers `next.config.js` fields and does not consider middleware or filesystem routes, so the result in production may be different than the unit test.

```js
import {
  getRedirectUrl,
  unstable_getResponseFromNextConfig,
} from 'next/experimental/testing/server'

const response = await unstable_getResponseFromNextConfig({
  url: 'https://nextjs.org/test',
  nextConfig: {
    async redirects() {
      return [{ source: '/test', destination: '/test2', permanent: false }]
    },
  },
})
expect(response.status).toEqual(307)
expect(getRedirectUrl(response)).toEqual('https://nextjs.org/test2')
```

{% content-ref url="appdir.md" %}
[appdir.md](appdir.md)
{% endcontent-ref %}

{% content-ref url="assetprefix.md" %}
[assetprefix.md](assetprefix.md)
{% endcontent-ref %}

{% content-ref url="authinterrupts.md" %}
[authinterrupts.md](authinterrupts.md)
{% endcontent-ref %}

{% content-ref url="basepath.md" %}
[basepath.md](basepath.md)
{% endcontent-ref %}

{% content-ref url="../../functions/cachelife.md" %}
[cachelife.md](../../functions/cachelife.md)
{% endcontent-ref %}

{% content-ref url="compress.md" %}
[compress.md](compress.md)
{% endcontent-ref %}

{% content-ref url="crossorigin.md" %}
[crossorigin.md](crossorigin.md)
{% endcontent-ref %}

{% content-ref url="csschunking.md" %}
[csschunking.md](csschunking.md)
{% endcontent-ref %}

{% content-ref url="devindicators.md" %}
[devindicators.md](devindicators.md)
{% endcontent-ref %}

{% content-ref url="distdir.md" %}
[distdir.md](distdir.md)
{% endcontent-ref %}

{% content-ref url="dynamicio.md" %}
[dynamicio.md](dynamicio.md)
{% endcontent-ref %}

{% content-ref url="env.md" %}
[env.md](env.md)
{% endcontent-ref %}

{% content-ref url="eslint.md" %}
[eslint.md](eslint.md)
{% endcontent-ref %}

{% content-ref url="expiretime.md" %}
[expiretime.md](expiretime.md)
{% endcontent-ref %}

{% content-ref url="exportpathmap.md" %}
[exportpathmap.md](exportpathmap.md)
{% endcontent-ref %}

{% content-ref url="generatebuildid.md" %}
[generatebuildid.md](generatebuildid.md)
{% endcontent-ref %}

{% content-ref url="generateetags.md" %}
[generateetags.md](generateetags.md)
{% endcontent-ref %}

{% content-ref url="../../functions/headers.md" %}
[headers.md](../../functions/headers.md)
{% endcontent-ref %}

{% content-ref url="httpagentoptions.md" %}
[httpagentoptions.md](httpagentoptions.md)
{% endcontent-ref %}

{% content-ref url="images.md" %}
[images.md](images.md)
{% endcontent-ref %}

{% content-ref url="cachehandler.md" %}
[cachehandler.md](cachehandler.md)
{% endcontent-ref %}

{% content-ref url="inlinecss.md" %}
[inlinecss.md](inlinecss.md)
{% endcontent-ref %}

{% content-ref url="logging.md" %}
[logging.md](logging.md)
{% endcontent-ref %}

{% content-ref url="mdxrs.md" %}
[mdxrs.md](mdxrs.md)
{% endcontent-ref %}

{% content-ref url="ondemandentries.md" %}
[ondemandentries.md](ondemandentries.md)
{% endcontent-ref %}

{% content-ref url="optimizepackageimports.md" %}
[optimizepackageimports.md](optimizepackageimports.md)
{% endcontent-ref %}

{% content-ref url="output.md" %}
[output.md](output.md)
{% endcontent-ref %}

{% content-ref url="pageextensions.md" %}
[pageextensions.md](pageextensions.md)
{% endcontent-ref %}

{% content-ref url="poweredbyheader.md" %}
[poweredbyheader.md](poweredbyheader.md)
{% endcontent-ref %}

{% content-ref url="ppr.md" %}
[ppr.md](ppr.md)
{% endcontent-ref %}

{% content-ref url="productionbrowsersourcemaps.md" %}
[productionbrowsersourcemaps.md](productionbrowsersourcemaps.md)
{% endcontent-ref %}

{% content-ref url="reactcompiler.md" %}
[reactcompiler.md](reactcompiler.md)
{% endcontent-ref %}

{% content-ref url="reactmaxheaderslength.md" %}
[reactmaxheaderslength.md](reactmaxheaderslength.md)
{% endcontent-ref %}

{% content-ref url="reactstrictmode.md" %}
[reactstrictmode.md](reactstrictmode.md)
{% endcontent-ref %}

{% content-ref url="redirects.md" %}
[redirects.md](redirects.md)
{% endcontent-ref %}

{% content-ref url="rewrites.md" %}
[rewrites.md](rewrites.md)
{% endcontent-ref %}

{% content-ref url="sassoptions.md" %}
[sassoptions.md](sassoptions.md)
{% endcontent-ref %}

{% content-ref url="serveractions.md" %}
[serveractions.md](serveractions.md)
{% endcontent-ref %}

{% content-ref url="servercomponentshmrcache.md" %}
[servercomponentshmrcache.md](servercomponentshmrcache.md)
{% endcontent-ref %}

{% content-ref url="serverexternalpackages.md" %}
[serverexternalpackages.md](serverexternalpackages.md)
{% endcontent-ref %}

{% content-ref url="staletimes.md" %}
[staletimes.md](staletimes.md)
{% endcontent-ref %}

{% content-ref url="staticgeneration.md" %}
[staticgeneration.md](staticgeneration.md)
{% endcontent-ref %}

{% content-ref url="trailingslash.md" %}
[trailingslash.md](trailingslash.md)
{% endcontent-ref %}

{% content-ref url="transpilepackages.md" %}
[transpilepackages.md](transpilepackages.md)
{% endcontent-ref %}

{% content-ref url="turbo.md" %}
[turbo.md](turbo.md)
{% endcontent-ref %}

{% content-ref url="typedroutes.md" %}
[typedroutes.md](typedroutes.md)
{% endcontent-ref %}

{% content-ref url="typescript.md" %}
[typescript.md](typescript.md)
{% endcontent-ref %}

{% content-ref url="urlimports.md" %}
[urlimports.md](urlimports.md)
{% endcontent-ref %}

{% content-ref url="usecache.md" %}
[usecache.md](usecache.md)
{% endcontent-ref %}

{% content-ref url="uselightningcss.md" %}
[uselightningcss.md](uselightningcss.md)
{% endcontent-ref %}

{% content-ref url="webpack.md" %}
[webpack.md](webpack.md)
{% endcontent-ref %}

{% content-ref url="webvitalsattribution.md" %}
[webvitalsattribution.md](webvitalsattribution.md)
{% endcontent-ref %}





