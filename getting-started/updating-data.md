---
description: Learn how to update data in your Next.js application.
---

# Updating Data

You can update data in Next.js using React's [Server Functions](https://react.dev/reference/rsc/server-functions). This page will go through how you can create and invoke Server Functions.

### Creating Server Functions

A Server Function can be defined by using the [`use server`](https://react.dev/reference/rsc/use-server) directive. You can place the directive at the top of an **asynchronous** function to mark the function as a Server Function, or at the top of a separate file to mark all exports of that file. We recommend using a separate file in most instances.

```ts
'use server'

export async function createPost(formData: FormData) {}

export async function deletePost(formData: FormData) {}
```

```js
'use server'

export async function createPost(formData) {}

export async function deletePost(formData) {}
```

#### Server Components

Server Functions can be inlined in Server Components by adding the `"use server"` directive to the top of the function body:

```tsx
export default function Page() {
  // Server Action
  async function createPost() {
    'use server'
    // Update data
    // ...

  return <></>
}
```

```jsx
export default function Page() {
  // Server Action
  async function createPost() {
    'use server'
    // Update data
    // ...
  }

  return <></>
}
```

#### Client Components

It's not possible to define Server Functions in Client Components. However, you can invoke them in Client Components by importing them from a file that has the `"use server"` directive at the top of it:

```ts
'use server'

export async function createPost() {}
```

```js
'use server'

export async function createPost() {}
```

```tsx
'use client'

import { createPost } from '@/app/actions'

export function Button() {
  return <button formAction={createPost}>Create</button>
}
```

```jsx
'use client'

import { createPost } from '@/app/actions'

export function Button() {
  return <button formAction={createPost}>Create</button>
}
```

### Invoking Server Functions

There are two mains ways you can invoke a Server Function:

1. Forms in Server and Client Components
2. Event Handlers in Client Components

#### Forms

React extends the HTML [`<form>`](https://react.dev/reference/react-dom/components/form) element to allow Server Function to be invoked with the HTML `action` prop.

When invoked in a form, the function automatically receives the [`FormData`](https://developer.mozilla.org/docs/Web/API/FormData/FormData) object. You can extract the data using the native [`FormData` methods](https://developer.mozilla.org/en-US/docs/Web/API/FormData#instance_methods):

```tsx
import { createPost } from '@/app/actions'

export function Form() {
  return (
    <form action={createPost}>
      <input type="text" name="title" />
      <input type="text" name="content" />
      <button type="submit">Create</button>
    </form>
  )
}
```

```jsx
import { createPost } from '@/app/actions'

export function Form() {
  return (
    <form action={createPost}>
      <input type="text" name="title" />
      <input type="text" name="content" />
      <button type="submit">Create</button>
    </form>
  )
}
```

```ts
'use server'

export async function createPost(formData: FormData) {
  const title = formData.get('title')
  const content = formData.get('content')

  // Update data
  // Revalidate cache
}
```

```js
'use server'

export async function createPost(formData) {
  const title = formData.get('title')
  const content = formData.get('content')

  // Update data
  // Revalidate cache
}
```

> **Good to know:** When passed to the `action` prop, Server Functions are also known as _Server Actions_.

#### Event Handlers

You can invoke a Server Function in a Client Component by using event handlers such as `onClick`.

```tsx
'use client'

import { incrementLike } from './actions'
import { useState } from 'react'

export default function LikeButton({ initialLikes }: { initialLikes: number }) {
  const [likes, setLikes] = useState(initialLikes)

  return (
    <>
      <p>Total Likes: {likes}</p>
      <button
        onClick={async () => {
          const updatedLikes = await incrementLike()
          setLikes(updatedLikes)
        }}
      >
        Like
      </button>
    </>
  )
}
```

```jsx
'use client'

import { incrementLike } from './actions'
import { useState } from 'react'

export default function LikeButton({ initialLikes }) {
  const [likes, setLikes] = useState(initialLikes)

  return (
    <>
      <p>Total Likes: {likes}</p>
      <button
        onClick={async () => {
          const updatedLikes = await incrementLike()
          setLikes(updatedLikes)
        }}
      >
        Like
      </button>
    </>
  )
}
```

#### Showing a pending state

While executing a Server Function, you can show a loading indicator with React's [`useActionState`](https://react.dev/reference/react/useActionState) hook. This hook returns a `pending` boolean:

```tsx
'use client'

import { useActionState } from 'react'
import { createPost } from '@/app/actions'
import { LoadingSpinner } from '@/app/ui/loading-spinner'

export function Button() {
  const [state, action, pending] = useActionState(createPost, false)

  return (
    <button onClick={async () => action()}>
      {pending ? <LoadingSpinner /> : 'Create Post'}
    </button>
  )
}
```

```jsx
'use client'

import { useActionState } from 'react'
import { createPost } from '@/app/actions'
import { LoadingSpinner } from '@/app/ui/loading-spinner'

export function Button() {
  const [state, action, pending] = useActionState(createPost, false)

  return (
    <button onClick={async () => action()}>
      {pending ? <LoadingSpinner /> : 'Create Post'}
    </button>
  )
}
```

#### Revalidating the cache

After performing an update, you can revalidate the Next.js cache and show the updated data by calling `revalidatePath` or `revalidateTag` within the Server Function:

```ts
'use server'

import { revalidatePath } from 'next/cache'

export async function createPost(formData: FormData) {
  // Update data
  // ...

  revalidatePath('/posts')
}
```

```js
'use server'

import { revalidatePath } from 'next/cache'

export async function createPost(formData) {
  // Update data
  // ...
  revalidatePath('/posts')
}
```

#### Redirecting

You may want to redirect the user to a different page after performing an update. You can do this by calling `redirect` within the Server Function:

```ts
'use server'

import { redirect } from 'next/navigation'

export async function createPost(formData: FormData) {
  // Update data
  // ...

  redirect('/posts')
}
```

```js
'use server'

import { redirect } from 'next/navigation'

export async function createPost(formData) {
  // Update data
  // ...

  redirect('/posts')
}
```

### API Reference <a href="#api-reference" id="api-reference"></a>

Learn more about the features mentioned in this page by reading the API Reference.

{% content-ref url="../api-reference/functions/revalidatepath.md" %}
[revalidatepath.md](../api-reference/functions/revalidatepath.md)
{% endcontent-ref %}

{% content-ref url="../api-reference/functions/revalidatetag.md" %}
[revalidatetag.md](../api-reference/functions/revalidatetag.md)
{% endcontent-ref %}

{% content-ref url="../api-reference/functions/redirect.md" %}
[redirect.md](../api-reference/functions/redirect.md)
{% endcontent-ref %}

