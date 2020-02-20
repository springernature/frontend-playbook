# Common remediations

This page describes some common accessibility issues, and gives examples and suggestions for repairs. 

- [Keyboard navigation](#keyboard-navigation)
  - [Missing or inadequate focus styles](#missing-or-inadequate-focus-styles)
  - [Visual order doesn't match source order](#visual-order-doesnt-match-source-order)
- [Links and buttons](#links-and-buttons)
   - [Links with no href](#links-with-no-href)
   - [No advance warning when opening new window](#no-advance-warning-when-opening-new-window)
- [Images](#images)
   - [Images with no alt attribute](#images-with-no-alt-attribute)
   - [Meaningful images with meaningless alt attributes](#meaningful-images-with-meaningless-alt-attributes)
   - [Meaningless images with meaningful alt attributes](#meaningless-images-with-meaningful-alt-attributes)
   - [Redundant alt attributes](#redundant-alt-attributes)
   - [Brand logos](#brand-logos)
- [Page titles](#page-titles)
   - [Title doesn’t describe the page](#title-doesnt-describe-the-page)
   - [Same title used on multiple pages](#same-title-used-on-multiple-pages)
- [Headings](#headings)
   - [Headings used for styling](#headings-used-for-styling)
   - [Implied headings](#implied-headings)
   - [Multiple H1s per page](#multiple-h1s-per-page)
   - [Heading sequence is not logical](#heading-sequence-is-not-logical)
- [HTML Attributes](#html-attributes)
   - [Reliance on title attributes for accessibility](#reliance-on-title-attributes-for-accessibility)
   - [Redundant title attributes](#redundant-title-attributes)
- [Semantics](#semantics)
   - [No built-in semantics](#no-built-in-semantics)

## Keyboard navigation

### Missing or inadequate focus styles

#### What's the problem?

Focus styles are missing from interactive elements, or are present but difficult to see. 

#### Who's affected by the problem?

* Keyboard users
* Low vision users browsing with a magnifier

#### Why's it a problem?

Not everyone uses a mouse. Some users navigate through a page with their keyboard by pressing the <kbd>tab</kbd> key to move from one focusable element to another. If focus styles are removed or insufficient, these users have no way of knowing which element they are about to activate. 

All elements that receive focus MUST have visible focus styles. 

Browser default focus styles are likely insufficient as they can be difficult to see in some designs. We prefer focus styles to be highly visible. 

#### How do I fix it? 

We do this:
```css
a:focus {
   outline: 3px solid #fece3e;
}

a:focus, button:focus {
   background-color: #fc0;
   outline: 2px solid #fc0;
}
```

We _don't_ do this:
```css
a:focus {
   outline: 0;
}
```

### Visual order doesn't match source order

#### What's the problem?

CSS positioning has been used so that the visual order of interactive elements doesn't match the HTML source order. 

#### Who's affected by the problem?

* Keyboard users
* Screen reader users

#### Why's it a problem?

Keyboard users (including screen reader users) expect to tab forwards and backwards in a linear sequence. Switching the visual order of elements can confuse these users or cause them to activate the wrong control. 

#### How do I fix it? 

Make sure the visual order of components matches the order in the HTML source. Tab through your pages every so often just to make sure you haven't accidentally messed up the tab order.

We do this:
```html
<button> I Should </button>
<button> Be focused</button>
<button> Last </button>
```

We don't do this:
```html
<button style=”float: right”> I Should </button>
<button> Be focused</button>
<button> Last </button>
```

## Links and buttons

### Links with no href

#### What's the problem?

Anchors (`a` elements) without an `href` attribute have been used.

#### Who's affected by the problem?

* Keyboard users
* Voice input users

#### Why's it a problem?

Anchors (`a` elements) without an `href` attribute are placeholders for links, not true links. All true anchor links require an `href` attribute to be functional.  

Omitting the `href` attribute prevents keyboard users and voice input users from being able to use the link at all. 

#### How do I fix it? 

We do this:
```html
<a href=”#location”>Visit this location</a>
```
We _don’t_ do this:
```html
<a onclick=”myFunc();”>Visit this location</a>
```

### No advance warning when opening new window

#### What's the problem?

Links open in new window without warning the user that this will happen.

#### Who's affected by the problem?

* Screen reader users
* Low vision users who magnify the entire screen
* Users with cognitive challenges

#### Why's it a problem?

Having a window open unexpectedly when you click on a link can be disorientating to users who can only see a portion of the screen, who can't see the screen at all, or who can become easily distracted by unexpected changes to their browsing context. 

#### How do I fix it? 

Avoid opening links in new windows wherever possible. 

If you really have to do it, warn the user before they click on the link that it'll open in a new window. You can use text like "opens in a new window" or a visual icon. If you choose to use an icon, make sure it's accessible to screen reader users. 

Note: you MUST use `rel="noopener"` on outbound links that open in a new window. See the [secure markup guide](../security/secure-markup.md/#add-relnoopener-to-outbound-links-in-new-windows) for an explanation. 

We do this:
```html
<a href="https://mysite.com" target="_blank" rel="noopener">
   My site (opens in a new window)
</a>

 Or
 
<a href="https://mysite.com" target="_blank" rel="noopener">
   My site <img src="..." alt="opens in a new window"> 
</a> 
```

We don’t do this:
```html
<a href="knitting.html" target="_blank">All about Knitting</a>
```

## Images

### Images with no alt attribute

#### What's the problem?

An image has no alt attribute. 

#### Who's affected by the problem?

* Screen reader users
* All users if the image fails to load for any reason (network problems, server issues, etc.)

#### Why's it a problem?

* Screen reader users will hear the filename of the image read out instead, which likely will not tell them anything about the image, and in the case of auto-generated filenames presents a very poor user experience. 
* Users who can't see the image because of some kind of technical failure will have no idea what the image is supposed to represent.
* Alt is a required attribute on every `img` tag. Your HTML is invalid without it. 

#### How do I fix it? 

We do this:
```html
<img src="/images/NYCpark.png" alt="Aerial view of Central Park in New York" />
```

We don't do this:
```html
<img src="/images/NYCpark.png" />
```

### Meaningful images with meaningless alt attributes

#### What's the problem?

An image has poor alt text. The alt text may not describe the image properly, leave vital information out, or otherwise fail to provide the user with an adequate text alternative to the image. 

#### Who's affected by the problem?

* Screen reader users
* All users if the image fails to load for any reason (network problems, server issues, etc.)

#### Why's it a problem?

* Users who can't see the image because of some kind of technical failure will not understand what the image is supposed to represent.

#### How do I fix it? 

Alt text should be used to convey the intent of an image. 

Do not:
* Use generic strings with no descriptive content like “photo”, “image”, or “icon”
* Add useless descriptions that only make sense to you, the author, in the context of design elements, like "hero image"

We do this:
```html
<img src="/images/kinghenry.jpg" alt="King Henry VIII of England">
<img src="/images/icon-cart.png" alt="Cart">
```

We don't do this:
```html
 <img src="/images/kinghenry.jpg" alt="Image">
 <img src="/images/icon-cart.png" alt="Icon">
```

### Meaningless images with meaningful alt attributes

#### What's the problem?

A decorative image has been given alt text. 

#### Who's affected by the problem?

* Screen reader users

#### Why's it a problem?

Screen reader users do not need to know about images that convey no information. Adding alt text to these images forces these users to listen to information that they don't care about, and doesn't help them use the page. 

#### How do I fix it? 

If an image is decorative, the alt attribute should be present, but its value left blank. This conveys that the image isn’t necessary for understanding the page.

We do this:
```html
 <img src="/images/spacer.gif" alt="" />
 <img src="/images/bg_img.gif" alt="" />
```

We _don’t_ do this:
```html
 <img src="/images/spacer.gif" alt="spacer image" />
 <img src="/images/bg_img.gif" alt="background image" />
```

### Redundant alt text

#### What's the problem?

An image is situated adjacent to text that repeats the same information in the alt attribute. 

#### Who's affected by the problem?

* Screen reader users

#### Why's it a problem?

If an image represents information that is already available in text, screen reader users have to needlessly listen to multiple repetitions of the same information. 

#### How do I fix it? 

If the information is already available in adjacent text, the alt attribute should be present, but its value left blank. 

We do this:
```html
<div class=”person”><img src="/images/mrs-a-person.gif" alt=""><a href=”/”>Mrs. A. Person</a></div>
```

We _don’t_ do this:
```html
<div class=”person”><img src="/images/mrs-a-person.gif" alt="Mrs. A. Person" /><a href=”/”>Mrs. A. Person</a></div>
```

### Brand logos

#### What's the problem?

A brand logo has been given incorrect alternative text. It may incorporate unnecessary information, contain a meaningless string, or fail to show parity with the image. 

#### Who's affected by the problem?

* Screen reader users
* All users if the image fails to load for any reason (network problems, server issues, etc.)

#### Why's it a problem?

The purpose of a brand logo is for people to recognise the brand it represents. If the alt text fails to demonstrate this, then it's failed at its primary purpose. 

#### How do I fix it? 

The alt text for a brand logo should contain the name of the brand. If additional text is visible in the logo, that text must be included too. 

Do not:
* Use useless information like "logo"
* Use the alt text to add additional information or instructions

We do this:
```html
<img src="w3c.png" alt="W3C">
<img src="nature-logo.png" alt="Nature">
<img src="bmc-logo.png" alt="BMC - Part of Springer Nature">
```

We don't do this:
```html
<img src="w3c.png" alt="logo image">
<img src="nature-logo.png" alt="Click here to go to the Nature homepage">
<img src="bmc-logo.png" alt="BMC">
```

## Page titles

### Title doesn’t describe the page

#### What's the problem?

The `<title>` attribute fails to describe the purpose of the page. 

#### Who's affected by the problem?

* Everyone

#### Why's it a problem?

When your page titles are inadequate:

* Screen reader users are unable to know what the point of a page is without scanning its entire contents
* All users are unable to easily find the correct tab if they temporarily change contexts
* All users who bookmark the page with their browser are given a poor default name for the bookmark

#### How do I fix it? 

All page titles must clearly summarise the purpose of the page.

We do this:
```html
<title>Career opportunities | Website.com </title>
<title>Contact us | Website.com </title>
```
 
We _don’t_ do this:
```html
<title>Website.com</title>
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

## Headings  

### Headings used for styling

#### What's the problem?

Semantic heading tags (i.e. `<h1>`, `<h2>`, `<h3>`, `<h4>`, `<h5>`, `<h6>`) are being used purely to visually style text that doesn't head a section of content. 

#### Who's affected by the problem?

* Screen reader users
* Search engines

#### Why's it a problem?

Semantic tags have meaning. When you use a semantic tag for something other than its meaningful purpose, your document makes less sense. This is a severe issue for screen reader users, who need proper semantic structure in order to understand how your document is structured. 

Search engines also use heading levels to get a sense of the information that your page contains. If your document misuses semantic tags for visual effect, search engines are less able to parse the information in your document and your pages could be penalised in SERPs, or be less discoverable to search engine users. 

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

Search engines also use heading levels to get a sense of the information that your page contains. If your document omits semantic tags, search engines are less able to parse the information in your document and your pages could be penalised in SERPs, or be less discoverable to search engine users. 

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

Search engines also use heading levels to get a sense of the information that your page contains. If your document omits semantic tags, or uses them incorrectly, search engines are less able to parse the information in your document and your pages could be penalised in SERPs, or be less discoverable to search engine users. 

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

## HTML Attributes

### Reliance on title attributes for accessibility

#### What's the problem?

An element uses the `title=""` attribute to contain important information. This could be instructions on how to use an element, an explanation of what the element means, or some other kind of text that the user needs to be able to access in order to use the component. 

#### Who's affected by the problem?

* Screen reader users
* Touchscreen users
* Keyboard users
* Users who don't hover over the element long enough to realise that the title attribute exists

#### Why's it a problem?

The `title` attribute appears when a user hovers over the element that its applied to. Users who have no hover capability (e.g. those with touchscreens, or those using a keyboard or other Assistive Technology) are not able to access the content in this attribute. 

Exposure of the contents of the `title=""` attribute is also unreliable in screen readers. Some screen readers do not expose information provided in a `title` attribute to the user at all. 

#### How do I fix it? 

Avoid the use of the `title` attribute. The HTML 5 specification [explicitly discourages its use](https://www.w3.org/TR/html53/dom.html#the-title-attribute). 

We do this:
```html
<a href="...">My link location</a>
<span>Important instructions that the user needs to be able to read to understand the UI</span>
```

We _don’t_ do this:
```html
<a href="..." title="My link location"></a>
<span title="Important instructions that the user needs to be able to read to understand the UI"></span>
```

Note: There is one exception. A `title=""` is required on iframes to describe to the user what the purpose of the iframe is. Always use a title attribute on iframes. 

### Redundant title attributes

#### What's the problem?

An element has a `title=""` attribute that contains redundant information. It may simply repeat the text content of the element, include unnecessary information, or otherwise provide no value to the user. 

#### Who's affected by the problem?

* Screen reader users

#### Why's it a problem?

Some screen readers expose information provided in the `title=""` attribute to the user, in addition to the accessible name. This means that some screen reader users may have to listen to multiple unnecessary repetitions of the same information. 

Using a `title=""` attribute to contain basic explanations of how elements work is unnecessary and highly irritating for screen reader users. They do not need you to use the `title=""` attribute to explain to them that a link can be clicked on. 

#### How do I fix it?

Do not: 

* Replicate an accessible name in the `title=""` attribute
* Pad the `title=""` attribute with unnecessary text
* Use the `title=""` attribute to explain basic browser functionality

If the usage of your component is truly difficult to understand, the UX needs to be simplified, or you need to provide _visible_ instructions that be accessed by all users. 

We do this:
```html
<a href=”...”>Nature homepage</a>
<a href="...">BMC Annual Report 2018</a>
<a href="...">link.springer.com</a>
```

We _don’t_ do this:
```html
<a href=”...” title=”Nature homepage”>Nature homepage</a>
<a href="..." title="Biomedcentral has published its annual report">BMC Annual Report 2018</a>
<a href="..." title="Click this link to visit the SpringerLink website">link.springer.com</a>
```

## Semantics
 
### No built-in semantics

#### What's the problem?

Elements with no semantics (`<div>`s and `<span>`s) have been used instead of elements with the correct semantics. The elements may be styled with CSS to look like semantic elements, and/or have JavaScript functionality attached that makes them perform in a similar way to a native element, but the correct native element has not been used. 

#### Who's affected by the problem?

* Everyone

#### Why's it a problem?

Elements with no semantics (divs and spans) are not understood or handled automatically by user agents. Unless you fully understand the entire specification for a native element (such as a button), and implement it precisely to that specification, your attempts to replicate its functionality will fail. 

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
