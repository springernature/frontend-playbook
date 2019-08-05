# A simple performance checklist

Web performance is an important consideration in everything that we build, from the early design stages, until a product has reached end-of-life.

This checklist aims to help you and your team create performant products.

Remember that, for most of these rules, there's always the chance that following them may impact performance in a negative way. Always use [any of the tools below](#tooling) to run before/after comparisons.

## HTTP Requests

A lower number of requests is directly related to better performance and higher user engagement. Make sure that the [number of HTTP requests is as small as possible](https://learning.oreilly.com/library/view/high-performance-web/9780596529307/ch03.html) by:

* Ensuring that there are [no redirects](https://learning.oreilly.com/library/view/high-performance-web/9780596529307/ch13.html) on the page itself or in any of the first party resources.
* Concatenating first party CSS and JS, when suitable. This is true even when using HTTP2.
* Ensuring that no first party resources are returning HTTP 4xx or 5xx errors.
* Serve first party resources from as few different domains as possible in order to [reduce DNS lookups](https://www.oreilly.com/library/view/high-performance-web/9780596529307/ch11.html).

## Page weight

Another important factor that impacts user engagement is [the size of the resources](https://blog.chriszacharias.com/page-weight-matters). On low performing networks or devices, the size of the resources being loaded can delay the loading of the page by several seconds and increase power consumption significantly.

* Ensure that all text resources over 1500 bytes [are minified](https://learning.oreilly.com/library/view/high-performance-web/9780596529307/ch12.html).
* Ensure that all text resources over 1500 bytes use Brotli, Zopfli or [GZip compression](https://learning.oreilly.com/library/view/high-performance-web/9780596529307/ch06.html).
* [Choose the right format for images, and optimise images and SVGs](images.md).
* Set an [appropriate expiry date or a maximum age](https://learning.oreilly.com/library/view/high-performance-web/9780596529307/ch05.html) for all static resources.
* For resources that change rarely, consider [fingerprinting them](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching) and setting a expiry date [far in the future](https://developers.google.com/web/tools/lighthouse/audits/cache-policy).

## Render blocking resources

CSS and JS resources can be [render blocking](https://developers.google.com/web/tools/lighthouse/audits/blocking-resources) as the browser will pause rendering of a page while a CSS file or a synchronous JS file or script are being loaded. On slow connections this can delay the page load by several seconds. Ensure there are as few render blocking resources as possible by:

* Ensure all JavaScript files use [`async` or, when possible, `defer` attributes](https://www.growingwiththeweb.com/2014/02/async-vs-defer-attributes.html).
* Ensure that only the smallest amount of CSS needed to render the page is being loaded synchronously. [Load the rest of the CSS asynchronously](https://www.filamentgroup.com/lab/load-css-simpler/).

## The critical rendering path

The [critical rendering path](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/analyzing-crp) is made up by the resources that are required in order for the browser to complete rendering the current view. By optimizing the critical rendering path you can improve the time to first render of our pages.

* Study the waterfall and find out which resources are in the critical path. Make them load earlier by using [`rel="dns-prefetch"` and `rel="preconnect"`](https://www.keycdn.com/blog/resource-hints) resource hints as appropriate. Ensure that resources [like CSS](https://web.dev/defer-non-critical-css/)that are _not_ in the critical path are loaded asynchronously or lazy-loaded when possible.

## Post launch

* Add the site to [SpeedCurve](https://speedcurve.com) for continuous performance monitoring and alerting. Contact the Frontend Enablement team if you need access to this tool.

## Tooling

The following tools can be used to run performance tests on one or more pages:

* [Lighthouse](https://developers.google.com/web/tools/lighthouse/): A Google tool that audits pages for performance, accessibility, and others. Available as part of [Chrome's devtools](https://developers.google.com/web/tools/lighthouse/#devtools).
* [WebPagetest](https://www.webpagetest.org/): The standard tool for synthetic web performance testing.
* Private WebPage test instance: coming soon.
* [Speedcurve](https://speedcurve.com/): A tool that automates running tests on WebPagetest and provides graphs, trends, and alerts.

## Further resources

* [MDN web docs: Web performance](https://developer.mozilla.org/en-US/docs/Learn/Performance)
