# Browser Caching

## HTML Markup

* Serve these with a `Cache-Control: no-cache` header. This will instruct the browser to cache locally but only after checking with the server that the content hasn’t changed. Note that `no-cache` does NOT mean "don’t cache", rather it tells the browser to always revalidate when the resource is requested. `no-store` tells the browser not to cache at all, which isn’t usually desirable.

## CSS, JS and Images

* Set a long `max-age` eg: `Cache-Control: max-age: 31536000` (one year). Content on these URLs should typically not change so it should be safe to cache them for really long periods.
* Use a [cache-busting](https://www.keycdn.com/support/what-is-cache-busting) mechanism for versioning assets to ensure that the browser caches each version as a different URL. Example: `sncss-29d48c7.css` where “_29d48c7_” is an auto-generated number unique to every version of the file.

## General

* If it is under your control, ensure the server provides a validation token (`ETag`) header. The `ETag` header is an additional identifier for a specific version of a resource. It is especially useful to prevent simultaneous updates overwriting each other. If you use a CDN, it is likely this header will already be provided. Learn more:
    *  [MDN ETag](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/ETag)
    * [Express options for 'ETag' setting](https://expressjs.com/en/api.html#etag.options.table)

It’s important to note that there isn’t a one-size-fits-all approach to caching, so always decide a caching strategy based on your needs.

## Further resources

* [Web Fundamentals: HTTP Caching](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching)
