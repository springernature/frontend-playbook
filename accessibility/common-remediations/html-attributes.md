# HTML Attributes

## The issues

- [Reliance on title attributes for accessibility](#reliance-on-title-attributes-for-accessibility)
- [Redundant title attributes](#redundant-title-attributes)

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