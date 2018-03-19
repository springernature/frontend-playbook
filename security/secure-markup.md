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

## Use sane form defaults

Sanitising user input is the job of the server and/or JavaScript, but we can help by specifying some attributes of form widgets as part of a ["belt & braces"](https://www.collinsdictionary.com/dictionary/english/belt-and-braces) approach to security:

**TODO: how contentious is ^that?**

- `form` -- specify `accept-charset` and `enctype` **TODO: not specifying these smells bad, but is it?**
- `input` -- if the value of the type attribute is `text`, `email`, `search`, `password`, `tel`, or `url`, specify the `maxlength` attribute.
- `textarea` -- specify the `maxlength` attribute.
- for non-essential "autocomplete" functionality, consider using a `datalist` element instead of JavaScript.
- `input type="file"` -- use the `accept` attribute **TODO: not specifying this smells bad, but is it?**
- `autocomplete` **TODO there are info leakage issues (at least) around use of this if a vector is found, but is that enough for a blanket "considered harmful"?**
- `keygen` is deprecated, don't use it.

## Use the `sandbox` attribute for `iframe`s

Even if you control the content of the `iframe`, do use the `sandbox` attribute. This attribute restricts the functionality of the framed document.

Note the default behaviour of the attribute is very strict (e.g. no JavaScript, forms cannot be submitted) so tailor the value of the attribute to your use case. Mike West has written [a great article about `iframe sandbox`](https://www.html5rocks.com/en/tutorials/security/sandboxed-iframes/) and MDN has [a lovely reference article on `sandbox`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe#attr-sandbox).

## Use the `type` & `typemustmatch` attribute for `object`s

`typemustmatch` is currently very new, and lacking support in browsers -- but no harm including it if you can.

> This Boolean attribute indicates if the type attribute and the actual content type of the resource must match to be used.
> &mdash; <cite>[MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/object#attr-typemustmatch)</cite>

For more information please see the [W3C HTML5.3 specification](https://www.w3.org/TR/html53/semantics-embedded-content.html).

----

