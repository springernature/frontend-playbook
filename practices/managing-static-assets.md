# Managing static assets

Static assets are files that don't need to be generated, modified or processed by an application before being delivered to the user. This typically includes CSS, JavaScript, images and web fonts. Static assets change rarely, and their content doesn't depend on user input or preferences.

We host on our own infrastructure these kinds of static resources, instead of including them on our pages from an third-party CDN. This applies especially to JavaScript files or libraries, and font files.

Self-hosting static assets has several advantages over relying on third parties for their delivery:

* **Resilience.** As long as our site is up, the static resource will be up too. We don't depend on third party servers or additional CDNs besides our own, and we won't be affected by their outages, or closure of the service.
* **Consistency.** Static assets are cached and served like the rest of our resources are, and they use the same CDN. As a result, resource timings and user experience are more consistent all around the world.
* **Security.** reduces our front-end [attack surface](https://en.wikipedia.org/wiki/Attack_surface) as the resources will enjoy the same level of security as the rest of first party content, and we don't depend on third parties being secure. Self-hosting the asset makes it easier for us to use [Subresource Integrity (SRI)](https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity) for an additional layer of security.
* **Performance.** Self-hosting can save the users the cost of the DNS request, TCP connection and TLS negotiation for each self-hosted request, which in slow connections can make a big difference. This can also be mitigated with [`rel=dns-prefetch`](https://developer.mozilla.org/en-US/docs/Learn/Performance/dns-prefetch) and [`rel=preconnect`](https://developer.mozilla.org/en-US/docs/Web/HTML/Link_types/preconnect), but self-hosting the assets eliminates that penalty completely.
* **Filtering.** Some CDNs are filtered by the big firewall in China. This can slow down the loading of certain resources, or even make them fail to load completely. Self-hosting static assets helps mitigate this, as all of the 1st party resources on a page will be served from the same place.
