---
description: >-
  Optimize the performance of third-party libraries in your application with the
  `@next/third-parties` package.
---

# Third Party Libraries

**`@next/third-parties`** is a library that provides a collection of components and utilities that improve the performance and developer experience of loading popular third-party libraries in your Next.js application.

All third-party integrations provided by `@next/third-parties` have been optimized for performance and ease of use.

### Getting Started

To get started, install the `@next/third-parties` library:

```bash
npm install @next/third-parties@latest next@latest
```

`@next/third-parties` is currently an **experimental** library under active development. We recommend installing it with the **latest** or **canary** flags while we work on adding more third-party integrations.

### Google Third-Parties

All supported third-party libraries from Google can be imported from `@next/third-parties/google`.

#### Google Tag Manager

The `GoogleTagManager` component can be used to instantiate a [Google Tag Manager](https://developers.google.com/tag-platform/tag-manager) container to your page. By default, it fetches the original inline script after hydration occurs on the page.

To load Google Tag Manager for all routes, include the component directly in your root layout and pass in your GTM container ID:

```tsx
import { GoogleTagManager } from '@next/third-parties/google'

export default function RootLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return (
    <html lang="en">
      <GoogleTagManager gtmId="GTM-XYZ" />
      <body>{children}</body>
    </html>
  )
}
```

```jsx
import { GoogleTagManager } from '@next/third-parties/google'

export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <GoogleTagManager gtmId="GTM-XYZ" />
      <body>{children}</body>
    </html>
  )
}
```

To load Google Tag Manager for all routes, include the component directly in your custom `_app` and pass in your GTM container ID:

```jsx
import { GoogleTagManager } from '@next/third-parties/google'

export default function MyApp({ Component, pageProps }) {
  return (
    <>
      <Component {...pageProps} />
      <GoogleTagManager gtmId="GTM-XYZ" />
    </>
  )
}
```

To load Google Tag Manager for a single route, include the component in your page file:

```jsx
import { GoogleTagManager } from '@next/third-parties/google'

export default function Page() {
  return <GoogleTagManager gtmId="GTM-XYZ" />
}
```

```jsx
import { GoogleTagManager } from '@next/third-parties/google'

export default function Page() {
  return <GoogleTagManager gtmId="GTM-XYZ" />
}
```

**Sending Events**

The `sendGTMEvent` function can be used to track user interactions on your page by sending events using the `dataLayer` object. For this function to work, the `<GoogleTagManager />` component must be included in either a parent layout, page, or component, or directly in the same file.

```jsx
'use client'

import { sendGTMEvent } from '@next/third-parties/google'

export function EventButton() {
  return (
    <div>
      <button
        onClick={() => sendGTMEvent({ event: 'buttonClicked', value: 'xyz' })}
      >
        Send Event
      </button>
    </div>
  )
}
```

```jsx
import { sendGTMEvent } from '@next/third-parties/google'

export function EventButton() {
  return (
    <div>
      <button
        onClick={() => sendGTMEvent({ event: 'buttonClicked', value: 'xyz' })}
      >
        Send Event
      </button>
    </div>
  )
}
```

Refer to the Tag Manager [developer documentation](https://developers.google.com/tag-platform/tag-manager/datalayer) to learn about the different variables and events that can be passed into the function.

**Server-side Tagging**

If you're using a server-side tag manager and serving `gtm.js` scripts from your tagging server you can use `gtmScriptUrl` option to specify the URL of the script.

**Options**

Options to pass to the Google Tag Manager. For a full list of options, read the [Google Tag Manager docs](https://developers.google.com/tag-platform/tag-manager/datalayer).

<table><thead><tr><th width="191">Name</th><th width="106">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>gtmId</code></td><td>Required</td><td>Your GTM container ID. Usually starts with <code>GTM-</code>.</td></tr><tr><td><code>gtmScriptUrl</code></td><td>Optional</td><td>GTM script URL. Defaults to <code>https://www.googletagmanager.com/gtm.js</code>.</td></tr><tr><td><code>dataLayer</code></td><td>Optional</td><td>Data layer object to instantiate the container with.</td></tr><tr><td><code>dataLayerName</code></td><td>Optional</td><td>Name of the data layer. Defaults to <code>dataLayer</code>.</td></tr><tr><td><code>auth</code></td><td>Optional</td><td>Value of authentication parameter (<code>gtm_auth</code>) for environment snippets.</td></tr><tr><td><code>preview</code></td><td>Optional</td><td>Value of preview parameter (<code>gtm_preview</code>) for environment snippets.</td></tr></tbody></table>

#### Google Analytics

The `GoogleAnalytics` component can be used to include [Google Analytics 4](https://developers.google.com/analytics/devguides/collection/ga4) to your page via the Google tag (`gtag.js`). By default, it fetches the original scripts after hydration occurs on the page.

> **Recommendation**: If Google Tag Manager is already included in your application, you can configure Google Analytics directly using it, rather than including Google Analytics as a separate component. Refer to the [documentation](https://developers.google.com/analytics/devguides/collection/ga4/tag-options#what-is-gtm) to learn more about the differences between Tag Manager and `gtag.js`.

To load Google Analytics for all routes, include the component directly in your root layout and pass in your measurement ID:

```tsx
import { GoogleAnalytics } from '@next/third-parties/google'

export default function RootLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return (
    <html lang="en">
      <body>{children}</body>
      <GoogleAnalytics gaId="G-XYZ" />
    </html>
  )
}
```

```jsx
import { GoogleAnalytics } from '@next/third-parties/google'

export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <body>{children}</body>
      <GoogleAnalytics gaId="G-XYZ" />
    </html>
  )
}
```

To load Google Analytics for all routes, include the component directly in your custom `_app` and pass in your measurement ID:

```jsx
import { GoogleAnalytics } from '@next/third-parties/google'

export default function MyApp({ Component, pageProps }) {
  return (
    <>
      <Component {...pageProps} />
      <GoogleAnalytics gaId="G-XYZ" />
    </>
  )
}
```

To load Google Analytics for a single route, include the component in your page file:

```jsx
import { GoogleAnalytics } from '@next/third-parties/google'

export default function Page() {
  return <GoogleAnalytics gaId="G-XYZ" />
}
```

```jsx
import { GoogleAnalytics } from '@next/third-parties/google'

export default function Page() {
  return <GoogleAnalytics gaId="G-XYZ" />
}
```

**Sending Events**

The `sendGAEvent` function can be used to measure user interactions on your page by sending events using the `dataLayer` object. For this function to work, the `<GoogleAnalytics />` component must be included in either a parent layout, page, or component, or directly in the same file.

```jsx
'use client'

import { sendGAEvent } from '@next/third-parties/google'

export function EventButton() {
  return (
    <div>
      <button
        onClick={() => sendGAEvent('event', 'buttonClicked', { value: 'xyz' })}
      >
        Send Event
      </button>
    </div>
  )
}
```

```jsx
import { sendGAEvent } from '@next/third-parties/google'

export function EventButton() {
  return (
    <div>
      <button
        onClick={() => sendGAEvent('event', 'buttonClicked', { value: 'xyz' })}
      >
        Send Event
      </button>
    </div>
  )
}
```

Refer to the Google Analytics [developer documentation](https://developers.google.com/analytics/devguides/collection/ga4/event-parameters) to learn more about event parameters.

**Tracking Pageviews**

Google Analytics automatically tracks pageviews when the browser history state changes. This means that client-side navigations between Next.js routes will send pageview data without any configuration.

To ensure that client-side navigations are being measured correctly, verify that the [_“Enhanced Measurement”_](https://support.google.com/analytics/answer/9216061#enable_disable) property is enabled in your Admin panel and the _“Page changes based on browser history events”_ checkbox is selected.

> **Note**: If you decide to manually send pageview events, make sure to disable the default pageview measurement to avoid having duplicate data. Refer to the Google Analytics [developer documentation](https://developers.google.com/analytics/devguides/collection/ga4/views?client_type=gtag#manual_pageviews) to learn more.

**Options**

Options to pass to the `<GoogleAnalytics>` component.

<table><thead><tr><th width="196">Name</th><th width="113">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>gaId</code></td><td>Required</td><td>Your <a href="https://support.google.com/analytics/answer/12270356">measurement ID</a>. Usually starts with <code>G-</code>.</td></tr><tr><td><code>dataLayerName</code></td><td>Optional</td><td>Name of the data layer. Defaults to <code>dataLayer</code>.</td></tr><tr><td><code>nonce</code></td><td>Optional</td><td>A nonce.</td></tr></tbody></table>

#### Google Maps Embed

The `GoogleMapsEmbed` component can be used to add a [Google Maps Embed](https://developers.google.com/maps/documentation/embed/embedding-map) to your page. By default, it uses the `loading` attribute to lazy-load the embed below the fold.

{% tabs %}
{% tab title="TS" %}
```jsx
import { GoogleMapsEmbed } from '@next/third-parties/google'

export default function Page() {
  return (
    <GoogleMapsEmbed
      apiKey="XYZ"
      height={200}
      width="100%"
      mode="place"
      q="Brooklyn+Bridge,New+York,NY"
    />
  )
}
```
{% endtab %}

{% tab title="JS" %}
```jsx
import { GoogleMapsEmbed } from '@next/third-parties/google'

export default function Page() {
  return (
    <GoogleMapsEmbed
      apiKey="XYZ"
      height={200}
      width="100%"
      mode="place"
      q="Brooklyn+Bridge,New+York,NY"
    />
  )
}
```
{% endtab %}
{% endtabs %}

**Options**

Options to pass to the Google Maps Embed. For a full list of options, read the [Google Map Embed docs](https://developers.google.com/maps/documentation/embed/embedding-map).

<table><thead><tr><th width="205">Name</th><th width="106">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>apiKey</code></td><td>Required</td><td>Your api key.</td></tr><tr><td><code>mode</code></td><td>Required</td><td><a href="https://developers.google.com/maps/documentation/embed/embedding-map#choosing_map_modes">Map mode</a></td></tr><tr><td><code>height</code></td><td>Optional</td><td>Height of the embed. Defaults to <code>auto</code>.</td></tr><tr><td><code>width</code></td><td>Optional</td><td>Width of the embed. Defaults to <code>auto</code>.</td></tr><tr><td><code>style</code></td><td>Optional</td><td>Pass styles to the iframe.</td></tr><tr><td><code>allowfullscreen</code></td><td>Optional</td><td>Property to allow certain map parts to go full screen.</td></tr><tr><td><code>loading</code></td><td>Optional</td><td>Defaults to lazy. Consider changing if you know your embed will be above the fold.</td></tr><tr><td><code>q</code></td><td>Optional</td><td>Defines map marker location. <em>This may be required depending on the map mode</em>.</td></tr><tr><td><code>center</code></td><td>Optional</td><td>Defines the center of the map view.</td></tr><tr><td><code>zoom</code></td><td>Optional</td><td>Sets initial zoom level of the map.</td></tr><tr><td><code>maptype</code></td><td>Optional</td><td>Defines type of map tiles to load.</td></tr><tr><td><code>language</code></td><td>Optional</td><td>Defines the language to use for UI elements and for the display of labels on map tiles.</td></tr><tr><td><code>region</code></td><td>Optional</td><td>Defines the appropriate borders and labels to display, based on geo-political sensitivities.</td></tr></tbody></table>

#### YouTube Embed

The `YouTubeEmbed` component can be used to load and display a YouTube embed. This component loads faster by using [`lite-youtube-embed`](https://github.com/paulirish/lite-youtube-embed) under the hood.

{% tabs %}
{% tab title="TS" %}
```jsx
import { YouTubeEmbed } from '@next/third-parties/google'

export default function Page() {
  return <YouTubeEmbed videoid="ogfYd705cRs" height={400} params="controls=0" />
}
```
{% endtab %}

{% tab title="JS" %}
```jsx
import { YouTubeEmbed } from '@next/third-parties/google'

export default function Page() {
  return <YouTubeEmbed videoid="ogfYd705cRs" height={400} params="controls=0" />
}
```
{% endtab %}
{% endtabs %}

**Options**

<table><thead><tr><th width="159">Name</th><th width="139">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>videoid</code></td><td>Required</td><td>YouTube video id.</td></tr><tr><td><code>width</code></td><td>Optional</td><td>Width of the video container. Defaults to <code>auto</code></td></tr><tr><td><code>height</code></td><td>Optional</td><td>Height of the video container. Defaults to <code>auto</code></td></tr><tr><td><code>playlabel</code></td><td>Optional</td><td>A visually hidden label for the play button for accessibility.</td></tr><tr><td><code>params</code></td><td>Optional</td><td>The video player params defined <a href="https://developers.google.com/youtube/player_parameters#Parameters">here</a>.<br>Params are passed as a query param string.<br>Eg: <code>params="controls=0&#x26;start=10&#x26;end=30"</code></td></tr><tr><td><code>style</code></td><td>Optional</td><td>Used to apply styles to the video container.</td></tr></tbody></table>
