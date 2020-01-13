# Common remediations

This page describes some common accessibility issues, and gives examples and suggestions for repairs. 


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


### Interactive components not accessible by keyboard

#### Unsemantic elements used for interactive components

Built-in interactive HTML elements like anchors, text fields, buttons, and select lists (among others) are handled automatically by the browser. Users can interact with them with the mouse, the keyboard, by voice, or any other kind of technology that they like. 

Elements with no semantics (divs and spans) don’t have this automatic handling, and a simple `onclick` handler doesn’t provide it. These elements generally can’t be interacted with by users of Assistive Technology unless you write large amounts of JavaScript to make it possible. 

Where a built-in interactive element is available, use it. 

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


#### Links with no href

All anchor links (the `a` element) require an `href` attribute in order to be functional as links. Omitting the `href` attribute prevents keyboard users and voice input users from being able to use the link at all. 

We do this:
```html
<a href=”#location”>Visit this location</a>
```
We _don’t_ do this:
```html
<a onclick=”myFunc();”>Visit this location</a>
```



####  Inappropriate negative tabindex

Interactive elements with a negative tabindex attribute (`tabindex=-1`) are not usable by keyboard users. 



### Visual order is not followed with source code
Just try to follow the visual order of elements while coding in HTML, don’t adjust elements to take positions with CSS, then this is confusing to keyboard users who expect to tab forwards and backwards in a linear sequence.

As a rule, try tabbing through your pages every so often just to make sure you haven't accidentally messed up the tab order. 

We do this:
```html
<button> I Should </button>
<button> Be focused<button />
<button> Last <button />
```

We don't do this:
```html
<button style=”float: right”> I Should <button />
<button> Be focused<button />
<button> Last <button />
```



### No advance warning when opening new window 

Opening new windows automatically when a link is activated can be disorienting for people who have difficulty perceiving visual content, and for some people with cognitive disabilities, if they are not warned in advance.

We do this:
```html
<a href="https://mysite.com" target="_blank" rel="noopener">
 My site
 <span class="visuallyhidden">, opens in a new window</span>
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
Make sure any text in images of text is at least 14 points and has good contrast with the background.

We do this:
```html
<a href="https://www.w3.org/"> <img src="w3c.png" alt="W3C"></a>
```

We don't do this:
```html
<a href="https://www.w3.org/"> <img src="w3c.png" title="homepage" alt="logo image"></a>
```
