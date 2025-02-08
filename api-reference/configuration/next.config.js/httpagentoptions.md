---
description: >-
  Next.js will automatically use HTTP Keep-Alive by default. Learn more about
  how to disable HTTP Keep-Alive here.
---

# httpAgentOptions

In Node.js versions prior to 18, Next.js automatically polyfills `fetch()` with undici and enables [HTTP Keep-Alive](https://developer.mozilla.org/docs/Web/HTTP/Headers/Keep-Alive) by default.

To disable HTTP Keep-Alive for all `fetch()` calls on the server-side, open `next.config.js` and add the `httpAgentOptions` config:

```js
module.exports = {
  httpAgentOptions: {
    keepAlive: false,
  },
}
```
