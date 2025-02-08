---
description: API documentation for the metadata file conventions.
---

# Metadata Files

## Metadata Files API Reference

This section of the docs covers **Metadata file conventions**. File-based metadata can be defined by adding special metadata files to route segments.

Each file convention can be defined using a static file (e.g. `opengraph-image.jpg`), or a dynamic variant that uses code to generate the file (e.g. `opengraph-image.js`).

Once a file is defined, Next.js will automatically serve the file (with hashes in production for caching) and update the relevant head elements with the correct metadata, such as the asset's URL, file type, and image size.

> **Good to know**:
>
> * Special Route Handlers like `sitemap.ts`, `opengraph-image.tsx`, and `icon.tsx`, and other metadata files are cached by default.
> * If using along with `middleware.ts`, configure the matcher to exclude the metadata files.

{% content-ref url="favicon-icon-and-apple-icon.md" %}
[favicon-icon-and-apple-icon.md](favicon-icon-and-apple-icon.md)
{% endcontent-ref %}

{% content-ref url="manifest.json.md" %}
[manifest.json.md](manifest.json.md)
{% endcontent-ref %}

{% content-ref url="opengraph-image-and-twitter-image.md" %}
[opengraph-image-and-twitter-image.md](opengraph-image-and-twitter-image.md)
{% endcontent-ref %}

{% content-ref url="robots.txt.md" %}
[robots.txt.md](robots.txt.md)
{% endcontent-ref %}

{% content-ref url="sitemap.xml.md" %}
[sitemap.xml.md](sitemap.xml.md)
{% endcontent-ref %}

