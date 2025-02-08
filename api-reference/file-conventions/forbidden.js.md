---
description: API reference for the forbidden.js special file.
---

# forbidden.js

The **forbidden** file is used to render UI when the `forbidden` function is invoked during authentication. Along with allowing you to customize the UI, Next.js will return a `403` status code.

```tsx
import Link from 'next/link'

export default function Forbidden() {
  return (
    <div>
      <h2>Forbidden</h2>
      <p>You are not authorized to access this resource.</p>
      <Link href="/">Return Home</Link>
    </div>
  )
}
```

```jsx
import Link from 'next/link'

export default function Forbidden() {
  return (
    <div>
      <h2>Forbidden</h2>
      <p>You are not authorized to access this resource.</p>
      <Link href="/">Return Home</Link>
    </div>
  )
}
```

### Reference

#### Props

`forbidden.js` components do not accept any props.

### Version History

| Version   | Changes                    |
| --------- | -------------------------- |
| `v15.1.0` | `forbidden.js` introduced. |

### Next Steps <a href="#next-steps" id="next-steps"></a>

{% content-ref url="../functions/forbidden.md" %}
[forbidden.md](../functions/forbidden.md)
{% endcontent-ref %}

