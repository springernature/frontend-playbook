# Images

Images that present information to the user must have a text alternative that serves the equivalent purpose. This allows users who can't see an image for any reason not to be disadvantaged by information not being visible to them. 

See [Understanding Success Criterion 1.1.1 Non-text Content](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content.html) for further details. 

## The issues

   - [Images with no alt attribute](#images-with-no-alt-attribute)
   - [Meaningful images with meaningless alt attributes](#meaningful-images-with-meaningless-alt-attributes)
   - [Meaningless images with meaningful alt attributes](#meaningless-images-with-meaningful-alt-attributes)
   - [Redundant alt attributes](#redundant-alt-attributes)
   - [Brand logos](#brand-logos)
   - [SVG inside a control is independently focusable](#svg-inside-a-control-is-independently-focusable)
   - [CSS background images have no accessible name](#css-background-images-have-no-accessible-name)
   - [Icon has no visible label](#icon-has-no-visible-label)
   - [Icon font in or as accessible name](#icon-font-in-or-as-accessible-name)


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

### SVG inside a control is independently focusable

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

If you would like the SVG to be available to assistive technologies (e.g. it has important alt text that the user would need in order to understand what the control does):

We do this:
```html
<a href="/">Link text <svg focusable="false">...</svg></a>

<button>Button text <svg focusable="false">...</svg>

```

If you would **not** like the SVG to be available to assistive technologies (if it is purely decorative):

We do this:
```html
<a href="/">Link text <svg focusable="false" aria-hidden="true">...</svg></a>

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
