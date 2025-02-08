---
description: >-
  Learn how to use the use cache directive to cache data in your Next.js
  application.
---

# use cache

> This feature is currently available in the canary channel and subject to change. Try it out by [upgrading Next.js](https://nextjs.org/docs/app/building-your-application/upgrading/canary), and share your feedback on [GitHub](https://github.com/vercel/next.js/issues).

The `use cache` directive designates a component and/or a function to be cached. It can be used at the top of a file to indicate that all exports in the file are cacheable, or inline at the top of a function or component to inform Next.js the return value should be cached and reused for subsequent requests. This is an experimental Next.js feature, and not a native React feature like `use client` or `use server`.

### Usage

Enable support for the `use cache` directive with the `useCache` flag in your `next.config.ts` file:

```ts
import type { NextConfig } from 'next'

const nextConfig: NextConfig = {
  experimental: {
    useCache: true,
  },
}

export default nextConfig
```

```js
/** @type {import('next').NextConfig} */
const nextConfig = {
  experimental: {
    useCache: true,
  },
}

module.exports = nextConfig
```

Additionally, `use cache` directives are also enabled when the `dynamicIO` flag is set.

Then, you can use the `use cache` directive at the file, component, or function level:

```tsx
// File level
'use cache'

export default async function Page() {
  // ...
}

// Component level
export async function MyComponent() {
  'use cache'
  return <></>
}

// Function level
export async function getData() {
  'use cache'
  const data = await fetch('/api/data')
  return data
}
```

### Good to know

* `use cache` is an experimental Next.js feature, and not a native React feature like `use client` or `use server`.
* Any [serializable](https://react.dev/reference/rsc/use-server#serializable-parameters-and-return-values) arguments (or props) passed to the cached function, as well as any serializable values it reads from the parent scope, will be converted to a format like JSON and automatically become a part of the cache key.
* Any non-serializable arguments, props, or closed-over values will turn into opaque references inside the cached function, and can be only passed through and not inspected nor modified. These non-serializable values will be filled in at the request time and won't become a part of the cache key.
  * For example, a cached function can take in JSX as a `children` prop and return `<div>{children}</div>`, but it won't be able to introspect the actual `children` object.
* The return value of the cacheable function must also be serializable. This ensures that the cached data can be stored and retrieved correctly.
* Functions that use the `use cache` directive must not have any side-effects, such as modifying state, directly manipulating the DOM, or setting timers to execute code at intervals.
* If used alongside Partial Prerendering, segments that have `use cache` will be prerendered as part of the static HTML shell.
* Unlike `unstable_cache` which only supports JSON data, `use cache` can cache any serializable data React can render, including the render output of components.

### Examples

#### Caching entire routes with `use cache`

To prerender an entire route, add `use cache` to the top **both** the `layout` and `page` files. Each of these segments are treated as separate entry points in your application, and will be cached independently.

```tsx
'use cache'

export default function Layout({ children }: { children: ReactNode }) {
  return <div>{children}</div>
}
```

```jsx
'use cache'

export default function Layout({ children }) {
  return <div>{children}</div>
}
```

Any components imported and nested in `page` file will inherit the cache behavior of `page`.

```tsx
'use cache'

async function Users() {
  const users = await fetch('/api/users')
  // loop through users
}

export default function Page() {
  return (
    <main>
      <Users />
    </main>
  )
}
```

```jsx
'use cache'

async function Users() {
  const users = await fetch('/api/users')
  // loop through users
}

export default function Page() {
  return (
    <main>
      <Users />
    </main>
  )
}
```

> This is recommended for applications that previously used the `export const dynamic = "force-static"` option, and will ensure the entire route is prerendered.

#### Caching component output with `use cache`

You can use `use cache` at the component level to cache any fetches or computations performed within that component. When you reuse the component throughout your application it can share the same cache entry as long as the props maintain the same structure.

The props are serialized and form part of the cache key, and the cache entry will be reused as long as the serialized props produce the same value in each instance.

```tsx
export async function Bookings({ type = 'haircut' }: BookingsProps) {
  'use cache'
  async function getBookingsData() {
    const data = await fetch(`/api/bookings?type=${encodeURIComponent(type)}`)
    return data
  }
  return //...
}

interface BookingsProps {
  type: string
}
```

```jsx
export async function Bookings({ type = 'haircut' }) {
  'use cache'
  async function getBookingsData() {
    const data = await fetch(`/api/bookings?type=${encodeURIComponent(type)}`)
    return data
  }
  return //...
}
```

#### Caching function output with `use cache`

Since you can add `use cache` to any asynchronous function, you aren't limited to caching components or routes only. You might want to cache a network request or database query or compute something that is very slow. By adding `use cache` to a function containing this type of work it becomes cacheable, and when reused, will share the same cache entry.

```tsx
export async function getData() {
  'use cache'

  const data = await fetch('/api/data')
  return data
}
```

```jsx
export async function getData() {
  'use cache'

  const data = await fetch('/api/data')
  return data
}
```

#### Revalidating

By default, Next.js sets a **revalidation period of 15 minutes** when you use the `use cache` directive. Next.js sets a near-infinite expiration duration, meaning it's suitable for content that doesn't need frequent updates.

While this revalidation period may be useful for content you don't expect to change often, you can use the `cacheLife` and `cacheTag` APIs to configure the cache behavior:

* `cacheLife`: For time-based revalidation periods.
* `cacheTag`: For on-demand revalidation.

Both of these APIs integrate across the client and server caching layers, meaning you can configure your caching semantics in one place and have them apply everywhere.

See the `cacheLife` and `cacheTag` docs for more information.

#### Interleaving

If you need to pass non-serializable arguments to a cacheable function, you can pass them as `children`. This means the `children` reference can change without affecting the cache entry.

```tsx
export default async function Page() {
  const uncachedData = await getData()
  return (
    <CacheComponent>
      <DynamicComponent data={uncachedData} />
    </CacheComponent>
  )
}

async function CacheComponent({ children }: { children: ReactNode }) {
  'use cache'
  const cachedData = await fetch('/api/cached-data')
  return (
    <div>
      <PrerenderedComponent data={cachedData} />
      {children}
    </div>
  )
}
```

```jsx
export default async function Page() {
  const uncachedData = await getData()
  return (
    <CacheComponent>
      <DynamicComponent data={uncachedData} />
    </CacheComponent>
  )
}

async function CacheComponent({ children }) {
  'use cache'
  const cachedData = await fetch('/api/cached-data')
  return (
    <div>
      <PrerenderedComponent data={cachedData} />
      {children}
    </div>
  )
}
```

You can also pass Server Actions through cached components to Client Components without invoking them inside the cacheable function.

```tsx
import ClientComponent from './ClientComponent'

export default async function Page() {
  const performUpdate = async () => {
    'use server'
    // Perform some server-side update
    await db.update(...)
  }

  return <CacheComponent performUpdate={performUpdate} />
}

async function CachedComponent({
  performUpdate,
}: {
  performUpdate: () => Promise<void>
}) {
  'use cache'
  // Do not call performUpdate here
  return <ClientComponent action={performUpdate} />
}
```

```jsx
import ClientComponent from './ClientComponent'

export default async function Page() {
  const performUpdate = async () => {
    'use server'
    // Perform some server-side update
    await db.update(...)
  }

  return <CacheComponent performUpdate={performUpdate} />
}

async function CachedComponent({ performUpdate }) {
  'use cache'
  // Do not call performUpdate here
  return <ClientComponent action={performUpdate} />
}
```

```tsx
'use client'

export default function ClientComponent({
  action,
}: {
  action: () => Promise<void>
}) {
  return <button onClick={action}>Update</button>
}
```

```jsx
'use client'

export default function ClientComponent({ action }) {
  return <button onClick={action}>Update</button>
}
```

### Related <a href="#related" id="related"></a>

View related API references.

{% content-ref url="../configuration/next.config.js/usecache.md" %}
[usecache.md](../configuration/next.config.js/usecache.md)
{% endcontent-ref %}

{% content-ref url="../configuration/next.config.js/dynamicio.md" %}
[dynamicio.md](../configuration/next.config.js/dynamicio.md)
{% endcontent-ref %}

{% content-ref url="../functions/cachelife.md" %}
[cachelife.md](../functions/cachelife.md)
{% endcontent-ref %}

{% content-ref url="../functions/cachetag.md" %}
[cachetag.md](../functions/cachetag.md)
{% endcontent-ref %}

{% content-ref url="../functions/cachelife.md" %}
[cachelife.md](../functions/cachelife.md)
{% endcontent-ref %}

{% content-ref url="../functions/revalidatetag.md" %}
[revalidatetag.md](../functions/revalidatetag.md)
{% endcontent-ref %}



