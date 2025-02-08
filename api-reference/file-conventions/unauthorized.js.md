---
description: API reference for the unauthorized.js special file.
---

# unauthorized.js

The **unauthorized** file is used to render UI when the `unauthorized` function is invoked during authentication. Along with allowing you to customize the UI, Next.js will return a `401` status code.

```tsx
import Login from '@/app/components/Login'

export default function Unauthorized() {
  return (
    <main>
      <h1>401 - Unauthorized</h1>
      <p>Please log in to access this page.</p>
      <Login />
    </main>
  )
}
```

```jsx
import Login from '@/app/components/Login'

export default function Unauthorized() {
  return (
    <main>
      <h1>401 - Unauthorized</h1>
      <p>Please log in to access this page.</p>
      <Login />
    </main>
  )
}
```

### Reference

#### Props

`unauthorized.js` components do not accept any props.

### Examples

#### Displaying login UI to unauthenticated users

You can use `unauthorized` function to render the `unauthorized.js` file with a login UI.

```tsx
import { verifySession } from '@/app/lib/dal'
import { unauthorized } from 'next/server'

export default async function DashboardPage() {
  const session = await verifySession()

  if (!session) {
    unauthorized()
  }

  return <div>Dashboard</div>
}
```

```jsx
import { verifySession } from '@/app/lib/dal'
import { unauthorized } from 'next/navigation'

export default async function DashboardPage() {
  const session = await verifySession()

  if (!session) {
    unauthorized()
  }

  return <div>Dashboard</div>
}
```

```tsx
import Login from '@/app/components/Login'

export default function UnauthorizedPage() {
  return (
    <main>
      <h1>401 - Unauthorized</h1>
      <p>Please log in to access this page.</p>
      <Login />
    </main>
  )
}
```

```jsx
import Login from '@/app/components/Login'

export default function UnauthorizedPage() {
  return (
    <main>
      <h1>401 - Unauthorized</h1>
      <p>Please log in to access this page.</p>
      <Login />
    </main>
  )
}
```

### Version History

| Version   | Changes                       |
| --------- | ----------------------------- |
| `v15.1.0` | `unauthorized.js` introduced. |

### Next Steps <a href="#next-steps" id="next-steps"></a>

{% content-ref url="../functions/unauthorized.md" %}
[unauthorized.md](../functions/unauthorized.md)
{% endcontent-ref %}

