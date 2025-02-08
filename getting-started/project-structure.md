---
description: >-
  An overview of the folder and file conventions in Next.js, and how to organize
  your project.
---

# Project structure

## Project structure and organization

This page provides an overview of the folder and file conventions in Next.js, as well as tips for organizing your project.

### Folder and file conventions

#### Top-level folders

Top-level folders are used to organize your application's code and static assets.

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

|          |                                    |
| -------- | ---------------------------------- |
| `app`    | App Router                         |
| `pages`  | Pages Router                       |
| `public` | Static assets to be served         |
| `src`    | Optional application source folder |

#### Top-level files

Top-level files are used to configure your application, manage dependencies, run middleware, integrate monitoring tools, and define environment variables.

|                      |                                         |
| -------------------- | --------------------------------------- |
| **Next.js**          |                                         |
| `next.config.js`     | Configuration file for Next.js          |
| `package.json`       | Project dependencies and scripts        |
| `instrumentation.ts` | OpenTelemetry and Instrumentation file  |
| `middleware.ts`      | Next.js request middleware              |
| `.env`               | Environment variables                   |
| `.env.local`         | Local environment variables             |
| `.env.production`    | Production environment variables        |
| `.env.development`   | Development environment variables       |
| `.eslintrc.json`     | Configuration file for ESLint           |
| `.gitignore`         | Git files and folders to ignore         |
| `next-env.d.ts`      | TypeScript declaration file for Next.js |
| `tsconfig.json`      | Configuration file for TypeScript       |
| `jsconfig.json`      | Configuration file for JavaScript       |

#### Routing Files

|                |                     |                              |
| -------------- | ------------------- | ---------------------------- |
| `layout`       | `.js` `.jsx` `.tsx` | Layout                       |
| `page`         | `.js` `.jsx` `.tsx` | Page                         |
| `loading`      | `.js` `.jsx` `.tsx` | Loading UI                   |
| `not-found`    | `.js` `.jsx` `.tsx` | Not found UI                 |
| `error`        | `.js` `.jsx` `.tsx` | Error UI                     |
| `global-error` | `.js` `.jsx` `.tsx` | Global error UI              |
| `route`        | `.js` `.ts`         | API endpoint                 |
| `template`     | `.js` `.jsx` `.tsx` | Re-rendered layout           |
| `default`      | `.js` `.jsx` `.tsx` | Parallel route fallback page |

#### Nested routes

|                 |                      |
| --------------- | -------------------- |
| `folder`        | Route segment        |
| `folder/folder` | Nested route segment |

#### Dynamic routes

|                 |                                  |
| --------------- | -------------------------------- |
| `[folder]`      | Dynamic route segment            |
| `[...folder]`   | Catch-all route segment          |
| `[[...folder]]` | Optional catch-all route segment |

#### Route Groups and private folders

|            |                                                  |
| ---------- | ------------------------------------------------ |
| `(folder)` | Group routes without affecting routing           |
| `_folder`  | Opt folder and all child segments out of routing |

#### Parallel and Intercepted Routes

|                  |                            |
| ---------------- | -------------------------- |
| `@folder`        | Named slot                 |
| `(.)folder`      | Intercept same level       |
| `(..)folder`     | Intercept one level above  |
| `(..)(..)folder` | Intercept two levels above |
| `(...)folder`    | Intercept from root        |

#### Metadata file conventions

**App icons**

|              |                                     |                          |
| ------------ | ----------------------------------- | ------------------------ |
| `favicon`    | `.ico`                              | Favicon file             |
| `icon`       | `.ico` `.jpg` `.jpeg` `.png` `.svg` | App Icon file            |
| `icon`       | `.js` `.ts` `.tsx`                  | Generated App Icon       |
| `apple-icon` | `.jpg` `.jpeg`, `.png`              | Apple App Icon file      |
| `apple-icon` | `.js` `.ts` `.tsx`                  | Generated Apple App Icon |

**Open Graph and Twitter images**

|                   |                              |                            |
| ----------------- | ---------------------------- | -------------------------- |
| `opengraph-image` | `.jpg` `.jpeg` `.png` `.gif` | Open Graph image file      |
| `opengraph-image` | `.js` `.ts` `.tsx`           | Generated Open Graph image |
| `twitter-image`   | `.jpg` `.jpeg` `.png` `.gif` | Twitter image file         |
| `twitter-image`   | `.js` `.ts` `.tsx`           | Generated Twitter image    |

**SEO**

|           |             |                       |
| --------- | ----------- | --------------------- |
| `sitemap` | `.xml`      | Sitemap file          |
| `sitemap` | `.js` `.ts` | Generated Sitemap     |
| `robots`  | `.txt`      | Robots file           |
| `robots`  | `.js` `.ts` | Generated Robots file |

#### Files conventions

