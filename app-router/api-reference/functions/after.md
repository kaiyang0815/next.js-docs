---
description: API Reference for the after function.
icon: bird
---

# after

`after` allows you to schedule work to be executed after a response (or prerender) is finished. This is useful for tasks and other side effects that should not block the response, such as logging and analytics.

It can be used in Server Components (including [`generateMetadata`](https://nextjs.org/docs/app/api-reference/functions/generate-metadata)), Server Actions, Route Handlers, and Middleware.

The function accepts a callback that will be executed after the response (or prerender) is finished:

```tsx
import { after } from 'next/server'
// Custom logging function
import { log } from '@/app/utils'

export default function Layout({ children }: { children: React.ReactNode }) {
  after(() => {
    // Execute after the layout is rendered and sent to the user
    log()
  })
  return <>{children}</>
}
```

```jsx
import { after } from 'next/server'
// Custom logging function
import { log } from '@/app/utils'

export default function Layout({ children }) {
  after(() => {
    // Execute after the layout is rendered and sent to the user
    log()
  })
  return <>{children}</>
}
```

> **Good to know:** `after` is not a Dynamic API and calling it does not cause a route to become dynamic. If it's used within a static page, the callback will execute at build time, or whenever a page is revalidated.

### Reference

#### Parameters

* A callback function which will be executed after the response (or prerender) is finished.

#### Duration

`after` will run for the platform's default or configured max duration of your route. If your platform supports it, you can configure the timeout limit using the `maxDuration` route segment config.

### Good to know

* `after` will be executed even if the response didn't complete successfully. Including when an error is thrown or when `notFound` or `redirect` is called.
* You can use React `cache` to deduplicate functions called inside `after`.
* `after` can be nested inside other `after` calls, for example, you can create utility functions that wrap `after` calls to add additional functionality.

### Alternatives

The use case for `after` is to process secondary tasks without blocking the primary response. It's similar to using the platform's [`waitUntil()`](https://vercel.com/docs/functions/functions-api-reference) or removing `await` from a promise, but with the following differences:

* **`waitUntil()`**: accepts a promise and enqueues a task to be executed during the lifecycle of the request, whereas `after` accepts a callback that will be executed **after** the response is finished.
* **Removing `await`**: starts executing during the response, which uses resources. It's also not reliable in serverless environments as the function stops computation immediately after the response is sent, potentially interrupting the task.

We recommend using `after` as it has been designed to consider other Next.js APIs and contexts.

### Examples

#### With request APIs

You can use request APIs such as `cookies` and `headers` inside `after` in Server Actions and Route Handlers. This is useful for logging activity after a mutation. For example:

```ts
import { after } from 'next/server'
import { cookies, headers } from 'next/headers'
import { logUserAction } from '@/app/utils'

export async function POST(request: Request) {
  // Perform mutation
  // ...

  // Log user activity for analytics
  after(async () => {
    const userAgent = (await headers().get('user-agent')) || 'unknown'
    const sessionCookie =
      (await cookies().get('session-id'))?.value || 'anonymous'

    logUserAction({ sessionCookie, userAgent })
  })

  return new Response(JSON.stringify({ status: 'success' }), {
    status: 200,
    headers: { 'Content-Type': 'application/json' },
  })
}
```

```js
import { after } from 'next/server'
import { cookies, headers } from 'next/headers'
import { logUserAction } from '@/app/utils'

export async function POST(request) {
  // Perform mutation
  // ...

  // Log user activity for analytics
  after(async () => {
    const userAgent = (await headers().get('user-agent')) || 'unknown'
    const sessionCookie =
      (await cookies().get('session-id'))?.value || 'anonymous'

    logUserAction({ sessionCookie, userAgent })
  })

  return new Response(JSON.stringify({ status: 'success' }), {
    status: 200,
    headers: { 'Content-Type': 'application/json' },
  })
}
```

However, you cannot use these request APIs inside `after` in Server Components. This is because Next.js needs to know which part of the tree access the request APIs to support Partial Prerendering, but `after` runs after React's rendering lifecycle.

| Version History | Description                  |
| --------------- | ---------------------------- |
| `v15.1.0`       | `after` became stable.       |
| `v15.0.0-rc`    | `unstable_after` introduced. |
