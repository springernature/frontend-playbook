# Secure Markup

  * [Scope of this document](#scope-of-this-document)
  * [Use UTF-8 and specify this in a `meta` tag](#use-utf-8-and-specify-this-in-a-meta-tag)
  * [Use Subresource Integrity](#use-subresource-integrity)
  * [Use sane form defaults](#use-sane-form-defaults)
    + [A note on autofill](#a-note-on-autofill)
  * [Use the `sandbox` attribute for `iframe`s](#use-the-sandbox-attribute-for-iframes)
  * [Use the `type` & `typemustmatch` attribute for `object`s](#use-the-type--typemustmatch-attribute-for-objects)

## Scope of this document
You should be aware of the security implications of your frontend code. This document outlines some steps you can take to reduce the risk of markup exposing us, or our users, to security flaws.

Note: this document does not cover JavaScript or interactions which may touch the server, e.g. XSS or HTTP headers. (It is assumed security-related headers are set in the HTTP headers, not in `meta` tag equivalents.)

Additionally, you're encouraged to familiarise yourself with the [OWASP HTML5 Security Cheat Sheet](https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/HTML5_Security_Cheat_Sheet.md).

## Use UTF-8 and specify this in a `meta` tag

Do this: `<meta charset="utf-8">`.

Not specifying the appropriate character set has historically been a source of [charset-related security problems](https://code.google.com/archive/p/doctype-mirror/wikis/ArticleUtf7.wiki) as well as a source of rendering bugs.

Ideally this should be specified in both the HTTP header and a `meta` element, in case one breaks.

## Use Subresource Integrity

Often we serve assets such as JavaScript or CSS files via [CDN](https://www.cloudflare.com/learning/cdn/what-is-a-cdn/)'s for performance reasons. But what if that resource is corrupted, either on the CDN or over the network?

Files served via CDN's (or your own asset servers) are high-priority targets for attackers, because they enable attackers to inject [payloads](https://en.wikipedia.org/wiki/Payload_(computing)#Security) into many sites with just one breach.

Subresource Integrity protects against corrupted resource files by instructing the browser to calculate a [hash](https://en.wikipedia.org/wiki/Cryptographic_hash_function) of the downloaded file's content, then compare that hash to one we previously computed for the known-good file. If the hashes don't match, the browser doesn't parse the loaded file.

We tell the browser the hash of the known-good file by embedding the hash value in the HTML&mdash;using the `integrity` attribute on the corresponding `script` or `link` element.

This may sound complicated but it's not too hard to do!

Example markup (from the [MDN article on Subresource Integrity](https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity)):
```
<script src="https://example.com/example-framework.js"
  integrity="sha384-oqVuAfXRKap7fdgcCY5uykM6+R9GqQ8K/uxy9rx7HNQlGYl1kPzQho1wx4JwY8wC"
  crossorigin="anonymous"></script>
```

(Use of the `crossorigin` attribute depends on [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) support of the asset server.)

Subresource Integrity can be used in conjunction with a [Content Security Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP) but does not require a CSP to work.

As Subresource Integrity should be relatively easy to add to a frontend build tool chain, you should use it for any `script` or `link` element, especially as [browser support for Subresource Integrity](https://caniuse.com/#feat=subresource-integrity) is good.

- [Gentle introduction to Subresource Integrity by keycdn.com](https://www.keycdn.com/support/subresource-integrity/)
- [MDN article on Subresource Integrity](https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity)

## Use sane form defaults

We must not write data that comes from the user into the DOM without first [sanitising](https://www.smashingmagazine.com/2011/01/keeping-web-users-safe-by-sanitizing-input-data/) that data. Input includes not only form data, but also things like user agent strings, request headers, URL parameters and cookies.

Sanitising input is the responsibility of the server in most cases, but we must also sanitise input in rich JavaScript applications (e.g. URL fragments) at the risk of exposing our users to attacks like [DOM XSS/Client-Side XSS](https://www.owasp.org/index.php/Types_of_Cross-Site_Scripting#DOM_Based_XSS_.28AKA_Type-0.29).

Such sanitisation is beyond the scope of this document, but as authors of HTML forms we can mitigate _some_ classes of client-side attack by specifying some form widget attributes. This is no substitute for sanitisation but constitutes part of a ["belt & braces"](https://www.collinsdictionary.com/dictionary/english/belt-and-braces) approach to security, as well as reducing common sources of bugs.

- `form` &mdash; specify `accept-charset="utf-8"`. Charset issues are a common source of bugs generally. If a page has been parsed as UTF-8 the browser _should_ default to sending data as UTF-8, but it's easy to specify the `accept-charset` as extra protection in case something breaks, so why not do it?
- `input` &mdash; if the value of the type attribute is `text`, `email`, `search`, `password`, `tel`, or `url`, specify the `maxlength` attribute.
- `textarea` &mdash; specify the `maxlength` attribute.
- `input type="file"` &mdash; use the `accept` attribute to specify which types of file can be uploaded (specify by extension or MIME type). Again this is no substitute for server validation but improves usability.
- for non-essential "autocomplete" functionality, consider using a `datalist` element instead of JavaScript.
- `keygen` is deprecated, don't use it.

### A note on autofill

Whether the browser autofills input elements is controlled by the `autocomplete` attribute, for which there are a [large number of potential values](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/autocomplete#Values).

Firstly, while there are security concerns about autofill & Personally Identifiable Information (PII),

> ...in-browser password management is generally seen as a net gain for security. Since users do not have to remember passwords that the browser stores for them, they are able to choose stronger passwords than they would otherwise.
> For this reason, many modern browsers do not support autocomplete="off" for login fields
> &mdash; <cite>[MDN - Turning off form autocompletion](https://developer.mozilla.org/en-US/docs/Web/Security/Securing_your_site/Turning_off_form_autocompletion)</cite>

As such, while you can disable autofill for sensitive fields (see MDN article above) browser vendors feel it is not a good idea overall.

Secondly,

> User agents should verify that all fields with the autocomplete attribute are visible within the viewport before automatically entering data.
> &mdash; <cite>[HTML 5.3 specification](https://www.w3.org/TR/html53/sec-forms.html#sec-autofill)</cite>

So to be sure, *avoid enabling autocomplete for elements which may be visually-hidden*.


## Use the `sandbox` attribute for `iframe`s

Even if you control the content of the `iframe`, do use the `sandbox` attribute if you can. This attribute restricts the functionality of the framed document [(_why "sandbox"?_)](https://en.wikipedia.org/wiki/Sandbox_(computer_security)).

Note the default sandbox is very strict (e.g. no JavaScript, forms cannot be submitted) so tailor the value of the attribute to your use case. Mike West has written [a great article about `iframe sandbox`](https://www.html5rocks.com/en/tutorials/security/sandboxed-iframes/) and MDN has [a lovely reference article on `sandbox`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe#attr-sandbox).

## Use the `type` & `typemustmatch` attribute for `object`s

`typemustmatch` is currently very new, and lacking support in browsers &mdash; but no harm including it if you can.

> This Boolean attribute indicates if the type attribute and the actual content type of the resource must match to be used.
> &mdash; <cite>[MDN - typemustmatch](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/object#attr-typemustmatch)</cite>

For more information please see the [W3C HTML5.3 specification](https://www.w3.org/TR/html53/semantics-embedded-content.html).

----
