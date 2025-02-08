---
description: >-
  Learn how to use the cacheTag function to manage cache invalidation in your
  Next.js application.
---

# cacheTag

The `cacheTag` function allows you to tag cached data for on-demand invalidation. By associating tags with cache entries, you can selectively purge or revalidate specific cache entries without affecting other cached data.

### Usage

To use `cacheTag`, enable the `dynamicIO` flag in your `next.config.js` file:

```ts
import type { NextConfig } from 'next'

const nextConfig: NextConfig = {
  experimental: {
    dynamicIO: true,
  },
}

export default nextConfig
```

```js
const nextConfig = {
  experimental: {
    dynamicIO: true,
  },
}

export default nextConfig
```

The `cacheTag` function takes a single string value, or a string array.

```tsx
import { unstable_cacheTag as cacheTag } from 'next/cache'

export async function getData() {
  'use cache'
  cacheTag('my-data')
  const data = await fetch('/api/data')
  return data
}
```

```jsx
import { unstable_cacheTag as cacheTag } from 'next/cache'

export async function getData() {
  'use cache'
  cacheTag('my-data')
  const data = await fetch('/api/data')
  return data
}
```

You can then purge the cache on-demand using `revalidateTag` API in another function, for example, a route handler or Server Action:

```tsx
'use server'

import { revalidateTag } from 'next/cache'

export default async function submit() {
  await addPost()
  revalidateTag('my-data')
}
```

```jsx
'use server'

import { revalidateTag } from 'next/cache'

export default async function submit() {
  await addPost()
  revalidateTag('my-data')
}
```

### Good to know

* **Idempotent Tags**: Applying the same tag multiple times has no additional effect.
* **Multiple Tags**: You can assign multiple tags to a single cache entry by passing an array to `cacheTag`.

```tsx
cacheTag('tag-one', 'tag-two')
```

### Examples

#### Tagging components or functions

Tag your cached data by calling `cacheTag` within a cached function or component:

```tsx
import { unstable_cacheTag as cacheTag } from 'next/cache'

interface BookingsProps {
  type: string
}

export async function Bookings({ type = 'haircut' }: BookingsProps) {
  'use cache'
  cacheTag('bookings-data')

  async function getBookingsData() {
    const data = await fetch(`/api/bookings?type=${encodeURIComponent(type)}`)
    return data
  }

  return //...
}
```

```jsx
import { unstable_cacheTag as cacheTag } from 'next/cache'

export async function Bookings({ type = 'haircut' }) {
  'use cache'
  cacheTag('bookings-data')

  async function getBookingsData() {
    const data = await fetch(`/api/bookings?type=${encodeURIComponent(type)}`)
    return data
  }

  return //...
}
```

#### Creating tags from external data

You can use the data returned from an async function to tag the cache entry.

```tsx
import { unstable_cacheTag as cacheTag } from 'next/cache'

interface BookingsProps {
  type: string
}

export async function Bookings({ type = 'haircut' }: BookingsProps) {
  async function getBookingsData() {
    'use cache'
    const data = await fetch(`/api/bookings?type=${encodeURIComponent(type)}`)
    cacheTag('bookings-data', data.id)
    return data
  }
  return //...
}
```

```jsx
import { unstable_cacheTag as cacheTag } from 'next/cache'

export async function Bookings({ type = 'haircut' }) {
  async function getBookingsData() {
    'use cache'
    const data = await fetch(`/api/bookings?type=${encodeURIComponent(type)}`)
    cacheTag('bookings-data', data.id)
    return data
  }
  return //...
}
```

#### Invalidating tagged cache

Using `revalidateTag`, you can invalidate the cache for a specific tag when needed:

```tsx
'use server'

import { revalidateTag } from 'next/cache'

export async function updateBookings() {
  await updateBookingData()
  revalidateTag('bookings-data')
}
```

```jsx
'use server'

import { revalidateTag } from 'next/cache'

export async function updateBookings() {
  await updateBookingData()
  revalidateTag('bookings-data')
}
```

### Related <a href="#related" id="related"></a>

View related API references.

{% content-ref url="../configuration/next.config.js/dynamicio.md" %}
[dynamicio.md](../configuration/next.config.js/dynamicio.md)
{% endcontent-ref %}

{% content-ref url="../directives/use-cache.md" %}
[use-cache.md](../directives/use-cache.md)
{% endcontent-ref %}

{% content-ref url="revalidatetag.md" %}
[revalidatetag.md](revalidatetag.md)
{% endcontent-ref %}

{% content-ref url="cachelife.md" %}
[cachelife.md](cachelife.md)
{% endcontent-ref %}

