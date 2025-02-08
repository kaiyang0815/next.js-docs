---
description: Optimize your Next.js application for best performance and user experience.
---

# Optimizing

## Optimizations

Next.js comes with a variety of built-in optimizations designed to improve your application's speed and [Core Web Vitals](https://web.dev/vitals/). This guide will cover the optimizations you can leverage to enhance your user experience.

### Built-in Components

Built-in components abstract away the complexity of implementing common UI optimizations. These components are:

* **Images**: Built on the native `<img>` element. The Image Component optimizes images for performance by lazy loading and automatically resizing images based on device size.
* **Link**: Built on the native `<a>` tags. The Link Component prefetches pages in the background, for faster and smoother page transitions.
* **Scripts**: Built on the native `<script>` tags. The Script Component gives you control over loading and execution of third-party scripts.

### Metadata

Metadata helps search engines understand your content better (which can result in better SEO), and allows you to customize how your content is presented on social media, helping you create a more engaging and consistent user experience across various platforms.

The Metadata API in Next.js allows you to modify the `<head>` element of a page. You can configure metadata in two ways:

* **Config-based Metadata**: Export a static `metadata` object or a dynamic `generateMetadata` function in a `layout.js` or `page.js` file.
* **File-based Metadata**: Add static or dynamically generated special files to route segments.

Additionally, you can create dynamic Open Graph Images using JSX and CSS with imageResponse constructor.

The Head Component in Next.js allows you to modify the `<head>` of a page. Learn more in the Head Component documentation.

### Static Assets

Next.js `/public` folder can be used to serve static assets like images, fonts, and other files. Files inside `/public` can also be cached by CDN providers so that they are delivered efficiently.

### Analytics and Monitoring

For large applications, Next.js integrates with popular analytics and monitoring tools to help you understand how your application is performing. Learn more in the Analytics, OpenTelemetry, and Instrumentation guides.

{% content-ref url="image-optimization.md" %}
[image-optimization.md](image-optimization.md)
{% endcontent-ref %}

{% content-ref url="videos.md" %}
[videos.md](videos.md)
{% endcontent-ref %}

{% content-ref url="fonts.md" %}
[fonts.md](fonts.md)
{% endcontent-ref %}

{% content-ref url="metadata.md" %}
[metadata.md](metadata.md)
{% endcontent-ref %}

{% content-ref url="scripts.md" %}
[scripts.md](scripts.md)
{% endcontent-ref %}

{% content-ref url="package-bundling.md" %}
[package-bundling.md](package-bundling.md)
{% endcontent-ref %}

{% content-ref url="lazy-loading.md" %}
[lazy-loading.md](lazy-loading.md)
{% endcontent-ref %}

{% content-ref url="analytics.md" %}
[analytics.md](analytics.md)
{% endcontent-ref %}

{% content-ref url="instrumentation.md" %}
[instrumentation.md](instrumentation.md)
{% endcontent-ref %}

{% content-ref url="opentelemetry.md" %}
[opentelemetry.md](opentelemetry.md)
{% endcontent-ref %}

{% content-ref url="static-assets.md" %}
[static-assets.md](static-assets.md)
{% endcontent-ref %}

{% content-ref url="third-party-libraries.md" %}
[third-party-libraries.md](third-party-libraries.md)
{% endcontent-ref %}

{% content-ref url="memory-usage.md" %}
[memory-usage.md](memory-usage.md)
{% endcontent-ref %}

