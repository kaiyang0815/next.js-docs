---
description: Learn about the switchable runtimes (Edge and Node.js) in Next.js.
---

# Runtimes

Next.js has two server runtimes you can use in your application:

* The **Node.js Runtime** (default), which has access to all Node.js APIs and compatible packages from the ecosystem.
* The **Edge Runtime** which contains a more limited set of APIs.

### Use Cases

* The Node.js Runtime is used for rendering your application.
* The Edge Runtime is used for Middleware (routing rules like redirects, rewrites, and setting headers).

### Caveats

* The Edge Runtime does not support all Node.js APIs. Some packages may not work as expected. Learn more about the unsupported APIs in the Edge Runtime.
* The Edge Runtime does not support Incremental Static Regeneration (ISR).
* Both runtimes can support streaming depending on your deployment infrastructure.

### Next Steps <a href="#next-steps" id="next-steps"></a>

View the Edge Runtime API reference.

{% content-ref url="../../api-reference/edge-runtime.md" %}
[edge-runtime.md](../../api-reference/edge-runtime.md)
{% endcontent-ref %}
