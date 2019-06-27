# Managing static assets

By **static assets** we mean webfonts, JavaScript libraries (like jQuery or Mathjax), and any other files that get loaded by the browser from a domain that is not ours. These static assets are characterised by:

* Being essential or important for the working of a page.
* Being updated infrequently.
* Require some manual intervention in order to be updated.

Usually these assets are added to the page as part of the application, and not through tag managers.

For this kind of static resources is our choice to **self-host them on our servers** instead of including them on our pages from an external CDN.

## Benefits of self-hosting static assets

* **Resilience.** As long as our site is up, the resource will be up. We don't depend on other servers or additional CDNs and we won't be affected by their outages, or closure of the service.
* **Consistency.** Static assets are cached and served in exactly the same way that the reset of our resources are, and they use the same CDN. As a result, timings and user experience is more consistent all around the world.
* **Security.** reduces our front-end [attack surface](https://en.wikipedia.org/wiki/Attack_surface).
* **Performance.** Self-hosting can save us the cost of the DNS request, TCP connection and TLS negotiation, which in slow connections can easily be between 1000ms and 2000ms. This can also be mitigated with `rel=preconnect`.
* **Filtering.** Some CDNs are filtered by the big firewall in China. This can slow down the loading of the page, or even make them break. Self-hosting static assets prevents this.
* **Security.** Self-hosting the asset makes it easier for us to use [Subresource Integrity (SRI)](https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity) in the future.
