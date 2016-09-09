Markup

Background

HTML up to 3.2 was written with SGML syntax rules.  HTML 4 was written with SGML syntax (HTML 4.01) and XML (XHTML 1.0).  HTML 5 breaks with SGML and has two serializations, a new one called "html" (which looks like SGML but is not an application of SGML) and again XML (XHTML).

https://www.w3.org/blog/2008/01/html5-is-html-and-xml/

HTML vs XML

When a document is transmitted with an XML MIME type, such as application/xhtml+xml, this is intended to hint to the client that the document should be rendered with an XML parser, and popular contemporary clients honour this.

https://www.w3.org/TR/html5/introduction.html#html-vs-xhtml

One of the benefits of XML is its strictness -- the flipside of this benefit is that XML is not designed to fail safely.  The internet, the web, and typical web clients however are designed to fail safely. This is a philosophical difference with practical implications.

In professional web development, one typically has to rely on 3rd-party code which is executed in our domain, but under which we have no real control (advertisments, tracking code, resources served from 3rd-party CDNs, etc).  Additionally accidents happen, and broken code goes live.  So we must think defensively and cannot rely on the validity and stability of our documents.  When XHTML is served with an application/xhtml+xml MIME type, any errors introduce fatal errors in the document parser and completely unusable pages are the result.

So for business purposes it is impractical to serve XHTML with anything other than a text/html MIME type.  This means the client cannot leverage an XML parser and instead uses a regular HTML parser, so any XML benefits are lost to the client. Additionally it introduces cognitive dissonance (a document which is an application of XML not being treated as such), we are serving a heavier page over an HTML 5 equivalent for no client-side benefit, and we lose some HTML features with XHTML such as NOSCRIPT (which still appears in 3rd-party code).

https://www.w3.org/TR/html5/scripting-1.html#the-noscript-element

It is not impossible to imagine a back-end markup-generation system that only ouputs XHTML, but as any valid XHTML document is essentially expressable in HTML* (the reverse is not true) this should be seen as a shortcoming in the markup generator, at least as far as the client is concerned.

*contentious -- exceptions?


Validation

We must strive to ensure all HTML documents validate.  Invalid markup results in us relying on any client to do what we intended, not what we instructed.  Clients regularly disagree on how to interpret out instructions, yet alone our intentions, so in the interests of consistency of execution we must do what we can to ensure our HTML is valid.

To omit end tags?
While the HTML4 & 5 specs allow some end tags to be omitted for some (but not all) elements, it's unreasonable to expect developers to remember which elements this applies to.  Additionally this kind of inconsistency can play havok with automatic syntax highlighting tools, and impairs our ability to spot bugs that would otherwise offend our pattern-recognition powers.


Void elements -- to explicitly or implicitly close?
https://www.w3.org/TR/html5/syntax.html#void-elements

We implicitly close void elements.  Explicitly closing void elements (e.g. <br />) is not invalid per se in HTML 5.  However, explicitly closing void elements is an artifact of XML serializations, not HTML, so may introduce cognitive dissonance in many authors given that we are authoring html.  Another source of dissonance is that explicitly closing void elements was invalid in older verions of HTML.

Conversely, it may be the case that their omission impacts authors more used to writing XML, or HTML with an XML serialization. However as far as machines are concerned, they increase page weight with zero benefit.


