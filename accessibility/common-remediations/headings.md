# Headings  

Headings are vital for screen reader users to be able to make sense of your pages. Without a proper heading structure, they can't explore your document easily and can struggle to use your interface. 

## The issues

- [Headings used for styling](#headings-used-for-styling)
- [Implied headings](#implied-headings)
- [Multiple H1s per page](#multiple-h1s-per-page)
- [Heading sequence is not logical](#heading-sequence-is-not-logical)
- [Missing heading](#missing-heading)

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