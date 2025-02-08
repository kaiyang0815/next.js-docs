---
description: >-
  Style your Next.js Application with CSS Modules, Global Styles, and external
  stylesheets.
---

# CSS

<details>

<summary>Examples</summary>

* [Basic CSS Example](https://github.com/vercel/next.js/tree/canary/examples/basic-css)

</details>

Next.js supports multiple ways of handling CSS, including:

* CSS Modules
* Global Styles
* External Stylesheets

### CSS Modules

Next.js has built-in support for CSS Modules using the `.module.css` extension.

CSS Modules locally scope CSS by automatically creating a unique class name. This allows you to use the same class name in different files without worrying about collisions. This behavior makes CSS Modules the ideal way to include component-level CSS.

#### Example

CSS Modules can be imported into any file inside the \`app\` directory:

```tsx
import styles from './styles.module.css'

export default function DashboardLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return <section className={styles.dashboard}>{children}</section>
}
```

```jsx
import styles from './styles.module.css'

export default function DashboardLayout({ children }) {
  return <section className={styles.dashboard}>{children}</section>
}
```

```css
.dashboard {
  padding: 24px;
}
```

For example, consider a reusable `Button` component in the `components/` folder:

First, create `components/Button.module.css` with the following content:

```css
/*
You do not need to worry about .error {} colliding with any other `.css` or
`.module.css` files!
*/
.error {
  color: white;
  background-color: red;
}
```

Then, create `components/Button.js`, importing and using the above CSS file:

```jsx
import styles from './Button.module.css'

export function Button() {
  return (
    <button
      type="button"
      // Note how the "error" class is accessed as a property on the imported
      // `styles` object.
      className={styles.error}
    >
      Destroy
    </button>
  )
}
```

CSS Modules are **only enabled for files with the `.module.css` and `.module.sass` extensions**.

In production, all CSS Module files will be automatically concatenated into **many minified and code-split** `.css` files. These `.css` files represent hot execution paths in your application, ensuring the minimal amount of CSS is loaded for your application to paint.

### Global Styles

Global styles can be imported into any layout, page, or component inside the \`app\` directory.

> **Good to know**:
>
> * This is different from the `pages` directory, where you can only import global styles inside the `_app.js` file.
> * Next.js does not support usage of global styles unless they are actually global, meaning they can apply to all pages and can live for the lifetime of the application. This is because Next.js uses React's built-in support for stylesheets to integrate with Suspense. This built-in support currently does not remove stylesheets as you navigate between routes. Because of this, we recommend using CSS Modules over global styles.

For example, consider a stylesheet named `app/global.css`:

```css
body {
  padding: 20px 20px 60px;
  max-width: 680px;
  margin: 0 auto;
}
```

Inside the root layout (`app/layout.js`), import the `global.css` stylesheet to apply the styles to every route in your application:

```tsx
// These styles apply to every route in the application
import './global.css'

export default function RootLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return (
    <html lang="en">
      <body>{children}</body>
    </html>
  )
}
```

```jsx
// These styles apply to every route in the application
import './global.css'

export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <body>{children}</body>
    </html>
  )
}
```

To add a stylesheet to your application, import the CSS file within `pages/_app.js`.

For example, consider the following stylesheet named `styles.css`:

```css
body {
  font-family: 'SF Pro Text', 'SF Pro Icons', 'Helvetica Neue', 'Helvetica',
    'Arial', sans-serif;
  padding: 20px 20px 60px;
  max-width: 680px;
  margin: 0 auto;
}
```

Create a `pages/_app.js` file if not already present. Then, [`import`](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/import) the `styles.css` file.

```jsx
import '../styles.css'

// This default export is required in a new `pages/_app.js` file.
export default function MyApp({ Component, pageProps }) {
  return <Component {...pageProps} />
}
```

These styles (`styles.css`) will apply to all pages and components in your application. Due to the global nature of stylesheets, and to avoid conflicts, you may **only import them inside `pages/_app.js`**.

In development, expressing stylesheets this way allows your styles to be hot reloaded as you edit them—meaning you can keep application state.

In production, all CSS files will be automatically concatenated into a single minified `.css` file. The order that the CSS is concatenated will match the order the CSS is imported into the `_app.js` file. Pay special attention to imported JS modules that include their own CSS; the JS module's CSS will be concatenated following the same ordering rules as imported CSS files. For example:

```jsx
import '../styles.css'
// The CSS in ErrorBoundary depends on the global CSS in styles.css,
// so we import it after styles.css.
import ErrorBoundary from '../components/ErrorBoundary'

