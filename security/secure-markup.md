# Secure Markup

Developers should be aware of the security implications of their front-end code. This document outlines some steps developers can follow to ensure their makup does not expose us, or users, to common security flaws.

Note: this document does not cover JavaScript, or interactions which may touch the server, e.g. XSS or HTTP headers. (It is assumed security-related HTTP headers are set in the headers, not in the `meta` tag equivalents.)

Additionally, developers are encouraged to familiarise themsevles with the [OWASP HTML5 Security Cheat Sheet](https://www.owasp.org/index.php/HTML5_Security_Cheat_Sheet).

## Use UTF-8 and specify this in a `meta` tag

Do this: `<meta charset="utf-8">`.

Not specifying the appropriate character set is a source of rendering bugs and historically has been a source of [charset-related security problems](https://code.google.com/archive/p/doctype-mirror/wikis/ArticleUtf7.wiki).

(As an aside, the longer `<meta http-equiv="Content-Type" content="text/html; charset=utf-8">` is functionally equivalent and should be avoided.)

## Add `rel="nopener"` to outbound links

Links leak the context of the opening window in the `window.opener` property, most notably a problem with links opening in new windows. This allows the opened window to alter the opening window via JavaScript. Exploiting this context leaking is know as ["tabnabbing"](https://mathiasbynens.github.io/rel-noopener/).

## Use the `sandbox` attribute for `iframe`s

Even if you control the content of the `iframe`, do use the `sandbox` attribute. This attribute restricts the functionality of the framed document.

Note the default behaviour of the attribute is very strict (e.g. no JavaScript, forms cannot be submitted) so tailor the value of the attribute to your use case. Mike West has written [a great article about `iframe sandbox`](https://www.html5rocks.com/en/tutorials/security/sandboxed-iframes/) and MDN has [a lovely reference article on `sandbox`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe#attr-sandbox).

## Use the `type` & `typemustmatch` attribute for `object`s

Bleeding edge at the time of writing, but no harm including it if you can.

> This Boolean attribute indicates if the type attribute and the actual content type of the resource must match to be used.
> &mdash; <cite>[MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/object#attr-typemustmatch)</cite>

For more information please see the [W3C HTML5.3 specification](https://www.w3.org/TR/html53/semantics-embedded-content.html).


----


TODO 
mime types 
sane form defaults


