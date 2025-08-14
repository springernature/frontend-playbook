# Success Criterion 1.3.1 Info and Relationships

This criterion is probably the most complex of all WCAG's criteria - fundamentally it involves implementing good semantics and information architecture so that Assistive Technology can properly report and interact with components. 

See [Understanding Info and Relationships](https://www.w3.org/WAI/WCAG22/Understanding/info-and-relationships.html) for further details. 

The issues and remediations listed in this file are not exhaustive. 

## The issues

- [Headings](#headings)
  - [Headings used for styling](#headings-used-for-styling)
  - [Implied headings](#implied-headings)
  - [Multiple H1s per page](#multiple-h1s-per-page)
  - [Heading sequence is not logical](#heading-sequence-is-not-logical)
  - [Missing heading](#missing-heading)
- [Page titles](#page-titles)  
  - [Title doesn’t describe the page](#title-doesnt-describe-the-page)
  - [Same title used on multiple pages](#same-title-used-on-multiple-pages)
- [Semantics](#semantics)
- [No built-in semantics](#no-built-in-semantics) 

## Headings

Headings are vital for screen reader users to be able to make sense of your pages. Without a proper heading structure, they can't explore your document easily and can struggle to use your interface. 

### Headings used for styling

#### What's the problem?

Semantic heading tags (i.e. `<h1>`, `<h2>`, `<h3>`, `<h4>`, `<h5>`, `<h6>`) are being used purely to visually style text that doesn't head a section of content. 

#### Who's affected by the problem?

* Screen reader users
* Search engines

#### Why's it a problem?

Semantic tags have meaning. When you use a semantic tag for something other than its meaningful purpose, your document makes less sense. This is a severe issue for screen reader users, who need proper semantic structure in order to understand how your document is structured. 

Search engines also use heading levels to get a sense of the information that your page contains. If your document misuses semantic tags for visual effect, search engines are less able to parse the information in your document and your pages could be penalised in [SERPs](https://en.wikipedia.org/wiki/Search_engine_results_page), or be less discoverable to search engine users. 

The purpose of CSS is to separate the concerns of visual styling from the base structure of semantic HTML. Mixing the two together violates the principle of [Separation of Concerns](https://en.wikipedia.org/wiki/Separation_of_concerns#HTML,_CSS,_JavaScript). 

#### How do I fix it? 

Do not use semantic heading tags to control the appearance of text. Use CSS for styling.

We do this:
```html
<h2 class=”h4”>This content needs a level 2 heading but I want it to look like a level 4 heading</h2>
```
 
We _don’t_ do this:
 
```html
<h4>This content needs a level 2 heading but I want it to look like a level 4 heading</h4>
```

### Implied headings

#### What's the problem?

CSS has been used to visually style text so that it looks like a heading, but there are no semantic heading tags (i.e. `<h1>`, `<h2>`, `<h3>`, `<h4>`, `<h5>`, `<h6>`).

#### Who's affected by the problem?

* Screen reader users
* Search engines

#### Why's it a problem?

Semantic tags have meaning. When semantic tags are absent from your document, it makes less sense. This is a severe issue for screen reader users, who need proper semantic structure in order to understand how your document is structured. 

Search engines also use heading levels to get a sense of the information that your page contains. If your document omits semantic tags, search engines are less able to parse the information in your document and your pages could be penalised in [SERPs](https://en.wikipedia.org/wiki/Search_engine_results_page), or be less discoverable to search engine users. 

#### How do I fix it? 

Do not style text to give the visual appearance of headings. Use semantic heading tags.

We do this:
 
```html
<h1>Level 1 heading</h1>
<h2>Level 2 heading</h2>
```
 
We _don’t_ do this:
 
```html
<p class=”h1”>Level 1 heading</p>
<p class=”h2”>Level 2 heading</p>
```

### Multiple H1s per page

#### What's the problem?

The document contains multiple `<h1>` elements. 

#### Who's affected by the problem?

* Screen reader users

#### Why's it a problem?

Screen reader users use semantic heading tags to understand the structure of the page. Respondents to the WebAIM Screen Reader Survey strongly prefer to see [one first level heading that contains the document title](https://webaim.org/projects/screenreadersurvey7/#heading). 

Multiple `<h1>` elements make it more difficult for them to understand the overall structure and purpose of the page. 

The W3C makes the case for a single `<h1>` element to describe the overall purpose of the entire page:

* The HTML spec says ["the h1 is the top level heading"](https://www.w3.org/TR/html5/sections.html#the-h1-h2-h3-h4-h5-and-h6-elements)
* The WAI recommendation says ["The most important heading has the rank 1 (h1)"](https://www.w3.org/WAI/tutorials/page-structure/headings/)

#### How do I fix it? 

Use a single level 1 heading to describe the topic or purpose of the page; it’s approximately equivalent to the text in the `<title>` element. 

We do this:
 
```html
<h1>My cool website about geese</h1>
<h2>Facts about geese</h2>
<h2>My short story about a goose I knew</h2>
```
 
We _don’t_ do this:
 
```html
<h1>My cool website about geese</h1>
<h1>Facts about geese</h1>
<h1>My short story about a goose I knew</h1>
```

### Heading sequence is not logical

#### What's the problem?

The sequence of headings doesn't accurately describe the structure of the page. You may have skipped heading levels, used the wrong heading level for a page section, or followed a heading with a different heading level that doesn't make sense. 

#### Who's affected by the problem?

* Screen reader users
* Search engines

#### Why's it a problem?

Semantic tags have meaning. When your semantic tags are arranged incorrectly, your document makes less sense. This is a severe issue for screen reader users, who need proper semantic structure in order to understand how your document is structured. 

Search engines also use heading levels to get a sense of the information that your page contains. If your document omits semantic tags, or uses them incorrectly, search engines are less able to parse the information in your document and your pages could be penalised in [SERPs](https://en.wikipedia.org/wiki/Search_engine_results_page), or be less discoverable to search engine users. 

#### How do I fix it? 

Your headings must follow a logical sequence from `<h1>` to `<h6>`. If you need to style a heading in a particular way, control that with CSS, not semantic heading tags. 

It may help to think about the heading structure of a web page as its table of contents.

We do this:

```html 
<h1>Homepage</h1>
  <h2>Headline Topic 1</h2>
     <h3>News Headline 1</h3>
     <h3>News Headline 2</h3>
        <h4>News Headline subtopic</h4>
  <h2>Headline Topic 2</h2>
     <h3>News Headline 1</h3>
     <h3>News Headline 2</h3>
        <h4>News Headline subtopic</h4>
```

We _don't_ do this:

```html
<h1>My Homepage</h1>
  <p>Headline Topic 1</p>
    <h2>News Headline 1</h2>
    <h4>News Headline 2</h4>
      <p>News Headline subtopic</p>
  <h3>Headline Topic 2</h3>
```

### Missing heading

#### What's the problem?

A section or context lacks a heading. It may be a section of a page, or a standalone context like a modal dialog. 

#### Who's affected by the problem?

* Screen reader users
* Users with cognitive disabilites or challenges

#### Why's it a problem?

Headings help users understand the structure of a page. When new sections or contexts are introduced without them, it can be difficult for users to understand how the content relates to the rest of the page. 

If a screen reader user is taken to a new context (e.g. a modal dialog) without a heading, it can be difficult for them to understand what's just happened without tabbing through the rest of the document to work it out.

#### How do I fix it? 

When you change context or begin a new section, use a heading to announce the content.

It may help to think about the heading structure of a web page as its table of contents. A ToC contains a reference to everything on the page - your heading structure should do the same. 


## Page titles

The HTML `<title>` element provides vital information to many users about the purpose and identity of your pages. Page titles must be provided, unique, and useful. 

### Title doesn’t describe the page

#### What's the problem?

The `<title>` element fails to describe the purpose of the page. You may have failed to add a title, used title text that is too generic to be useful, or used an excessively long title that obscures the page purpose. 

#### Who's affected by the problem?

* Everyone

#### Why's it a problem?

When your page titles are inadequate:

* Screen reader users are unable to know what the point of a page is without scanning its entire contents
* All users are unable to easily find the correct tab if they temporarily change contexts
* All users who bookmark the page with their browser are given a poor default name for the bookmark
* Search engines may only display the first 50-60 characters of the title attribute, so information could be lost in [SERPs](https://en.wikipedia.org/wiki/Search_engine_results_page)

#### How do I fix it? 

All page titles must clearly summarise the purpose of the page. Front-load the most important information about the page so that it appears first. 

We do this:
```html
<title>Career opportunities | Website.com </title>
<title>Contact us | Website.com </title>
```
 
We _don’t_ do this:
```html
<title>Website.com</title>
<title>Website</title>
<title>Website.com sells vital products in very important markets to our many happy customers | Contact Us</title>
```

### Same title used on multiple pages

#### What's the problem?

The `<title>` attribute fails to differentiate the purpose of the page. 

#### Who's affected by the problem?

* Everyone

#### Why's it a problem?

When your page titles are the same on every page:

* Screen reader users are unable to know what the point of a page is without scanning its entire contents
* All users are unable to easily find the correct tab if they temporarily change contexts
* All users who bookmark the page with their browser are given a poor default name for the bookmark

#### How do I fix it? 

Where pages are unique, their titles must also be unique. The page title should usually match the main heading (h1) of the page.

We do this:
```html
<title>Checkout | Billing information | My webpage </title>
<title>Checkout | Review Cart | My webpage </title>
```

We _don’t_ do this:
```html
<title>Checkout | My webpage</title>
```

## Semantics

Using the correct semantics in your HTML is vital if your page is going to work with technology that interfaces with it. At the most basic level, this means browsers themselves, but it's also required for assistive technology, search engines, third party content readers, virtual assistants like Siri or Cortana, and any other technical interface that can read and repurpose a webpage. 

### No built-in semantics

#### What's the problem?

HTML elements with no semantics (`<div>`s and `<span>`s) have been used instead of elements with the correct semantics. The elements may be styled with CSS to look like semantic elements, and/or have JavaScript functionality attached that makes them perform in a similar way to a native element, but the correct native element has not been used. 

#### Who's affected by the problem?

* Everyone

#### Why's it a problem?

HTML elements with no semantics are not understood or handled automatically by user agents. Unless you fully understand the entire specification for a native element (such as a `<button>`), and implement it precisely to that specification, your attempts to replicate its functionality robustly for all users will fail. 

Screen reader users, voice input users, keyboard users, switch device users, users of other kinds of Assistive Technologies, search engines, various types of automated testing software, among others, are likely to be unable to use your interface if you use unsemantic elements. 

#### How do I fix it?

* Use native HTML elements unless you have a very good reason not to
* Make sure you are using the correct native HTML element for the purpose
 
We do this:

```html
<button>Toggle UI</button>
<a href=”/”>Visit this location</a>
<h2>This is a level 2 heading</h2>
```

We _don’t_ do this:

```html
<div onclick=”doFunc();”>Toggle UI</div>
<span>Visit this location</span>
<span>This is a level 2 heading</span>
```
