---
description: >-
  Next.js allows you to serve static files, like images, in the public
  directory. You can learn how it works here.
---

# Static Assets

## Static Assets in `public`

Next.js can serve static files, like images, under a folder called `public` in the root directory. Files inside `public` can then be referenced by your code starting from the base URL (`/`).

For example, the file `public/avatars/me.png` can be viewed by visiting the `/avatars/me.png` path. The code to display that image might look like:

```jsx
import Image from 'next/image'

export function Avatar({ id, alt }) {
  return <Image src={`/avatars/${id}.png`} alt={alt} width="64" height="64" />
}

export function AvatarOfMe() {
  return <Avatar id="me" alt="A portrait of me" />
}
```

### Caching

Next.js cannot safely cache assets in the `public` folder because they may change. The default caching headers applied are:

```jsx
Cache-Control: public, max-age=0
```

### Robots, Favicons, and others

The folder is also useful for `robots.txt`, `favicon.ico`, Google Site Verification, and any other static files (including `.html`). But make sure to not have a static file with the same name as a file in the `pages/` directory, as this will result in an error. Read more.

For static metadata files, such as `robots.txt`, `favicon.ico`, etc, you should use special metadata files inside the `app` folder.

> Good to know:
>
> * The directory must be named `public`. The name cannot be changed and it's the only directory used to serve static assets.
> * Only assets that are in the `public` directory at build time will be served by Next.js. Files added at request time won't be available. We recommend using a third-party service like [Vercel Blob](https://vercel.com/docs/storage/vercel-blob?utm_source=next-site\&utm_medium=docs\&utm_campaign=next-website) for persistent file storage.
