# Markup

This document outlines the way we write markup and why. See our [house style document](../practices/house-style.md) to understand the rationale behind enforcement of style. 

- [HTML vs XHTML](#html-vs-xhtml)
	- [Validation](#validation)
	- [Do not omit optional end tags](#do-not-omit-optional-end-tags)
	- [Implicitly close void elements](#implicitly-close-void-elements)
	- [Form submit controls](#form-submit-controls)
- [Semantics](#semantics)
	- [Follow the HTML 4 outline model for heading levels](#follow-the-html-4-outline-model-for-heading-levels)
- [Templates](#templates)

## HTML vs XHTML

HTML up to 3.2 was written with SGML syntax rules.  HTML 4 could be written with either SGML syntax (HTML 4.01) or XML (XHTML 1.0).  [HTML 5 breaks with SGML and has two serializations](https://www.w3.org/blog/2008/01/html5-is-html-and-xml/), a new one called "html" (which looks like SGML but is not an application of SGML) and again XML (XHTML).

### We author HTML 5

When a document is transmitted with an XML MIME type, such as `application/xhtml+xml`, this is intended to instruct the client to render using an XML parser, and popular contemporary clients honour this. [See HTML vs XHTML on w3.org](https://www.w3.org/TR/html5/introduction.html#html-vs-xhtml).

One of the benefits of XML is its strictness -- the flip-side of this benefit is that XML is not designed to fail safely.  The internet, the web, and typical web clients are however designed to fail safely. This is a philosophical difference with practical implications.

In professional web development, one typically has to rely on 3rd-party code which is executed in our domain, but under which we have no real control (advertisements, tracking code, resources served from 3rd-party CDNs, etc).  Additionally accidents happen, and broken code goes live.  So we must think defensively and cannot rely on the validity of our documents.  When XHTML is served with an `application/xhtml+xml` MIME type, any errors introduce fatal errors in the document parser and completely unusable pages are the result.

So for business purposes it is impractical to serve XHTML with anything other than a `text/html` MIME type.  This means the client cannot leverage an XML parser and instead uses a regular HTML parser, so any XML benefits are lost to the client. Additionally it introduces cognitive dissonance (a document which is an application of XML not being treated as such), we are serving a heavier page over an HTML 5 equivalent for no client-side benefit, and we lose some HTML features with XHTML such as [NOSCRIPT](https://www.w3.org/TR/html5/scripting-1.html#the-noscript-element) (which still appears in 3rd-party code).

It is not impossible to imagine a back-end markup-generation system that only outputs XHTML, but as any valid XHTML document is essentially expressible in HTML (the reverse is not true) this should be seen as a shortcoming in the markup generator, at least as far as the client is concerned.

As such it seems beneficial to choose HTML 5 over XHTML.

### Validation

Do what is reasonable to ensure your documents [validate](https://validator.w3.org/). 

Invalid markup results in authors relying on all clients to do what they intended, not what they instructed.  Clients regularly disagree on how to interpret our instructions, yet alone our intentions, so to promote consistency of execution you must do what you can to ensure your HTML is valid.

Additionally, invalid HTML violates WCAG 2.1 Success Criterion [4.1.1 Parsing](https://www.w3.org/TR/WCAG21/#parsing) (Level A), and areas where your product falls short must be noted on your product's VPAT. It's probably easier just to make sure your HTML is valid in the first place. 

### Do not omit optional end tags

While the HTML 4 & 5 specs allow some end tags to be omitted for _some_ non-[void elements](https://www.w3.org/TR/html5/syntax.html#void-elements), it's unreasonable to expect authors to remember which elements this applies to.  Additionally this kind of inconsistency can play havok with text editors, any indentation policy, and impairs our ability to spot bugs that would otherwise offend our pattern-recognition powers.

We do this:

```html
<ol>
    <li>foo</li>
    <li>bar</li>
</ol>
```

We *don't* do this:

```html
<ol>
    <li>foo
    <li>bar
</ol>
```

### Implicitly close void elements

Explicitly closing void elements (e.g. `<br />`) is not invalid per se in HTML 5.  However, explicitly closing void elements is an artifact of XML serialization, not HTML 5's "html" serialization, so may introduce cognitive dissonance in many authors given that we are authoring html.  Additionally, explicitly closing void elements was invalid in older versions of HTML.

Conversely, it may be the case that their omission impacts authors more used to writing XML, or HTML with an XML serialization. However as far as machines are concerned, they increase page weight with zero benefit.

We do this:

```html
<meta charset="UTF-8">
```

We *don't* do this:

```html
<meta charset="UTF-8" />
```
### Form submit controls

In modern browsers, `button type="submit"` provides a superset of functionality when compared to `input type=submit`.

`button` elements are much easier to style than `input` elements. You can add
inner HTML content (think `<em>`, `<strong>`, or even `<img>`), and use
`::after` and `::before` pseudo-elements to achieve complex rendering while
`input` only accepts a textual value attribute.

**Note**: Submitting is `button` default behaviour, but we want to "code for
humans". Therefore do not ommit `type="submit"`.

Make sure to specify `name` and `value` attributes to maximize browsers
compatibility ([See IE11-Only Submit Bug on Stack
Overflow](https://stackoverflow.com/a/22703881/9461391)).

We do this:

```html
<form>
	<button type="submit" name="myButton" value="foo">Continue</button>
</form>
```

We *don't* do this:

```html
<form>
	<input type="submit" value="Continue">
</form>
```

and

We *don't* do this:

```html
<form>
	<button>Continue</button>
</form>
```

**Caution**: There is a shortcoming for Internet Explorer when using the `button`
element. Indeed it submits the text within the `button` element as its value in
the form data rather than the value of its `value` attribute.
This becomes problematic when using multiple submit buttons in a single form with each a different value and purpose. 

Here are some suggestions to work around these:

- Redesign the interface so multiple submit buttons are not required.
  - (Preferred) Use a multiple pages form as recommended by GOV.UK in [Structuring forms,
    Start with one thing per
    page](https://www.gov.uk/service-manual/design/form-structure#start-with-one-thing-per-page).
  - Replace them with radio buttons and a single submit button (requires an
    extra click from the user though);
- Use a separate form for each instance, with a hidden `input` providing
  the data the submit `button` would normally carry. This can be a good
  solution when you have a simple “Delete this row” problem.
- Last resort solution: Hide the value inside the name of the control. A loop
  over the names from the form data is needed in the business logic then. Please
  avoid as much as you can as this adds complexity to code and may degrade
  performance.

## Semantics

### Follow the HTML 4 outline model for heading levels

When HTML 5 was first announced, it brought with it a plethora of new semantic elements and an entirely new document outline model which leveraged them to provide meaning.  This was intended to supplant the HTML 4 model in which the heading level (h1 - h6) was used to imply the structure of the HTML document.  See [Using HTML sections and outlines](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Using_HTML_sections_and_outlines) for more information.

Unfortunately, this new document outline model was never well supported by browsers or assistive technologies. We considered sticking with the HTML 5 document outline model used in conjunction with setting ARIA attributes (`role="heading" aria-level="3"`) but this rather defeated any benefit from using the more localised heading levels, and was also poorly supported in some key assistive technologies.

The HTML 5 document outline algorithm specification has been removed in HTML 5.1. You should continue to use the older HTML 4 style heading levels in conjunction with the new HTML 5 semantic elements. Do not use multiple H1 headings on a single page. 

See the HTML specification for [the current recommendation for use in all HTML 5 documents](https://www.w3.org/TR/html5/sections.html#the-h1-h2-h3-h4-h5-and-h6-elements).

We do this:

```html
<h1>Page title</h1>

<article>
	<h2>Article title</h2>
	<h3>Article subtitle</h3>
</article>

<footer>
	<h2>Footer title</h2>
</footer>
```

We *don't* do this:

```html
<h1>Page title</h1>

<article>
	<h1>Article title</h1>
	<h2>Article subtitle</h2>
</article>

<footer>
	<h1>Footer title</h1>
</footer>
```

## Templates

Templates should, where possible, be written using [DustJS](http://www.dustjs.com/) or [Handlebars](http://handlebarsjs.com/). Use of linting is encouraged to prevent common errors. For projects using DustJS  [Dustmite](https://www.npmjs.com/package/dustmite) should be used. Dustmite will prevent any syntax errors. It also enforces consistent style in your template code and can catch more subtle errors like usage of the potentially unsafe `{@if}` dust helper.