|             |                     |                   |
| ----------- | ------------------- | ----------------- |
| `_app`      | `.js` `.jsx` `.tsx` | Custom App        |
| `_document` | `.js` `.jsx` `.tsx` | Custom Document   |
| `_error`    | `.js` `.jsx` `.tsx` | Custom Error Page |
| `404`       | `.js` `.jsx` `.tsx` | 404 Error Page    |
| `500`       | `.js` `.jsx` `.tsx` | 500 Error Page    |

#### Routes

|                       |                     |             |
| --------------------- | ------------------- | ----------- |
| **Folder convention** |                     |             |
| `index`               | `.js` `.jsx` `.tsx` | Home page   |
| `folder/index`        | `.js` `.jsx` `.tsx` | Nested page |
| **File convention**   |                     |             |
| `index`               | `.js` `.jsx` `.tsx` | Home page   |
| `file`                | `.js` `.jsx` `.tsx` | Nested page |

#### Dynamic routes

|                       |                     |                                  |
| --------------------- | ------------------- | -------------------------------- |
| **Folder convention** |                     |                                  |
| `[folder]/index`      | `.js` `.jsx` `.tsx` | Dynamic route segment            |
| `[...folder]/index`   | `.js` `.jsx` `.tsx` | Catch-all route segment          |
| `[[...folder]]/index` | `.js` `.jsx` `.tsx` | Optional catch-all route segment |
| **File convention**   |                     |                                  |
| `[file]`              | `.js` `.jsx` `.tsx` | Dynamic route segment            |
| `[...file]`           | `.js` `.jsx` `.tsx` | Catch-all route segment          |
| `[[...file]]`         | `.js` `.jsx` `.tsx` | Optional catch-all route segment |

### Component hierarchy

The React components defined in special files of a route segment are rendered in a specific hierarchy:

* `layout.js`
* `template.js`
* `error.js` (React error boundary)
* `loading.js` (React suspense boundary)
* `not-found.js` (React error boundary)
* `page.js` or nested `layout.js`

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

In a nested route, the components of a segment will be nested **inside** the components of its parent segment.

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

### Organizing your project

Apart from folder and file conventions, Next.js is **unopinionated** about how you organize and colocate your project files. But it does provide several features to help you organize your project.

#### Colocation

In the `app` directory, nested folders define route structure. Each folder represents a route segment that is mapped to a corresponding segment in a URL path.

However, even though route structure is defined through folders, a route is **not publicly accessible** until a `page.js` or `route.js` file is added to a route segment.

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

And, even when a route is made publicly accessible, only the **content returned** by `page.js` or `route.js` is sent to the client.

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

This means that **project files** can be **safely colocated** inside route segments in the `app` directory without accidentally being routable.

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

> **Good to know**:
>
> * While you **can** colocate your project files in `app` you don't **have** to. If you prefer, you can keep them outside the `app` directory.

#### Private folders

Private folders can be created by prefixing a folder with an underscore: `_folderName`

This indicates the folder is a private implementation detail and should not be considered by the routing system, thereby **opting the folder and all its subfolders** out of routing.

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

Since files in the `app` directory can be safely colocated by default, private folders are not required for colocation. However, they can be useful for:

* Separating UI logic from routing logic.
* Consistently organizing internal files across a project and the Next.js ecosystem.
* Sorting and grouping files in code editors.
* Avoiding potential naming conflicts with future Next.js file conventions.

> **Good to know**:
>
> * While not a framework convention, you might also consider marking files outside private folders as "private" using the same underscore pattern.
> * You can create URL segments that start with an underscore by prefixing the folder name with `%5F` (the URL-encoded form of an underscore): `%5FfolderName`.
> * If you don't use private folders, it would be helpful to know Next.js special file conventions to prevent unexpected naming conflicts.

#### Route groups

Route groups can be created by wrapping a folder in parenthesis: `(folderName)`

This indicates the folder is for organizational purposes and should **not be included** in the route's URL path.

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

Route groups are useful for:

* Organizing routes into groups e.g. by site section, intent, or team.
* Enabling nested layouts in the same route segment level:
  * Creating multiple nested layouts in the same segment, including multiple root layouts
  * Adding a layout to a subset of routes in a common segment

#### `src` directory

Next.js supports storing application code (including `app`) inside an optional `src` directory. This separates application code from project configuration files which mostly live in the root of a project.

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

#### Common strategies

The following section lists a very high-level overview of common strategies. The simplest takeaway is to choose a strategy that works for you and your team and be consistent across the project.

> **Good to know**: In our examples below, we're using `components` and `lib` folders as generalized placeholders, their naming has no special framework significance and your projects might use other folders like `ui`, `utils`, `hooks`, `styles`, etc.

**Store project files outside of `app`**

This strategy stores all application code in shared folders in the **root of your project** and keeps the `app` directory purely for routing purposes.

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

**Store project files in top-level folders inside of `app`**

This strategy stores all application code in shared folders in the **root of the `app` directory**.

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

**Split project files by feature or route**

This strategy stores globally shared application code in the root `app` directory and **splits** more specific application code into the route segments that use them.

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>
