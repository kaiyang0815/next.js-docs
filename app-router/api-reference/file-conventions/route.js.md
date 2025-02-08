---
description: API reference for the route.js special file.
---

# route.js

Route Handlers allow you to create custom request handlers for a given route using the Web [Request](https://developer.mozilla.org/docs/Web/API/Request) and [Response](https://developer.mozilla.org/docs/Web/API/Response) APIs.

```ts
export async function GET() {
  return Response.json({ message: 'Hello World' })
}
```

```js
export async function GET() {
  return Response.json({ message: 'Hello World' })
}
```

### Reference

#### HTTP Methods

A **route** file allows you to create custom request handlers for a given route. The following [HTTP methods](https://developer.mozilla.org/docs/Web/HTTP/Methods) are supported: `GET`, `POST`, `PUT`, `PATCH`, `DELETE`, `HEAD`, and `OPTIONS`.

```ts
export async function GET(request: Request) {}

export async function HEAD(request: Request) {}

export async function POST(request: Request) {}

export async function PUT(request: Request) {}

export async function DELETE(request: Request) {}

export async function PATCH(request: Request) {}

// If `OPTIONS` is not defined, Next.js will automatically implement `OPTIONS` and set the appropriate Response `Allow` header depending on the other methods defined in the Route Handler.
export async function OPTIONS(request: Request) {}
```

```js
export async function GET(request) {}

export async function HEAD(request) {}

export async function POST(request) {}

export async function PUT(request) {}

export async function DELETE(request) {}

export async function PATCH(request) {}

// If `OPTIONS` is not defined, Next.js will automatically implement `OPTIONS` and set the appropriate Response `Allow` header depending on the other methods defined in the Route Handler.
export async function OPTIONS(request) {}
```

#### Parameters

**`request` (optional)**

The `request` object is a NextRequest object, which is an extension of the Web [Request](https://developer.mozilla.org/docs/Web/API/Request) API. `NextRequest` gives you further control over the incoming request, including easily accessing `cookies` and an extended, parsed, URL object `nextUrl`.

```ts
import type { NextRequest } from 'next/server'

export async function GET(request: NextRequest) {
  const url = request.nextUrl
}
```

```js
export async function GET(request) {
  const url = request.nextUrl
}
```

**`context` (optional)**

* **`params`**: a promise that resolves to an object containing the dynamic route parameters for the current route.

```ts
export async function GET(
  request: Request,
  { params }: { params: Promise<{ team: string }> }
) {
  const team = (await params).team
}
```

```js
export async function GET(request, { params }) {
  const team = (await params).team
}
```

| Example                          | URL            | `params`                           |
| -------------------------------- | -------------- | ---------------------------------- |
| `app/dashboard/[team]/route.js`  | `/dashboard/1` | `Promise<{ team: '1' }>`           |
| `app/shop/[tag]/[item]/route.js` | `/shop/1/2`    | `Promise<{ tag: '1', item: '2' }>` |
| `app/blog/[...slug]/route.js`    | `/blog/1/2`    | `Promise<{ slug: ['1', '2'] }>`    |

### Examples

#### Handling cookies

```ts
import { cookies } from 'next/headers'

export async function GET(request: NextRequest) {
  const cookieStore = await cookies()

  const a = cookieStore.get('a')
  const b = cookieStore.set('b', '1')
  const c = cookieStore.delete('c')
}
```

```js
import { cookies } from 'next/headers'

export async function GET(request) {
  const cookieStore = await cookies()

  const a = cookieStore.get('a')
  const b = cookieStore.set('b', '1')
  const c = cookieStore.delete('c')
}
```

### Version History

| Version      | Changes                                                                   |
| ------------ | ------------------------------------------------------------------------- |
| `v15.0.0-RC` | `context.params` is now a promise. A codemod is available                 |
| `v15.0.0-RC` | The default caching for `GET` handlers was changed from static to dynamic |
| `v13.2.0`    | Route Handlers are introduced.                                            |
