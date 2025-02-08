---
description: >-
  Learn how to enable the experimental `authInterrupts` configuration option to
  use `forbidden` and `unauthorized`.
icon: bird
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

### Next Steps <a href="#next-steps" id="next-steps"></a>

{% content-ref url="../../functions/forbidden.md" %}
[forbidden.md](../../functions/forbidden.md)
{% endcontent-ref %}

{% content-ref url="../../functions/unauthorized.md" %}
[unauthorized.md](../../functions/unauthorized.md)
{% endcontent-ref %}

{% content-ref url="../../file-conventions/forbidden.js.md" %}
[forbidden.js.md](../../file-conventions/forbidden.js.md)
{% endcontent-ref %}

{% content-ref url="../../file-conventions/unauthorized.js.md" %}
[unauthorized.js.md](../../file-conventions/unauthorized.js.md)
{% endcontent-ref %}

