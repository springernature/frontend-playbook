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
   - [Decorative SVG inside a control is focusable](#decorative-svg-inside-a-control-is-focusable)
   - [CSS background images have no accessible name](#css-background-images-have-no-accessible-name)
   - [Icon has no visible label](#icon-has-no-visible-label)
   - [Icon font in or as accessible name](#icon-font-in-or-as-accessible-name)
- [Page titles](#page-titles)
   - [Title doesn’t describe the page](#title-doesnt-describe-the-page)
   - [Same title used on multiple pages](#same-title-used-on-multiple-pages)
- [Language of page and parts](#language-of-page-and-parts)
  - [Specified language is incorrect](#specified-language-is-incorrect)
  - [Change in language not specified](#change-in-language-not-specified)
- [Headings](#headings)
   - [Headings used for styling](#headings-used-for-styling)
   - [Implied headings](#implied-headings)
   - [Multiple H1s per page](#multiple-h1s-per-page)
   - [Heading sequence is not logical](#heading-sequence-is-not-logical)
   - [Missing heading](#missing-heading)
- [HTML Attributes](#html-attributes)
   - [Reliance on title attributes for accessibility](#reliance-on-title-attributes-for-accessibility)
   - [Redundant title attributes](#redundant-title-attributes)
- [Semantics](#semantics)
   - [No built-in semantics](#no-built-in-semantics)
- [Focus management](#focus-management)
   - [No focus management](#no-focus-management)
   - [Inappropriate use of `autofocus`](#inappropriate-use-of-autofocus)
   - [Focus fails to return to triggering element](#focus-fails-to-return-to-triggering-element)
- [High magnification](#high-magnification)
  - [Content obscured at high magnification](#content-obscured-at-high-magnification)
  - [Information removed at high magnification](#information-removed-at-high-magnification)

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

Keyboard users (including screen reader users) expect to tab forwards and backwards through interactive elements in a linear sequence. For left-to-right languages, this means the elements should be presented in left-to-right order. 

Switching the visual order of elements with CSS but not changing the order in the source code can lead to focus being placed on unexpected elements, which can confuse users or cause them to activate the wrong control. 

For example, using a `float:right;` on an interactive element can make it visually appear to be the last control in a group, but when a keyboard user tabs into the component, it may be the first control they interact with. 

#### How do I fix it? 

* Take care when using CSS positioning, flexbox, and grid layouts
* Make sure the visual order of components matches the order in the HTML source
* Tab through your document to make sure the focus order is expected

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

Avoid opening links in new tabs or windows wherever possible. 

If you really have to do it, warn the user before they click on the link that it'll open in a new window. You can use text like "opens in a new window" or a visual icon. If you choose to use an icon, make sure it's accessible to screen reader users. 

You MUST use `rel="noopener"` on outbound links that open in a new window. See the [secure markup guide](../security/secure-markup.md/#add-relnoopener-to-outbound-links-in-new-windows) for an explanation. 

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

### Decorative SVG inside a control is focusable

#### What's the problem?

A decorative SVG (e.g. an icon) inside a control (e.g. a link or a button) is present, but tab focusing has not been explicitly disabled. 

The SVG may or may not have `aria-hidden="true"` applied to hide it from Assistive Technology. 

#### Who's affected by the problem?

* Screen reader users with IE
* Keyboard users with IE

#### Why's it a problem?

A bug in IE incorrectly gives SVGs inside a control the `focusable="true"` property by default. This can cause unexpected issues for sighted keyboard users, including loss of visible focus, and additional unnecessary tab stops. 

Applying `aria-hidden="true"` to an SVG removes it from the accessibility tree. Screen reader users on IE can still tab into it, but don't get any useful information about the element. 

#### How do I fix it? 

We do this:
```html
<a href="/">Link text <svg focusable="false">...</svg></a>

<button>Button text <svg focusable="false" aria-hidden="true">...</svg>

```

We _don't_ do this:
```html
<a href="/">Link text <svg>...</svg></a>

<button>Button text <svg aria-hidden="true">...</svg>
```

### CSS background images have no accessible name

#### What's the problem?

A CSS background image has been used to express information. This may a logo, an icon, or some other form of image that has meaning in the UI. 

#### Who's affected by the problem?

* Screen reader users
* Users experiencing technical problems (e.g. network connectivity issues, CDN failures, etc.)

#### Why's it a problem?

A CSS background image can't have alt text. Screen reader users are unaware of what the image represents, and in many cases are unaware it exists at all. 

If the stylesheets fail for any reason (usually because of technical problems), users don't get a graceful fallback for the missing image. 

#### How do I fix it? 

Use an HTML image with appropriate alt text for images that are meaningful. 

We do this:
```html
<img src="nature.png" alt="Nature">
```

We _don't_ do this:
```
<span class="nature-logo"></span>

.nature-logo { background-image: url("nature.png"); }
```

### Icon has no visible label

#### What's the problem?

An icon is used to express information, but there's no visible text label that describes what it does. If the icon is part of a control, it may be associated with visually-hidden text or have an `aria-label` property. 

#### Who's affected by the problem?

* Voice input users
* Visual display users who are unfamiliar with the meaning of the icon

#### Why's it a problem?

The purpose of an icon isn't always easy to guess. Some users who can see the icon may be confused about what it's trying to tell them.

If the icon has visually-hidden text or an `aria-label`, but it's not obvious what that label might be, a voice input user may not be able to guess the right thing to say to activate the control. 

#### How do I fix it? 

Unless the icon has a very obvious purpose and accessible name that almost all people would understand (e.g. an 'x' icon in a top corner to close a component), use a visible text label. This can be instead of or in addition to the icon. 

#### Where do I find out more? 

* [Icon Usability - Nielsen Norman Group](https://www.nngroup.com/articles/icon-usability/)

### Icon font in or as accessible name

#### What's the problem?

An icon font has been used to create an icon that expresses information. The icon may be the only accessible name, or part of a longer accessible name. 

#### Who's affected by the problem?

* Screen reader users
* Voice input users

#### Why's it a problem?

Icon fonts use CSS `content` to display an icon. 

Used alone, they have no usable accessible text and can't be understood by screen reader users. Some screen reader software may not announce CSS content, so some screen reader users may not be aware the icon exists at all. When used in a control, voice input users will be unable to guess the right thing to say to activate the control. 

When used alongside accessible text, the icon's font character may be read out by some screen reader software, which may confuse those users. 

#### How do I fix it? 

Hide supplementary font icons from assistive technology. Do not use a font icon as the only accessible text for a control. 

We do this:
```html
<button>Shopping cart <span class="ico-cart" aria-hidden="true"></span></button>
```

We _don't_ do this:
```html
<button><span class="ico-cart"></span></button>
```

## Page titles

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

## Language of page and parts

### Specified language is incorrect

#### What's the problem?

The language specified in the HTML `lang` attribute doesn't match the language used for the main page. 

#### Who's affected by the problem?

* Screen reader users

#### Why's it a problem?

Words are pronounced differently in different languages. Screen reader software is designed to respect these pronunciation differences when it encounters web pages that specify their main language. 

If the language specified doesn't match the actual language used, the screen reader software may mispronounce the text of the page. 

#### How do I fix it? 

Make sure the language specified in the `lang` attribute accurately reflects the language of the page. If you provide a translated version of a page, make sure you provide the correct `lang` attribute, too. 

We do this:
```html
<html lang="es">
  ...
  <title>Las razas estándar de gansos</title>


<html lang="en">
  ...
  <title>The Standard Breeds of Geese</title>
```

We _don't_ do this:
```html
<html lang="en">
  ...
  <title>Die Standardrassen von Gänsen</title>
```

### Change in language not specified

#### What's the problem?

An element on the page contains text in a different language to the rest of the page, but the change in language isn't signalled with a `lang` attribute. 

#### Who's affected by the problem?

* Screen reader users

#### Why's it a problem?

Words are pronounced differently in different languages. Screen reader software is designed to respect these pronunciation differences when it encounters components on web pages that specify a change in language. 

If a piece of text in a document is presented in a different language without programmatically indicating the change, the screen reader software may mispronounce the text. 

#### How do I fix it? 

If you have text on a web page that is in a different language to the rest of the page, include the appropriate `lang` attribute in its wrapping element. 

We do this:
```html
<html lang="es">
  ...
  <title>Las razas estándar de gansos</title>
  ...
  <p lang="fr">C'est un belle journee sur le village, et tu es un méchant oie.</p>
```

We _don't_ do this:
```html
<html lang="en">
  ...
  <title>The Standard Breeds of Geese</title>
  ... 
  <p>C'est un belle journee sur le village, et tu es un méchant oie.</p>
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

When you change context or open a new section, use a heading to group the content. 

It may help to think about the heading structure of a web page as its table of contents. A ToC contains a reference to everything on the page - your heading structure should do the same. 

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

There is one exception. A `title=""` is required on iframes to describe to the user what the purpose of the iframe is. Always use a title attribute on iframes. 

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

## Focus management

### No focus management

#### What's the problem?

Programmatic focus is absent. You may have written an SPA that fails to handle focus management automatically, or you may have neglected to implement programmatic focus on a component that changes the user's context (e.g. a modal dialog).

#### Who's affected by the problem?

* Screen readers
* Keyboard users

#### Why's it a problem?

"Focus management" is the practice of setting the user's current focus programmatically. 

Most SPA frameworks fail to handle this automatically, and you need to implement it yourself. When a user activates a control to trigger a route change, the view visually updates. When you don't implement focus management, screen reader users are not made aware that the context has changed, and are left guessing whether or not activating the control did anything. Keyboard users may be able to see the visual changes, but they're left with their keyboard focus still on the trigger control. The control is no longer visible on the screen and may require additional, unnecessary work from the keyboard user to get reoriented. 

Implementing ARIA patterns that require focus management (e.g. modal dialogs), but neglecting to implement that focus management can also confuse users or prevent them from being able to use your document.  

#### How do I fix it?

Watch this video by Google Developer Advocate Rob Dodson on [Managing Focus (7:23)](https://www.youtube.com/watch?v=srLRSQg6Jgg&list=PLNYkxOF6rcICWx0C9LVWWVqvHlYJyqw7g&index=23&t=0s) for a demonstration of the problem and an explanation of how to fix it. 

If you're building a component that has an ARIA pattern (e.g. a modal dialog), follow the ARIA specification for the pattern you're using. Watch this video by Rob Dodson on [Accessible Modal Dialogs (12:45)](https://www.youtube.com/watch?v=JS68faEUduk&list=PLNYkxOF6rcICWx0C9LVWWVqvHlYJyqw7g&index=19) to see an example of how to apply the ARIA specification to a modal dialog. 

If you're building a SPA with a JavaScript framework, check for the correct way to enable focus management on router view changes. Read [Single Page Apps routers are broken](https://medium.com/@robdel12/single-page-apps-routers-are-broken-255daa310cf) by Robert DeLuca to get some suggestions that may work for your framework. 

### Inappropriate use of `autofocus`

#### What's the problem?

The `autofocus` attribute in a form field has been used to programmatically set focus in a way that's detrimental to the user experience. 

#### Who's affected by the problem?

* Screen reader users
* Keyboard users
* Touch device users
* Low vision users

#### Why's it a problem?

The `autofocus` attribute can be used to programmatically set the user's focus to a specific form field. 

If the field is not the only thing on the page, or if it comes after a number of other controls or pieces of content, screen reader users may miss all of the content that precedes the field. 

Keyboard users may be confused about the location of their focus, expecting it start at the top of the screen, and may become frustrated if they can't orient themselves. 

The autofocus behaviour can cause dynamic keyboards to display on some touch devices. In some cases, the autofocus behaviour can cause the browser to automatically scroll to the automatically-focused form field, disorienting users who can only see a portion of the screen (e.g. low vision users browsing at high magnification). 

#### How do I fix it?

The `autofocus` attribute is rarely helpful. If the user can perform multiple tasks on the page, or if the automatically-focused form field comes after other page content, then the `autofocus` attribute should not be used. 

### Focus fails to return to triggering element

#### What's the problem?

Upon some interaction, focus has been programmatically placed inside a component. When that component is closed, the user's focus is not returned to where it was before the new behaviour was triggered. 

#### Who's affected by the problem?

* Keyboard users
* Screen reader users

#### Why's it a problem?

Users expect consistency in an interface. Sometimes you need to programmatically set a user's focus in a component so they can carry out a task. If you don't return their focus afterwards to what they were doing before, it can be very confusing for users who navigate with the keyboard. 

If focus is placed on an unexpected or unrelated element, then the user might activate the wrong thing or struggle to work out where they are on the page. 

If focus is kept on a component that has been moved off-screen or hidden, a keyboard user will have a difficult time working out how they can get back to interacting with the visible components. 

If focus is lost entirely, then the browser will automatically return it to the top of the page. Keyboard and screen reader users will have a frustrating time getting back to where they were before you interrupted them. 

#### How do I fix it? 

Whenever you use programmatic focus to orient a user in some component (e.g. a menu or a modal dialog), make sure that their focus is returned to the invoking element when that component is closed. For example, if the component was invoked by activating a button, when the component is closed, focus must be returned to that button. 

If there was no invoking element (e.g. your component automatically appears when some JavaScript loads), return the user's focus to whatever they were interacting with before you manipulated their focus. 

## High magnification

### Content obscured at high magnification

#### What's the problem?

When the screen is magnified, content is obscured. Text or functionality may be pushed off-screen. Elements may overlap with or cover up other elements. 

#### Who's affected by the problem?

* Low-vision users

#### Why's it a problem?

Low-vision users may need to zoom or magnify content in their browsers to be able to use a website. If content or functionality is obscured when they do this, they may be unable to read or use the website. 

#### How do I fix it? 

Use a [responsive design](https://www.smashingmagazine.com/2011/01/guidelines-for-responsive-web-design/). 

Make sure that nothing in your layout becomes visually obscured down to a width of 320px. 

### Information removed at high magnification

#### What's the problem?

When the screen is magnified (or when using a mobile layout), important information is removed. Text labels for icons may be removed from the UI, or menu items could be lost. 

#### Who's affected by the problem?

* Low-vision users
* Mobile device users

#### Why's it a problem?

Low-vision users may need to zoom or magnify content in their browsers to be able to use a website. In a responsively-designed website, this may effectively put them into the "mobile" layout. 

Removing information for visual effect may make it difficult for these users to interpret content, or move around the site effectively.

#### How do I fix it? 

Avoid "hiding" content in mobile layouts - if it's important enough to display on desktop, it's important enough to display on mobile. 

Make sure that the "mobile" content has parity with the "desktop" content. 
