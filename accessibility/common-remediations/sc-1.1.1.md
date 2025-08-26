# Success Criterion 1.1.1 Non-text content

Non-text content such as images that present information to the user must have a text alternative that serves the equivalent purpose. This allows users who can't see an image or other non-text content, for any reason, not to be disadvantaged by information not being visible to them. 

See [Understanding Non-text Content](https://www.w3.org/WAI/WCAG22/Understanding/non-text-content.html) for further details. 

The issues and remediations listed in this file are not exhaustive. 

## The issues

- [No accessible text on controls](#no-accessible-text-on-controls)
- [Images](#images)
	- [Images with no alt attribute](#images-with-no-alt-attribute)
	- [Meaningful images with meaningless alt attributes](#meaningful-images-with-meaningless-alt-attributes)
	- [Meaningless images with meaningful alt attributes](#meaningless-images-with-meaningful-alt-attributes)
	- [Redundant alt text](#redundant-alt-text)
	- [Brand logos](#brand-logos)
	- [SVG inside a control is independently focusable](#svg-inside-a-control-is-independently-focusable)   
	- [CSS background images have no accessible name](#css-background-images-have-no-accessible-name)
	- [Icon has no visible label](#icon-has-no-visible-label)
	- [Icon font in or as accessible name](#icon-font-in-or-as-accessible-name)
- [Title attributes](#title-attributes)
	- [Reliance on title attributes for accessibility](#reliance-on-title-attributes-for-accessibility)
	- [Redundant title attributes](#redundant-title-attributes)


### No accessible text on controls

#### What's the problem?

A control has no accessible text. Buttons or links may have no text in them, or have CSS content as their only content.

Alternatively, text may exist but be overridden by faulty ARIA. This could mean an empty label (`aria-label=""`), or an attempt to associate the control with another element using `aria-labelledby` where the associated element doesn't exist in the document. 

#### Who's affected by the problem?

* Screen reader users
* Voice input users
* All users if a stylesheet containing CSS content fails to load for any reason (network problems, server issues, etc.)

#### Why's it a problem?

Controls with no accessible text can't be understood by screen reader users. CSS content isn't always exposed to Assistive Technology, and can't be relied on to provide context for screen readers. 

Controls with no accessible text can't be targeted by voice input users; they may be able to see the control but not interact with it. 

CSS content isn't part of the DOM, and may not be exposed to or by Assistive Technology. If CSS content is the only content of an control, Assistive Technology may treat the control as having no accessible text. 

ARIA labels invisibly override the native text in a control. If ARIA is used to incorrectly override native text with a blank string, or to refer to an element ID that doesn't exist in the document, the native text will no longer be accessible to Assistive Technology users. 

#### How do I fix it? 

We do this:
```html
<a href="/">Open control panel</a>

<button>Perform an action</button>
```

We _don't_ do this:
```
<a href="/" class="open-control-panel"></a>
...
.open-control-panel {
  content: "Open control panel";
}

<button class="perform-an-action"></button>
...
.perform-an-action {
  background-image: url('perform-an-action.svg');
}

<a href="/" aria-label="">Open control panel</a>
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

## Title attributes

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
