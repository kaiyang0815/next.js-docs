---
description: API Reference for the Favicon, Icon and Apple Icon file conventions.
---

# favicon, icon, and apple-icon

The `favicon`, `icon`, or `apple-icon` file conventions allow you to set icons for your application.

They are useful for adding app icons that appear in places like web browser tabs, phone home screens, and search engine results.

There are two ways to set app icons:

* Using image files (.ico, .jpg, .png)
* Using code to generate an icon (.js, .ts, .tsx)

### Image files (.ico, .jpg, .png)

Use an image file to set an app icon by placing a `favicon`, `icon`, or `apple-icon` image file within your `/app` directory. The `favicon` image can only be located in the top level of `app/`.

Next.js will evaluate the file and automatically add the appropriate tags to your app's `<head>` element.

| File convention | Supported file types                    | Valid locations |
| --------------- | --------------------------------------- | --------------- |
| `favicon`       | `.ico`                                  | `app/`          |
| `icon`          | `.ico`, `.jpg`, `.jpeg`, `.png`, `.svg` | `app/**/*`      |
| `apple-icon`    | `.jpg`, `.jpeg`, `.png`                 | `app/**/*`      |

#### `favicon`

Add a `favicon.ico` image file to the root `/app` route segment.

```html
<link rel="icon" href="/favicon.ico" sizes="any" />
```

#### `icon`

Add an `icon.(ico|jpg|jpeg|png|svg)` image file.

```html
<link
  rel="icon"
  href="/icon?<generated>"
  type="image/<generated>"
  sizes="<generated>"
/>
```

#### `apple-icon`

Add an `apple-icon.(jpg|jpeg|png)` image file.

```html
<link
  rel="apple-touch-icon"
  href="/apple-icon?<generated>"
  type="image/<generated>"
  sizes="<generated>"
/>
```

> **Good to know**:
>
> * You can set multiple icons by adding a number suffix to the file name. For example, `icon1.png`, `icon2.png`, etc. Numbered files will sort lexically.
> * Favicons can only be set in the root `/app` segment. If you need more granularity, you can use `icon`.
> * The appropriate `<link>` tags and attributes such as `rel`, `href`, `type`, and `sizes` are determined by the icon type and metadata of the evaluated file.
> * For example, a 32 by 32px `.png` file will have `type="image/png"` and `sizes="32x32"` attributes.
> * `sizes="any"` is added to icons when the extension is `.svg` or the image size of the file is not determined. More details in this [favicon handbook](https://evilmartians.com/chronicles/how-to-favicon-in-2021-six-files-that-fit-most-needs).

### Generate icons using code (.js, .ts, .tsx)

In addition to using literal image files, you can programmatically **generate** icons using code.

Generate an app icon by creating an `icon` or `apple-icon` route that default exports a function.

| File convention | Supported file types |
| --------------- | -------------------- |
| `icon`          | `.js`, `.ts`, `.tsx` |
| `apple-icon`    | `.js`, `.ts`, `.tsx` |

The easiest way to generate an icon is to use the `ImageResponse` API from `next/og`.

```tsx
import { ImageResponse } from 'next/og'

// Image metadata
export const size = {
  width: 32,
  height: 32,
}
export const contentType = 'image/png'

// Image generation
export default function Icon() {
  return new ImageResponse(
    (
      // ImageResponse JSX element
      <div
        style={{
          fontSize: 24,
          background: 'black',
          width: '100%',
          height: '100%',
          display: 'flex',
          alignItems: 'center',
          justifyContent: 'center',
          color: 'white',
        }}
      >
        A
      </div>
    ),
    // ImageResponse options
    {
      // For convenience, we can re-use the exported icons size metadata
      // config to also set the ImageResponse's width and height.
      ...size,
    }
  )
}
```

```jsx
import { ImageResponse } from 'next/og'

// Image metadata
export const size = {
  width: 32,
  height: 32,
}
export const contentType = 'image/png'

// Image generation
export default function Icon() {
  return new ImageResponse(
    (
      // ImageResponse JSX element
      <div
        style={{
          fontSize: 24,
          background: 'black',
          width: '100%',
          height: '100%',
          display: 'flex',
          alignItems: 'center',
          justifyContent: 'center',
          color: 'white',
        }}
      >
        A
      </div>
    ),
    // ImageResponse options
    {
      // For convenience, we can re-use the exported icons size metadata
      // config to also set the ImageResponse's width and height.
      ...size,
    }
  )
}
```

```html
<link rel="icon" href="/icon?<generated>" type="image/png" sizes="32x32" />
```

> **Good to know**:
>
> * By default, generated icons are **statically optimized** (generated at build time and cached) unless they use Dynamic APIs or uncached data.
> * You can generate multiple icons in the same file using `generateImageMetadata`.
> * You cannot generate a `favicon` icon. Use `icon` or a favicon.ico file instead.
> * App icons are special Route Handlers that is cached by default unless it uses a Dynamic API or dynamic config option.

#### Props

The default export function receives the following props:

**`params` (optional)**

An object containing the dynamic route parameters object from the root segment down to the segment `icon` or `apple-icon` is colocated in.

```tsx
export default function Icon({ params }: { params: { slug: string } }) {
  // ...
}
```

```jsx
export default function Icon({ params }) {
  // ...
}
```

| Route                           | URL         | `params`                  |
| ------------------------------- | ----------- | ------------------------- |
| `app/shop/icon.js`              | `/shop`     | `undefined`               |
| `app/shop/[slug]/icon.js`       | `/shop/1`   | `{ slug: '1' }`           |
| `app/shop/[tag]/[item]/icon.js` | `/shop/1/2` | `{ tag: '1', item: '2' }` |

#### Returns

The default export function should return a `Blob` | `ArrayBuffer` | `TypedArray` | `DataView` | `ReadableStream` | `Response`.

> **Good to know**: `ImageResponse` satisfies this return type.

#### Config exports

You can optionally configure the icon's metadata by exporting `size` and `contentType` variables from the `icon` or `apple-icon` route.

| Option        | Type                                                                                                            |
| ------------- | --------------------------------------------------------------------------------------------------------------- |
| `size`        | `{ width: number; height: number }`                                                                             |
| `contentType` | `string` - [image MIME type](https://developer.mozilla.org/docs/Web/HTTP/Basics_of_HTTP/MIME_types#image_types) |

**`size`**

```tsx
export const size = { width: 32, height: 32 }

export default function Icon() {}
```

```jsx
export const size = { width: 32, height: 32 }

export default function Icon() {}
```

```html
<link rel="icon" sizes="32x32" />
```

**`contentType`**

```tsx
export const contentType = 'image/png'

export default function Icon() {}
```

```jsx
export const contentType = 'image/png'

export default function Icon() {}
```

```html
<link rel="icon" type="image/png" />
```

**Route Segment Config**

`icon` and `apple-icon` are specialized Route Handlers that can use the same route segment configuration options as Pages and Layouts.

### Version History

| Version   | Changes                                      |
| --------- | -------------------------------------------- |
| `v13.3.0` | `favicon` `icon` and `apple-icon` introduced |
