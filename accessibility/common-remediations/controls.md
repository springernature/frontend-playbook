# Controls

All controls must be fully operable, and properly named and identified. 

Issues with controls (e.g. links or buttons) can cause failures in every category of WCAG's main principles - they can prevent components from being Percievable, Operable, Understandable, and Robust. 

## The issues

- [Links with no href](#links-with-no-href)
- [No advance warning when opening new window](#no-advance-warning-when-opening-new-window)
- [No accessible text on controls](#no-accessible-text-on-controls)

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
