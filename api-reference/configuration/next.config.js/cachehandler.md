---
description: >-
  Configure the Next.js cache used for storing and revalidating data to use any
  external service like Redis, Memcached, or others.
---

# cacheHandler

## Custom Next.js Cache Handler

Caching and revalidating pages (with Incremental Static Regeneration) use the same shared cache. When [deploying to Vercel](https://vercel.com/docs/incremental-static-regeneration?utm_source=next-site\&utm_medium=docs\&utm_campaign=next-website), the ISR cache is automatically persisted to durable storage.

When self-hosting, the ISR cache is stored to the filesystem (on disk) on your Next.js server. This works automatically when self-hosting using both the Pages and App Router.

You can configure the Next.js cache location if you want to persist cached pages and data to durable storage, or share the cache across multiple containers or instances of your Next.js application.

```js
module.exports = {
  cacheHandler: require.resolve('./cache-handler.js'),
  cacheMaxMemorySize: 0, // disable default in-memory caching
}
```

View an example of a custom cache handler and learn more about implementation.

### API Reference

The cache handler can implement the following methods: `get`, `set`, and `revalidateTag`.

#### `get()`

| Parameter | Type     | Description                  |
| --------- | -------- | ---------------------------- |
| `key`     | `string` | The key to the cached value. |

Returns the cached value or `null` if not found.

#### `set()`

| Parameter | Type           | Description                      |
| --------- | -------------- | -------------------------------- |
| `key`     | `string`       | The key to store the data under. |
| `data`    | Data or `null` | The data to be cached.           |
| `ctx`     | `{ tags: [] }` | The cache tags provided.         |

Returns `Promise<void>`.

#### `revalidateTag()`

| Parameter | Type                   | Description                   |
| --------- | ---------------------- | ----------------------------- |
| `tag`     | `string` or `string[]` | The cache tags to revalidate. |

Returns `Promise<void>`. Learn more about revalidating data or the `revalidateTag()` function.

**Good to know:**

* `revalidatePath` is a convenience layer on top of cache tags. Calling `revalidatePath` will call your `revalidateTag` function, which you can then choose if you want to tag cache keys based on the path.

### Version History

| Version   | Changes                                                      |
| --------- | ------------------------------------------------------------ |
| `v14.1.0` | Renamed to `cacheHandler` and became stable.                 |
| `v13.4.0` | `incrementalCacheHandlerPath` support for `revalidateTag`.   |
| `v13.4.0` | `incrementalCacheHandlerPath` support for standalone output. |
| `v12.2.0` | Experimental `incrementalCacheHandlerPath` added.            |
