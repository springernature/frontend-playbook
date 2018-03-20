# Secure Markup

TODO: add TOC

## Scope of this document
You should be aware of the security implications of your front-end code. This document outlines some steps you can take to reduce the risk of markup exposing us, or our users, to security flaws.

Note: this document does not cover JavaScript, or interactions which may touch the server, e.g. XSS or HTTP headers. (It is assumed security-related headers are set in the HTTP headers, not in `meta` tag equivalents.)

Additionally, you're encouraged to familiarise yourself with the [OWASP HTML5 Security Cheat Sheet](https://www.owasp.org/index.php/HTML5_Security_Cheat_Sheet).

## Use UTF-8 and specify this in a `meta` tag

Do this: `<meta charset="utf-8">`.

Not specifying the appropriate character set has historically has been a source of [charset-related security problems](https://code.google.com/archive/p/doctype-mirror/wikis/ArticleUtf7.wiki) as well as a source of rendering bugs.

## Add `rel="noopener"` to outbound links in new windows

Links leak the context of the opening window in the `window.opener` object. This allows the opened window to alter the opening window via JavaScript, regardless of whether the window is opened via JavaScript or simply a `target="_blank"` attribute. Exploiting this context leaking is known as ["tabnabbing"](https://mathiasbynens.github.io/rel-noopener/).

## Use sane form defaults

We must not write data that comes from the user into the DOM without first [sanitising](https://www.smashingmagazine.com/2011/01/keeping-web-users-safe-by-sanitizing-input-data/) that data. Input includes not only form data, but also things like user agent strings, request headers, URL parameters and cookies.

Sanitising input is the responsibility of the server in most cases, but we must also sanitise input in rich JavaScript applications (e.g. URL fragments) at the risk of exposing our users to attacks like [DOM XSS/Client-Side XSS](https://www.owasp.org/index.php/Types_of_Cross-Site_Scripting#DOM_Based_XSS_.28AKA_Type-0.29).

Such sanitisation is beyond the scope of this document, but as authors of HTML forms in particular we can mitigate _some_ classes of client-side attack by specifying some form widget attributes. This is no substitute for sanitisation but forms part of a ["belt & braces"](https://www.collinsdictionary.com/dictionary/english/belt-and-braces) approach to security, as well as reducing a common source of bugs.

- `form` &mdash; specify `accept-charset="utf-8"`. Charset issues are a common source of bugs generally. If a page has been parsed as UTF-8 the browser _should_ default to sending data as UTF-8, but it's easy to specify the `accept-charset` as extra protection in case something breaks, so why not do it?
- `input` &mdash; if the value of the type attribute is `text`, `email`, `search`, `password`, `tel`, or `url`, specify the `maxlength` attribute.
- `textarea` &mdash; specify the `maxlength` attribute.
- for non-essential "autocomplete" functionality, consider using a `datalist` element instead of JavaScript.
- `input type="file"` &mdash; use the `accept` attribute **TODO: not specifying this smells bad, but is it?**
- `autocomplete` **TODO there are info leakage issues (at least) around use of this if a vector is found, but is that enough for a blanket "considered harmful"?**
- `keygen` is deprecated, don't use it.

## Use the `sandbox` attribute for `iframe`s

Even if you control the content of the `iframe`, do use the `sandbox` attribute. This attribute restricts the functionality of the framed document.

Note the default behaviour of the attribute is very strict (e.g. no JavaScript, forms cannot be submitted) so tailor the value of the attribute to your use case. Mike West has written [a great article about `iframe sandbox`](https://www.html5rocks.com/en/tutorials/security/sandboxed-iframes/) and MDN has [a lovely reference article on `sandbox`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe#attr-sandbox).

## Use the `type` & `typemustmatch` attribute for `object`s

`typemustmatch` is currently very new, and lacking support in browsers &mdash; but no harm including it if you can.

> This Boolean attribute indicates if the type attribute and the actual content type of the resource must match to be used.
> &mdash; <cite>[MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/object#attr-typemustmatch)</cite>

For more information please see the [W3C HTML5.3 specification](https://www.w3.org/TR/html53/semantics-embedded-content.html).

----

