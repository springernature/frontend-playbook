# Managing static assets

Static assets are files that don't need to be generated, modified or processed by an application before being delivered to the user. This typically includes CSS, JavaScript, images and web fonts. Static assets change rarely, and their content doesn't depend on user input or preferences.

**We [MUST][rfc-2119] host these kinds of static resources on our own infrastructure and Content Delivery Network (CDN) instead of including them on our pages from a third-party CDN.**

JavaScript files or libraries introduce security and data compliance risk. Resources related to fonts and videos also carry heightened data compliance risk on the basis of legal precedence.

Self-hosting static assets has several advantages over relying on third parties for their delivery:

* **Data protection.** When a user requests a resource from a third party service via a site we control, we are responsible for sharing their Personally Identifiable Information - such as user IP addresses - with the third party. We have a commitment to treating our users personal data with proper care, and a responsibility to the company to follow local privacy laws.
* **Robustness.** As long as our site is up, the static resource will be up too. We don't depend on third party servers or additional CDNs besides our own, and we won't be affected by their outages, or closure of the service.
* **Consistency.** Static assets are cached and served like the rest of our resources, and use the same CDN. As a result, resource timings and user experience are more consistent all around the world.
* **Security.** Reduces our front-end [attack surface](https://en.wikipedia.org/wiki/Attack_surface) as the resources will enjoy the same level of security as the rest of first party content, and we don't have to trust the security of third parties. Self-hosting the asset makes it easier for us to use [Subresource Integrity (SRI)](https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity) for an additional layer of security.
* **Control.**
If we serve the asset we also have more control of how it's cached across the internet and by clients - so in the event of a compliance or security issue, we are able to react and protect our users and the company more quickly.
* **Performance.** Self-hosting may save the users the cost of the DNS request, TCP connection and TLS negotiation for each CDN-hosted request, which in slow connections may make a big difference. This can also be mitigated with [`rel=dns-prefetch`](https://developer.mozilla.org/en-US/docs/Learn/Performance/dns-prefetch) and [`rel=preconnect`](https://developer.mozilla.org/en-US/docs/Web/HTML/Link_types/preconnect), but self-hosting the assets eliminates that penalty completely.
* **Filtering.** Some CDNs are filtered by the [Great Firewall of China (GFW)](https://en.wikipedia.org/wiki/Great_Firewall). This can slow down the loading of certain resources, or even make them fail to load completely. Self-hosting static assets helps mitigate this, as all of the 1st party resources on a page will be served from the same place.

[rfc-2119]: https://tools.ietf.org/html/rfc2119