export default function MyApp({ Component, pageProps }) {
  return (
    <ErrorBoundary>
      <Component {...pageProps} />
    </ErrorBoundary>
  )
}
```

### External Stylesheets

Stylesheets published by external packages can be imported anywhere in the `app` directory, including colocated components:

```tsx
import 'bootstrap/dist/css/bootstrap.css'

export default function RootLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return (
    <html lang="en">
      <body className="container">{children}</body>
    </html>
  )
}
```

```jsx
import 'bootstrap/dist/css/bootstrap.css'

export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <body className="container">{children}</body>
    </html>
  )
}
```

> **Good to know**: External stylesheets must be directly imported from an npm package or downloaded and colocated with your codebase. You cannot use `<link rel="stylesheet" />`.

Next.js allows you to import CSS files from a JavaScript file. This is possible because Next.js extends the concept of [`import`](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/import) beyond JavaScript.

#### Import styles from `node_modules`

Since Next.js **9.5.4**, importing a CSS file from `node_modules` is permitted anywhere in your application.

For global stylesheets, like `bootstrap` or `nprogress`, you should import the file inside `pages/_app.js`. For example:

```jsx
import 'bootstrap/dist/css/bootstrap.css'

export default function MyApp({ Component, pageProps }) {
  return <Component {...pageProps} />
}
```

For importing CSS required by a third-party component, you can do so in your component. For example:

```jsx
import { useState } from 'react'
import { Dialog } from '@reach/dialog'
import VisuallyHidden from '@reach/visually-hidden'
import '@reach/dialog/styles.css'

function ExampleDialog(props) {
  const [showDialog, setShowDialog] = useState(false)
  const open = () => setShowDialog(true)
  const close = () => setShowDialog(false)

  return (
    <div>
      <button onClick={open}>Open Dialog</button>
      <Dialog isOpen={showDialog} onDismiss={close}>
        <button className="close-button" onClick={close}>
          <VisuallyHidden>Close</VisuallyHidden>
          <span aria-hidden>×</span>
        </button>
        <p>Hello there. I am a dialog</p>
      </Dialog>
    </div>
  )
}
```

### Ordering and Merging

Next.js optimizes CSS during production builds by automatically chunking (merging) stylesheets. The CSS order is _determined by the order in which you import the stylesheets into your application code_.

For example, `base-button.module.css` will be ordered before `page.module.css` since `<BaseButton>` is imported first in `<Page>`:

```tsx
import styles from './base-button.module.css'

export function BaseButton() {
  return <button className={styles.primary} />
}
```

```jsx
import styles from './base-button.module.css'

export function BaseButton() {
  return <button className={styles.primary} />
}
```

```tsx
import { BaseButton } from './base-button'
import styles from './page.module.css'

export default function Page() {
  return <BaseButton className={styles.primary} />
}
```

```jsx
import { BaseButton } from './base-button'
import styles from './page.module.css'

export default function Page() {
  return <BaseButton className={styles.primary} />
}
```

To maintain a predictable order, we recommend the following:

* Only import a CSS file in a single JS/TS file.
  * If using global class names, import the global styles in the same file in the order you want them to be applied.
* Prefer CSS Modules over global styles.
  * Use a consistent naming convention for your CSS modules. For example, using `<name>.module.css` over `<name>.tsx`.
* Extract shared styles into a separate shared component.
* If using Tailwind, import the stylesheet at the top of the file, preferably in the Root Layout.
* Turn off any linters/formatters (e.g., ESLint's [`sort-import`](https://eslint.org/docs/latest/rules/sort-imports)) that automatically sort your imports. This can inadvertently affect your CSS since CSS import order _matters_.

> **Good to know:**
>
> * CSS ordering can behave differently in development mode, always ensure to check the build (`next build`) to verify the final CSS order.
> * You can use the `cssChunking` option in `next.config.js` to control how CSS is chunked.

### Additional Features

Next.js includes additional features to improve the authoring experience of adding styles:

* When running locally with `next dev`, local stylesheets (either global or CSS modules) will take advantage of Fast Refresh to instantly reflect changes as edits are saved.
* When building for production with `next build`, CSS files will be bundled into fewer minified `.css` files to reduce the number of network requests needed to retrieve styles.
* If you disable JavaScript, styles will still be loaded in the production build (`next start`). However, JavaScript is still required for `next dev` to enable Fast Refresh.
