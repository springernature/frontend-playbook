# Markup

## Background

HTML up to 3.2 was written with SGML syntax rules.  HTML 4 could be written with either SGML syntax (HTML 4.01) or XML (XHTML 1.0).  [HTML 5 breaks with SGML and has two serializations](https://www.w3.org/blog/2008/01/html5-is-html-and-xml/), a new one called "html" (which looks like SGML but is not an application of SGML) and again XML (XHTML).


## HTML vs XHTML

**We author HTML 5.**

When a document is transmitted with an XML MIME type, such as `application/xhtml+xml`, this is intended to instruct the client to render using an XML parser, and popular contemporary clients honour this. [See HTML vs XHTML on w3.org](https://www.w3.org/TR/html5/introduction.html#html-vs-xhtml).

One of the benefits of XML is its strictness -- the flip-side of this benefit is that XML is not designed to fail safely.  The internet, the web, and typical web clients are however designed to fail safely. This is a philosophical difference with practical implications.

In professional web development, one typically has to rely on 3rd-party code which is executed in our domain, but under which we have no real control (advertisements, tracking code, resources served from 3rd-party CDNs, etc).  Additionally accidents happen, and broken code goes live.  So we must think defensively and cannot rely on the validity of our documents.  When XHTML is served with an `application/xhtml+xml` MIME type, any errors introduce fatal errors in the document parser and completely unusable pages are the result.

So for business purposes it is impractical to serve XHTML with anything other than a `text/html` MIME type.  This means the client cannot leverage an XML parser and instead uses a regular HTML parser, so any XML benefits are lost to the client. Additionally it introduces cognitive dissonance (a document which is an application of XML not being treated as such), we are serving a heavier page over an HTML 5 equivalent for no client-side benefit, and we lose some HTML features with XHTML such as [NOSCRIPT](https://www.w3.org/TR/html5/scripting-1.html#the-noscript-element) (which still appears in 3rd-party code).

It is not impossible to imagine a back-end markup-generation system that only outputs XHTML, but as any valid XHTML document is essentially expressible in HTML (the reverse is not true)* this should be seen as a shortcoming in the markup generator, at least as far as the client is concerned.

All things considered, it makes no sense to author XHTML.

***contentious -- exceptions?** as if that is the only contentious thing in this doc.


## Validation

**We do what is reasonable to ensure our documents [validate](https://validator.w3.org/) .**

Invalid markup results in authors relying on all clients to do what they intended, not what they instructed.  Clients regularly disagree on how to interpret out instructions, yet alone our intentions, so to promote consistency of execution we must do what we can to ensure our HTML is valid.

## To omit optional end tags?

**We do not omit optional end tags.**

While the HTML 4 & 5 specs allow some end tags to be omitted for _some_ non-[void elements](https://www.w3.org/TR/html5/syntax.html#void-elements), it's unreasonable to expect authors to remember which elements this applies to.  Additionally this kind of inconsistency can play havok with text editors, any indentation policy, and impairs our ability to spot bugs that would otherwise offend our pattern-recognition powers.


## Void Elements -- to explicitly or implicitly close?

**We implicitly close void elements.**

Explicitly closing void elements (e.g. `<br />`) is not invalid per se in HTML 5.  However, explicitly closing void elements is an artifact of XML serialization, not html, so may introduce cognitive dissonance in many authors given that we are authoring html.  Another source of dissonance is that explicitly closing void elements was invalid in older versions of HTML.

Conversely, it may be the case that their omission impacts authors more used to writing XML, or HTML with an XML serialization. However as far as machines are concerned, they increase page weight with zero benefit.


