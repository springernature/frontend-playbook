# Common remediations

This page describes some common accessibility issues, and gives examples and suggestions for repairs. 


- [Keyboard navigation](#keyboard-navigation)
  - [Missing or inadequate focus styles](#missing-or-inadequate-focus-styles)
  - [Visual order is not followed with source code](#visual-order-is-not-followed-with-source-code)
    
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

Not everyone uses a mouse. Some users navigate through a page with their keyboard by pressing the <kbd>tab</kbd> key to move from one focusable element to another. If focus styles are removed or insufficient, these users have no way of knowing which element they are about to activate. 

All elements that receive focus MUST have visible focus styles. 

Browser default focus styles are likely insufficient as they can be difficult to see in some designs. We prefer focus styles to be highly visible. 


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



### Visual order is not followed with source code
Just try to follow the visual order of elements while coding in HTML, don’t adjust elements to take positions with CSS, then this is confusing to keyboard users who expect to tab forwards and backwards in a linear sequence.

As a rule, try tabbing through your pages every so often just to make sure you haven't accidentally messed up the tab order. 

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

All anchor links (the `a` element) require an `href` attribute in order to be functional as links. Omitting the `href` attribute prevents keyboard users and voice input users from being able to use the link at all. 

We do this:
```html
<a href=”#location”>Visit this location</a>
```
We _don’t_ do this:
```html
<a onclick=”myFunc();”>Visit this location</a>
```


### No advance warning when opening new window 

Avoid opening links in new windows
This can be disorientating to screen reader users or users with cognitive disabilities.

If you must do it, warn the user before they click on the link that it'll open in a new window. You can use text like "opens in a new window" or a visual icon. If you choose to use an icon, make sure it's accessible to screen reader users.

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

Alt attributes are required on all `img` tags. Your HTML is invalid without them. 

We do this:
```html
<img src="/images/NYCpark.png" alt="Aerial view of Central Park in New York" />
```

We don't do this:
```html
<img src="/images/NYCpark.png" />
```


### Meaningful images with meaningless alt attributes

Alt text should be used to convey the intent of an image. Avoid using generic strings like “photo”, “image”, or “icon” as alt values, as they don’t communicate valuable content to the user. Be as descriptive as possible.

We do this:
```html
<img src="/images/kinghenry.jpg" alt="King Henry VIII of England">
```

We don't do this:
```html
 <img src="/images/kinghenry.jpg" alt="Image of King">
```



### Meaningless images with meaningful alt attributes

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



### Redundant alt attributes
If an image represents information that is already available in text, the alt attribute should be present, but its value left blank. This prevents screen reader users from having to listen to multiple repetitions of the same information. 

We do this:
```html
<div class=”person”><img src="/images/mrs-a-person.gif" alt=""><a href=”/”>Mrs. A. Person</a></div>
```

We _don’t_ do this:
```html
<div class=”person”><img src="/images/mrs-a-person.gif" alt="Mrs. A. Person" /><a href=”/”>Mrs. A. Person</a></div>
```



### Brand logos

For an image `alt` attribute is sufficient and more meaningful.
No need of title attribute, use an inline image with an alt attribute for the brand logo.

We do this:
```html
<a href="https://www.w3.org/"> <img src="w3c.png" alt="W3C"></a>
```

We don't do this:
```html
<a href="https://www.w3.org/"> <img src="w3c.png" title="homepage" alt="logo image"></a>
```

## Page titles

### Title doesn’t describe the page

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

The purpose of the level 1 heading is to describe the topic of the page; it’s approximately equivalent to the page title. Do not use more than one level heading per page. 


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

Headings must have logical sequence., the heading structure of a web page is like its table of contents.

We do this:

```html 
<h1>Homepage </h1>
  <h2> Headline Topic 1 </h2>
     <h3> News Headline 1 </h3>
     <h3> News Headline 2 </h3>
        <h4> News Headline subtopic </h4>
  <h2> Headline Topic 2 </h2>
     <h3> News Headline 1 </h3>
     <h3> News Headline 2 </h3>
        <h4> News Headline subtopic </h4>
```
 

We _don't_ do this:

```html
<h1>My Hobbies</h1>
<p>These all are activities I love to do on a regular basis.</p>
<h2>Physical Activities</h2>
<h4>Playing Soccer</h4>
<p>Soccer is a team sport played between two teams of eleven players with a spherical ball.</p>
<h3>Dancing</h3>
```


## HTML Attributes

### Reliance on title attributes for accessibility

Avoid the use of the `title` attribute for any purpose beyond naming a frame or iframe. The HTML 5 specification [explicitly discourages its use](https://www.w3.org/TR/html53/dom.html#the-title-attribute). 

The `title` attribute can’t be perceived by touchscreen device users, as there’s no `hover` event available to them. Some screen readers do not expose information provided in a `title` attribute to the user. 

We do this:
```html
<iframe title="My iframe content" src="..."></iframe>

<frame title="My frame content"></frame>
```

We _don’t_ do this:
```html
<a href="..." title="My link location"></a>

<span title="Important instructions that the user needs to be able to read to understand the UI"></span>
```


### Redundant title attributes

Some screen readers do expose information provided in a `title` attribute to the user, in addition to the accessible name (i.e. a screen reader may say both strings). Do not replicate an accessible name in the title attribute. 

We do this:
```html
<a href=”...”>My cool site</a>

<button>My cool button</button>
```

We _don’t_ do this:
```html
<a href=”...” title=”My cool site”>My cool site</a>

<button title=”My cool button”>My cool button</button>
```


## Semantics
 
### No built-in semantics
 
Elements with no semantics (divs and spans) are not understood or handled automatically by user agents. Use native HTML elements unless you have a good reason not to.
 
We do this:

```html
<button>Toggle UI</button>
<a href=”/”>Visit this location</a>
```

We _don’t_ do this:

```html
<div onclick=”doFunc();”>Toggle UI</div>
<span>Visit this location</a>
```
