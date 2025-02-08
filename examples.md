---
description: Learn how to implement common UI patterns and use cases using Next.js
---

# Examples

#### Data Fetching

* [Using the fetch API](building-your-application/data-fetching/data-fetching-and-caching.md#fetching-data-on-the-server-with-the-fetch-api)
* [Using an ORM or database client](building-your-application/data-fetching/data-fetching-and-caching.md#fetching-data-on-the-server-with-an-orm-or-database)
* [Reading search params on the server](api-reference/file-conventions/page.js.md)
* [Reading search params on the client](api-reference/functions/usesearchparams.md)

#### Revalidating Data

* [Using ISR to revalidate data after a certain time](building-your-application/data-fetching/incremental-static-regeneration-isr.md#time-based-revalidation)
* [Using ISR to revalidate data on-demand](building-your-application/data-fetching/incremental-static-regeneration-isr.md#on-demand-revalidation-with-revalidatepath)

#### Forms

* [Showing a pending state while submitting a form](building-your-application/data-fetching/server-actions-and-mutations.md#pending-states)
* [Server-side form validation](building-your-application/data-fetching/server-actions-and-mutations.md#server-side-form-validation)
* [Handling expected errors](building-your-application/routing/error-handling.md#handling-expected-errors-from-server-actions)
* [Handling unexpected exceptions](building-your-application/routing/error-handling.md#uncaught-exceptions)
* [Showing optimistic UI updates](building-your-application/data-fetching/server-actions-and-mutations.md#optimistic-updates)
* [Programmatic form submission](building-your-application/data-fetching/server-actions-and-mutations.md#programmatic-form-submission)

#### Server Actions

* [Passing additional values](building-your-application/data-fetching/server-actions-and-mutations.md#passing-additional-arguments)
* [Revalidating data](building-your-application/data-fetching/server-actions-and-mutations.md#revalidating-data)
* [Redirecting](building-your-application/data-fetching/server-actions-and-mutations.md#redirecting)
* [Setting cookies](api-reference/functions/cookies.md#setting-a-cookie)
* [Deleting cookies](api-reference/functions/cookies.md#deleting-cookies)

#### Metadata

* [Creating an RSS feed](building-your-application/routing/route-handlers.md#non-ui-responses)
* [Creating an Open Graph image](api-reference/file-conventions/metadata-files/opengraph-image-and-twitter-image.md)
* [Creating a sitemap](api-reference/file-conventions/metadata-files/sitemap.xml.md)
* [Creating a robots.txt file](api-reference/file-conventions/metadata-files/robots.txt.md)
* [Creating a custom 404 page](api-reference/file-conventions/not-found.js.md)
* [Creating a custom 500 page](api-reference/file-conventions/error.js.md)

#### Auth

* [Creating a sign-up form](building-your-application/authentication.md#sign-up-and-login-functionality)
* [Stateless, cookie-based session management](building-your-application/authentication.md#stateless-sessions)
* [Stateful, database-backed session management](building-your-application/authentication.md#database-sessions)
* [Managing authorization](building-your-application/authentication.md)

#### Testing

* [Vitest](building-your-application/testing/setting-up-vitest-with-next.js.md)
* [Jest](building-your-application/testing/jest.md)
* [Playwright](building-your-application/testing/playwright.md)
* [Cypress](building-your-application/testing/cypress.md)

#### Deployment

* [Creating a Dockerfile](building-your-application/deploying/#docker-image)
* [Creating a static export (SPA)](building-your-application/deploying/static-exports.md)
* [Configuring caching when self-hosting](building-your-application/deploying/#caching-and-isr)
* [Configuring Image Optimization when self-hosting](building-your-application/deploying/#image-optimization)
